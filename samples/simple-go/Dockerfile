# Use a base image with Go and Node.js installed
FROM golang:latest as builder

# Set up the working directory
WORKDIR /app

# Copy your Go file into the container
COPY . .

# Compile the Go file to WebAssembly
RUN GOARCH=wasm GOOS=js go build -o output.wasm main.go

# Use a separate stage for the runtime environment
FROM node:latest

# Install the wasmer CLI globally
RUN npm install -g @wasmer/cli

# Set up the working directory
WORKDIR /app

# Copy the compiled WebAssembly file from the previous stage
COPY --from=builder /app/output.wasm .

# Run the WebAssembly file using wasmer
CMD ["wasmer", "run", "output.wasm"]