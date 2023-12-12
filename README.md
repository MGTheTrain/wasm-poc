# wasm-sample

## Table of Contents

- [Summary](#summary)
- [References](#references)
- [How to use](#how-to-use)

## Summary

A collection showcasing how to generate WASM from various programming languages and execute the WASM code using a WASM runtime.

## References

TBD

## How to use

### simple-go sample

Run following commands:

```sh
cd samples/simple-go
docker build -t simple-go-wasm-app:stable .
docker run simple-go-wasm-app:stable
```

### simple-rust sample
