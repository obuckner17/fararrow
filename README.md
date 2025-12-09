# fararrow
Fararrow Platform

**Architecture Overview**

The system is split into three main components, all sharing a single Rust library (processor_lib):

    1. Core Logic (Library): The central, stable Rust engine responsible for data validation and filtering.

    2. Backend API (Serverless): An Axum service exposed as a HATEOAS API. It handles authentication, data persistence, and is ready for deployment via AWS Lambda (lambda-web).

    3. Wasm Frontend: A Yew application compiled to WebAssembly (Wasm). It runs directly in the browser, providing a zero-latency interface for real-time visualization and filtering of data.

 **Key Features**

    Rust Safety: Guaranteed memory and thread safety across the entire stack.

    Zero-Latency Filtering: Core processing logic runs instantly in the browser (Wasm).

    Scalable Backend: Designed for Function-as-a-Service (FaaS) deployment (AWS Lambda/Azure Functions).

    Contributor-Ready: Clear separation of concerns and robust test structure.

**Local Quick Start Guide**

To get the full hybrid system running locally, you must run the server and the frontend simultaneously in two separate terminal windows.

Prerequisites

   A. Rust toolchain installed (rustup).

   B. Wasm target installed: rustup target add wasm32-unknown-unknown

   C. Trunk installed: cargo install trunk

1. Run the Backend API (Terminal 1)

This starts the Axum server, ready to receive metric data and API requests.
Bash

# This command runs the binary defined in src/bin/server.rs
cargo run --bin server

(The server will start listening on http://127.0.0.1:3000)

2. Run the Wasm Frontend (Terminal 2)

This compiles the Yew code to Wasm and launches the local development server.
Bash

# This command builds the Wasm binary and serves the HTML
trunk serve --open

(Your browser will open to http://127.0.0.1:8080)

3. Test the Functionality

You can verify the backend's data processing and HATEOAS compliance by querying it directly while the server is running.
Bash

# Test the filtering endpoint with a population threshold of 9 million
curl -X POST http://127.0.0.1:3000/filter \
-H 'Content-Type: application/json' \
-d '{"min_population": 9000000}'

⚖️ License

This project is licensed under the MIT License.
