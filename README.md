# wasm-sample

## Table of Contents

- [Summary](#summary)
- [References](#references)
- [How to use](#how-to-use)

## Summary

A collection showcasing how to generate WASM from various programming languages and execute the WASM code using a WASM runtime.

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
docker run --rm simple-go-wasm-app:stable
```