+++
title = "Code Generation"
weight = 4
+++

## Installation
Install TYML CLI tools with:
```bash
cargo install tyml_core tyml_api_generator tyml_mock
```
(Requires Rust’s cargo.)

This section describes the API generator.

## Command
```bash
tyml-api-gen --help
```
Running this prints something like:

```
TYML: type checker for markup language

Usage: tyml-api-gen <COMMAND>

Commands:
  server
  client
  help    Print this message or the help of the given subcommand(s)

Options:
  -h, --help     Print help
  -V, --version  Print version
```
As shown, `tyml-api-gen` has two subcommands.

### Server
```bash
tyml-api-gen server <KIND> <TYML> <DIR> [NAME]
```
The server command has three required arguments and one optional argument.
Valid values are:

```
 - KIND: Kind of server to generate
    Allowed: rust-axum

 - TYML: The TYML file to use for generation

 - DIR: Destination directory (becomes a package/crate directory)

 - NAME: Package/crate name, default is "api"
```

- Example
```bash
tyml-api-gen server rust-axum api.tyml ./api-example-server/api
```

### Client
```bash
tyml-api-gen client <KIND> <TYML> <DIR> [NAME]
```
The client command has three required arguments and one optional argument.
Valid values are:

```
 - KIND: Kind of client to generate
    Allowed: typescript, rust

 - TYML: The TYML file to use for generation

 - DIR: Destination directory (becomes a package/crate directory)

 - NAME: Package/crate name, default is "api"
```

- Example
```bash
tyml-api-gen client typescript api.tyml ./api-example-client/api
```
