+++
title = "Refinement Types"
weight = 5
+++

## Refinement Types
TYML lets you add additional constraints to types.
```tyml
port: int @value 100..<200
```

## `@value` Attribute
Available for numeric types: `int`, `uint`, or `float`.
```tyml
setting: int @value 0..<100
```
You can specify ranges like `0..<100`. The forms are:

- `start..<end`: start inclusive, end exclusive
- `start..=end`: start inclusive, end inclusive
- `start..`: start inclusive, no upper bound
- `..<end`: end exclusive, no lower bound
- `..=end`: end inclusive, no lower bound

## `@length` Attribute
Restrict the number of Unicode characters of a `string`.
```tyml
setting: string @length 0..<100
```
Range notation is the same as for `@value`.

## `@u8size` Attribute
Restrict the UTF‑8 byte length of a `string`.
```tyml
setting: string @u8size 0..<100
```
Range notation is the same as for `@value`.

## `@regex` Attribute
Restrict a `string` by a regular expression.
```tyml
// Single quotes avoid escaping
setting: string @regex '^\\d+$'
```

## Multiple Conditions
Use `and` and `or` to combine constraints.
```tyml
// "and" has higher precedence.
// Use () to adjust precedence.
setting: string (@length 0..<10 or @length 100..<200) and @regex '^\\d+$'
```
