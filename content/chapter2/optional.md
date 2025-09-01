+++
title = "Optional Type (?)"
weight = 4
+++

## Optional Type
You can indicate that a value is not required.

Just append `?` to the type.
```tyml
/// If provided, it must be an int; otherwise it can be omitted
setting: int?
```

## Where `?` Can Appear
While we say “append `?` to the type”, strictly speaking you can place `?` after a type name or after an array type.

```tyml
/// Either int? or [int]
/// Equivalent to writing int? | [int]?
setting: int? | [int]
```

- Inside arrays
```tyml
/// This is an array of int?
/// In JSON, values like [null, 100] are allowed.
/// In languages without null like TOML, only an empty array can represent absence.
setting: [int?]
```

- Not allowed
```tyml
/// This form is not allowed!
setting: int |?
```
