# WASM Demo

## Wasmtime

> <https://wasmtime.dev/>

1. Install
    1. window : <https://github.com/bytecodealliance/wasmtime/releases/download/dev/wasmtime-dev-x86_64-windows.msi>
    2. linux : ```curl https://wasmtime.dev/install.sh -sSf | bash```
2. Code
    1. Rust

``` rust
fn main() {
    println!("Hello, world!");
}
```

``` shell
$ rustup target add wasm32-wasip1
$ rustc hello.rs --target wasm32-wasip1
$ wasmtime hello.wasm
Hello, world!
```

## wasm-pack

1. Install

    ``` shell
    cargo install wasm-pack
    ```
