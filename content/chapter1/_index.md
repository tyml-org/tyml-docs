+++
title = "Introduction"
weight = 1
sort_by = "weight"
insert_anchor_links = "right"
+++

## What Is [TYML](https://tyml-org.github.io/tyml-lang.org/)
TYML is a schema language that provides type checking and editor assistance for arbitrary configuration languages.
It currently supports the following configuration languages:
- `ini`
- `toml`
- `json`

## Quick Tour
TYML is designed to be more intuitive yet more precise than competing specifications such as `JsonSchema`.

It can also define REST API schemas similar to `OpenAPI`.

Here is a quick look at the syntax TYML uses.

```tyml
// "setting" is the setting name and "int" is its type
setting: int

/// Triple slashes "///" are treated as documentation comments
/// (They are recognized by the LSP and can be shown while editing.)
///
/// "[Setting]" means an array of type "Setting"
settings: [Setting]

/// You can define a struct type "Setting"
type Setting {
    ip: string
    port: int
    mode: Mode
}

/// Defining an enum restricts values to the specified strings
enum Mode {
    "Debug"
    "Release"
}

/// Appending "?" to a type makes the value optional
/// This is the so‑called nullable/optional type
nullable: int?

/// Using "|" creates a union type: a value of either side is accepted
or_type: int | string


/// You can also define REST APIs!
/// Code can of course be generated with the type generator (tyml-api-generator).
/// The docs you write here are propagated into the generated output.
interface API {
    function register(id: int = 100, name: string = "test") -> string {
        return "* Secret Token *"
    }

    authed function get_user(@claim: Claim) -> User {
        return { id = 100, name = "test" }
    }

    #[kind = "get"]
    function hello() -> string {
        return "Hello, world!"
    }
}
```

You can enable type checking and editor help in your config file by referencing the schema like this:
```toml
# !tyml example.tyml
# Specify the schema file by adding "!tyml" in a comment
setting = 100

[[settings]]
ip = "192.168.1.1"
port = 25565
mode = "Debug"

or_type = 200
```
