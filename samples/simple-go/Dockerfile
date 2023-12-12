# Use a base image with Go and Node.js installed
FROM ubuntu:20.04 as builder

# Set up the working directory
WORKDIR /app

# Copy the Go file into the container
COPY . .

# Install apt dependencies
RUN apt-get update && \
    apt-get install -y wget tar

ARG GO_VERSION=1.21.5

# Download and Install go
RUN wget https://dl.google.com/go/go${GO_VERSION}.linux-amd64.tar.gz

# Extract tar.gz
RUN tar -C /usr/local/ -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz

# Add /usr/local/go/bin to the PATH environment variable
RUN echo 'export PATH="/usr/local/go/bin:$PATH"' >> ~/.bashrc

# Set the PATH for the current session
ENV PATH="/usr/local/go/bin:$PATH"

# Compile the Go file to WebAssembly
RUN GOOS=wasip1 GOARCH=wasm go build -o output.wasm main.go

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
COPY --from=builder /app/output.wasm .