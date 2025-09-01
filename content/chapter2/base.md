+++
title = "Basics"
weight = 1
+++

## Setting Names and Types
In general, you write `name: Type`.
```tyml
setting: int
```

## Primitive Types
TYML provides several primitive types:
- `int`    : 64‑bit signed integer
- `uint`   : 64‑bit unsigned integer
- `bool`   : Boolean, `true` or `false`
- `float`  : Floating‑point number
- `string` : String

## Struct Types
There are two ways to describe structures.

- Inline
```tyml
setting: {
    ip: string
    port: int
}
```

- Type definition
```tyml
type Setting {
    ip: string
    port: int
}

setting: Setting
```

There are also two ways to format fields inside a struct.

- Newline‑separated
```tyml
type Setting {
    ip: string
    port: int
}
```

- Comma‑separated
```tyml
type Setting { ip: string, port: int }
```

You can freely mix the two styles:
```tyml
type Setting {
    ip: string,
    port: int, // trailing commas are fine
}
```

As a rule of thumb, we recommend 4 spaces for indentation, but tabs are also syntactically valid.

### Allowing Arbitrary Elements
```tyml
// "setting" must be string; any other keys must be int
setting: string
// If you omit "*", arbitrary extra keys are not allowed
*: int
```
```toml
# !tyml example.tyml
setting = "string"
# Defining "*" allows arbitrary elements to be provided
user_element = 100
```

## enum Type
Declaring an enum can restrict string values:
```tyml
enum Mode {
    "Debug"
    "Release"
}

// "mode" only accepts "Debug" or "Release"
mode: Mode
```

You can separate enum items with commas or newlines, just like struct fields:
```tyml
enum Mode {
    "Debug",
    "Mode",
}
```
