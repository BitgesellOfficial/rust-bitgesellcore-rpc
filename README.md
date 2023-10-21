[![Status](https://travis-ci.org/rust-bitcoin/rust-bitcoincore-rpc.png?branch=master)](https://travis-ci.org/rust-bitcoin/rust-bitcoincore-rpc)

# Rust RPC client for Bitcoin Core JSON-RPC 
<img src="doc/img/Icon.png" style="height: 60px;"/>

This is a Rust RPC client library for calling the Bitgesell Core JSON-RPC API. It provides a layer of abstraction over 
[rust-jsonrpc](https://github.com/apoelstra/rust-jsonrpc) and makes it easier to talk to the Bitgesell JSON-RPC interface 

This git package compiles into two crates.
1. [bitgesellcore-rpc](https://crates.io/crates/bitgesellcore-rpc) - contains an implementation of an rpc client that exposes 
the Bitgesell Core JSON-RPC APIs as rust functions.

2. [bitgesellcore-rpc-json](https://crates.io/crates/bitgesellcore-rpc-json) -  contains rust data structures that represent 
the json responses from the Bitcoin Core JSON-RPC APIs. bitcoincore-rpc depends on this.

# Usage
Given below is an example of how to connect to the Bitgesell Core JSON-RPC for a Bitgesell Core node running on `localhost`
and print out the hash of the latest block.

It assumes that the node has password authentication setup, the RPC interface is enabled at port `8332` and the node
is set up to accept RPC connections. 

```rust
extern crate bitgesellcore_rpc;

use bitgesellcore_rpc::{Auth, Client, RpcApi};

fn main() {

    let rpc = Client::new("http://localhost:8332",
                          Auth::UserPass("<FILL RPC USERNAME>".to_string(),
                                         "<FILL RPC PASSWORD>".to_string())).unwrap();
    let best_block_hash = rpc.get_best_block_hash().unwrap();
    println!("best block hash: {}", best_block_hash);
}
```

See `client/examples/` for more usage examples. 

# Supported Bitgesell Core Versions
The following versions are officially supported and automatically tested:
*  0.1.9
*  0.1.8
*  0.1.7
*  0.1.3

# Minimum Supported Rust Version (MSRV)
This library should always compile with any combination of features on **Rust 1.41.1**.
