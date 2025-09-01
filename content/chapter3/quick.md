+++
title = "Quick Start"
weight = 1
+++

## 1. Install the VSCode Extension
Install [`TYML for VSCode`](https://marketplace.visualstudio.com/items?itemName=bea4dev.tyml-lsp-vscode) from the VSCode Marketplace.

![tyml_vscode](https://tyml-org.github.io/tyml-docs-jp/chapter3/tyml_vscode.png)

## 2. Define Your API
Create a file named `api.tyml` anywhere.
```tyml
interface API {
    function hello() -> string {
        return "Hello, world!"
    }
}
```

## 3. Install TYML CLI Tools
Install with the following command (requires Rust’s cargo):
```bash
cargo install tyml_core tyml_api_generator
```

## 4. Generate Code and Implement
In this example, the server is Rust and the client is TypeScript.

### Server (Rust)
First, create a test crate.
```bash
cargo new api-example-server
```
Then generate types using the `api.tyml` defined in step 2.
```bash
tyml-api-gen server rust-axum api.tyml ./api-example-server/api
```
If you see `Success!`, it worked.

Add the generated `api` plus `async-trait` and `tokio` to `Cargo.toml`:
```toml
[dependencies]
api = { path = "./api/" }
async-trait = "0.1"
tokio = { version = "1", features = ["full"] }
```
Finally, edit `main.rs` to implement the API.
```rs
use api::{serve, types::API};
use async_trait::async_trait;

struct Server {}

#[async_trait]
impl API for Server {
    async fn hello(&self) -> String {
        "Hello, world!".to_string()
    }
}

#[tokio::main]
async fn main() {
    let server = Server {};

    serve(server, "localhost:3000").await.unwrap();
}
```

### Client
Generate TypeScript types.
```bash
tyml-api-gen client typescript api.tyml ./api-example-client/api
```
Then create `main.ts` inside `./api-example-client` and call the API.
```ts
import { API } from "./api/types.ts";

async function main() {
    const api = new API("http://localhost:3000")

    /// Call it like a method
    const result = await api.hello()

    console.log(result)
}

main()
```

## 5. Run
Run the following commands in the server and client directories respectively.

### Server
```bash
cargo run
```

### Client
```bash
npx tsx main.ts
```

### Result
If the client prints `Hello, world!`, it worked.
