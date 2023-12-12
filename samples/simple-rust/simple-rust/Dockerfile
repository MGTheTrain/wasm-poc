# Use a base image with Rust installed
FROM rust:latest as builder

# Set up the working directory
WORKDIR /app

# Copy your Rust code into the container
COPY . .

# Install the wasm-pack tool for building WebAssembly
RUN curl https://rustwasm.github.io/wasm-pack/installer/init.sh -sSf | sh

# Compile the Rust code to WebAssembly
RUN wasm-pack build --target web --out-name output --out-dir .

# Use a separate stage for the runtime environment
FROM node:latest

# Install the wasmer CLI globally
RUN npm install -g @wasmer/cli

# Set up the working directory
WORKDIR /app

# Copy the compiled WebAssembly files from the previous stage
COPY --from=builder /app/pkg .

# Run the WebAssembly file using wasmer
CMD ["wasmer", "run", "output_bg.wasm"]