+++
title = "Default Values"
weight = 3
+++

## Defaults
You can set default values on method parameters and return values.
```tyml
type Type {
    id: int
    name: string
}

interface API {
    function test(id: int = 100, name: string = "test") -> Type {
        return { id = 100, name = "test" }
    }
}
```
This feature is used by the [`TYML for VSCode`](https://marketplace.visualstudio.com/items?itemName=bea4dev.tyml-lsp-vscode) extension.

When opened in VSCode with the extension installed, you should see `▶ Run server` and `▶ Run client` like this:

![tyml_vscode_run](https://tyml-org.github.io/tyml-docs-jp/chapter3/tyml_vscode_run.png)

Clicking these lets you run a mock server or client so you can quickly test your application with one click.

## Notation
Defaults correspond to the actual JSON values used at runtime, but the syntax is slightly different from JSON.

### Primitives
Primitive values are the same as JSON:
```json
// int
100
// float
100.0
// string
"text"
// bool
true
false
// null
null
```

### Objects
Objects differ slightly from JSON.
Name literals do not need quotes, and `:` becomes `=`.
```tyml
{ id = 100, name = "text" }
```

### Arrays
Arrays are the same as JSON.
```json
[0, 100, null]
```
