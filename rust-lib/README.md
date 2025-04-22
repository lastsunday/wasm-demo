# Getting Started with WebAssembly

> modify from <https://dev.to/codesolutionshub/the-rise-of-wasm-webassembly-in-2024-why-every-developer-should-care-6i0>

To start using WASM, you need to understand its core components and how to compile code into WASM format.

## 1. Setting Up Your Environment

You can use various tools and languages to start developing with WASM. Here’s a simple example using Rust, one of the most popular languages for WASM development:

1. Install Rust: Follow the instructions on the official Rust website to install Rust.
1. Install the wasm-pack Tool: This tool helps compile Rust code to WebAssembly. 

    ```shell
    cargo install wasm-pack
    ```

## 2. Writing and Compiling Your First WASM Module

Create a new Rust project:

```shell
cargo new rust-lib --lib
cd rust-lib
```

Add the following Rust code in Cargo.toml:

```toml
[lib]
crate-type = ["cdylib", "rlib"]

[features]
default = ["console_error_panic_hook"]

[dependencies]
wasm-bindgen = "0.2.84"

# The `console_error_panic_hook` crate provides better debugging of panics by
# logging them with `console.error`. This is great for development, but requires
# all the `std::fmt` and `std::panicking` infrastructure, so isn't great for
# code size when deploying.
console_error_panic_hook = { version = "0.1.7", optional = true }

[dev-dependencies]
wasm-bindgen-test = "0.3.34"

[profile.release]
# Tell `rustc` to optimize for small code size.
opt-level = "s"
```

Add the following Rust code in src/lib.rs:

``` rust
use wasm_bindgen::prelude::*;

#[wasm_bindgen]
pub fn greet() -> String {
    "Hello, WebAssembly!".to_string()
}
```

Compile the Rust code to WASM:

``` shell
wasm-pack build --target web
```

This command generates a WASM module and the necessary JavaScript glue code to run the module in the browser.

### 3. Running WASM in the Browser

Create an HTML file to load and execute the WASM module:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Hello WASM</title>
</head>
<body>
  <h1 id="greeting"></h1>
  <script type="module">
    import init, { greet } from './pkg/rust_lib.js';

    async function runWasm() {
      await init();
      document.getElementById("greeting").textContent = greet();
    }

    runWasm();
  </script>
</body>
</html>
```

``` shell
cargo install simple-http-server
simple-http-server --nocache --index ./
```

#### quick dev

```shell
wasm-pack build --target web && simple-http-server --nocache --index  ./
```

access <http://127.0.0.1:8000>