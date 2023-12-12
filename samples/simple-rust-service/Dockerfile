# Use a base image 
FROM ubuntu:20.04 as builder

ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && \
    apt-get install -y curl

# Install Rust ecosystem
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

# Set up the working directory
WORKDIR /app

# Copy the Rust code into the container
COPY . .

# Set the HOME environment variable (if it's not already set)
ENV HOME /root

# Add $HOME/.cargo/bin to the PATH environment variable
RUN echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc

# Set the PATH for the current session
ENV PATH="/root/.cargo/bin:${PATH}"

# Add target module
RUN rustup target add wasm32-wasi

# Install the wasm-pack tool for building WebAssembly
RUN cargo build --target wasm32-wasi

# Use a separate stage for the runtime environment
FROM ubuntu:20.04

# Install apt dependencies
RUN apt-get update && \
    apt-get install -y curl tar xz-utils

# Install the wasmtime CLI globally
RUN curl https://wasmtime.dev/install.sh -sSf | bash

# Add $HOME/.wasmtime/bin to the PATH environment variable
RUN echo 'export PATH="$HOME/.wasmtime/bin:$PATH"' >> ~/.bashrc

# Set the PATH for the current session
ENV PATH="/root/.wasmtime/bin:${PATH}"

# Set up the working directory
WORKDIR /app

# Copy the compiled WebAssembly file from the previous stage
COPY --from=builder /app/target/wasm32-wasi/debug/simple-rust-service.wasm .