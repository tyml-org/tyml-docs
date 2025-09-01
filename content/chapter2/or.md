+++
title = "Union Type"
weight = 2
+++

## Union Type (or)
TYML lets you accept one of multiple types when needed.
```tyml
/// Accept either an int or a string
setting: int | string
```

- In TOML
```toml
# !tyml example.tyml
setting = 100
```
```toml
# !tyml example.tyml
setting = "string"
```
Both are valid.
