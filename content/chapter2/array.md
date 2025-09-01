+++
title = "Arrays"
weight = 3
+++

## Array Type
TYML supports array types.
```tyml
/// An array of strings
settings: [string]
```

Arrays of union types are also allowed.
```tyml
settings: [string | int]
```

- In TOML
```toml
# !tyml example.tyml
settings = ["string1", "string2", 100]
```
