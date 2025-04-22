# Getting Started with WebAssembly

> <https://dev.to/codesolutionshub/the-rise-of-wasm-webassembly-in-2024-why-every-developer-should-care-6i0>

To start using WASM, you need to understand its core components and how to compile code into WASM format.

## 1. Setting Up Your Environment

You can use various tools and languages to start developing with WASM. Here’s a simple example using Rust, one of the most popular languages for WASM development:

1. Install Rust: Follow the instructions on the official Rust website to install Rust.
1. Install the wasm-pack Tool: This tool helps compile Rust code to WebAssembly. codecargo install wasm-pack

### Window error

1. error occurred in cc-rs: failed to find tool "clang": program not found (see https://docs.rs/cc/latest/cc/#compile-time-requirements for help)

install https://www.msys2.org/

## 2. Writing and Compiling Your First WASM Module

Create a new Rust project:

```shell
cargo new hello-wasm --lib
cd hello-wasm
```

Add the following Rust code in src/lib.rs:

``` rust
#[no_mangle]
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
    import init, { greet } from './pkg/rust-lib.js';

    async function runWasm() {
      await init();
      document.getElementById("greeting").textContent = greet();
    }

    runWasm();
  </script>
</body>
</html>
```

Open the HTML file in a web browser to see the message “Hello, WebAssembly!”.