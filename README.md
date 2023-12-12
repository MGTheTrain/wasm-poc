# wasm-sample

## Table of Contents

- [Summary](#summary)
- [References](#references)
- [How to use](#how-to-use)

## Summary

A collection showcasing how to generate WASM from various programming languages and execute the WASM code using a WASM runtime. 

**NOTE:** HTTP services might be hard to compile since socket support might not yet be available in Wasi. Therefore search in [following link for `socket support`](https://atamel.dev/posts/2023/06-26_compile_rust_go_wasm_wasi/). Optionally check further projects:
- [runwasi - Facilitates running Wasm / WASI workloads managed by containerd](https://github.com/containerd/runwasi)
- [spin - Spin is the open source developer tool for building and running serverless applications powered by WebAssembly.](https://github.com/fermyon/spin)

## References

- [Compile Rust & Go to a Wasm+Wasi module and run in a Wasm runtime](https://atamel.dev/posts/2023/06-26_compile_rust_go_wasm_wasi/)

## How to use

### simple-rust sample

Run following commands:

```sh
cd samples/simple-rust
docker build -t simple-rust-wasm-app:stable .
docker run --rm simple-rust-wasm-app:stable bash -c "wasmtime run simple-rust.wasm"
```

### simple-go sample

Run following commands:

```sh
cd samples/simple-go
docker build -t simple-go-wasm-app:stable .
docker run --rm simple-go-wasm-app:stable bash -c "wasmtime run output.wasm"
```

### simple-rust-service

Run following commands to spin up a serverless application powered by WebAssembly:

```sh
cd samples/simple-rust-service
# Update in the `spin.toml` the cargo command
spin build # Build WebAssembly file
spin up # Run serverless HTTP service powered by WebAssembly
```

**NOTE:** Spin was installed and utilized with Ubuntu WSL