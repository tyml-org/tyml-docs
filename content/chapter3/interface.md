+++
title = "Core Definitions"
weight = 2
+++

## interface

Use the `interface` keyword to define REST API shapes.

```tyml
interface API {

}
```

Multiple definitions are also supported.

```tyml
interface API1 {}

interface API2 {}
```

Each definition is transpiled to the target language’s equivalent of an interface during code generation.

## function
Inside an interface, define methods with the `function` keyword.

You can specify argument and return types. Arguments map to query parameters.
```tyml
interface API {
    /// A method named "hello"
    /// Returns a string
    function hello() -> string

    /// You can also take arguments
    /// Use ',' to specify multiple parameters
    function arguments(id: int, name: string)
}
```

## @body
Use the `@body` keyword to specify the HTTP request body type.
```tyml
type BodyType {
    id: int
    name: string
}

interface API {
    function body_test(@body: BodyType)
}
```
