# Use a base image with Go and Node.js installed
FROM golang:latest as builder

# Set up the working directory
WORKDIR /app

# Copy your Go file into the container
COPY . .

RUN go install golang.org/dl/go1.21rc2@latest

# Compile the Go file to WebAssembly
RUN GOOS=wasip1 GOARCH=wasm go1.21rc2 build -o output.wasm main.go

# Use a separate stage for the runtime environment
FROM ubuntu:20.04

# Install apt dependencies
RUN apt-get update && \
    apt-get install -y curl tar xz-utils

# Install the wasmtime CLI globally
RUN curl https://wasmtime.dev/install.sh -sSf | bash

# Set up the working directory
WORKDIR /app

# Copy the compiled WebAssembly file from the previous stage
COPY --from=builder /app/output.wasm .

# Run the WebAssembly file using wasmtime
CMD ["wasmtime", "run", "output.wasm"]

