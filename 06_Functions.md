# Chapter 6: Functions in HCL

HCL provides a wide range of built-in functions for working with strings, numbers, collections, and types. These functions can be **composed and nested** within expressions.

## 1. String Functions

### `length(string)`

Returns the number of characters.

```hcl
length("hello")  # => 5
```

### `substr(string, offset, length)`

Extracts a substring.

```hcl
substr("terraform", 0, 4)  # => "terr"
```

### `replace(string, substring, replacement)`

Replaces substring with another string.

```hcl
replace("abcabc", "a", "x")  # => "xbcxbc"
```

### `split(delim, string)`

Splits string into a list.

```hcl
split(",", "a,b,c")  # => ["a", "b", "c"]
```

### `join(delim, list)`

Joins list elements into a string.

```hcl
join("-", ["a", "b", "c"])  # => "a-b-c"
```

### `trimspace(string)`

Removes leading/trailing whitespace.

```hcl
trimspace(" hello ")  # => "hello"
```

### `lower(string)` / `upper(string)`

Converts case.

```hcl
lower("FOO")  # => "foo"
upper("bar")  # => "BAR"
```

## 2. Numeric Functions

### `abs(number)`

Absolute value.

```hcl
abs(-3)  # => 3
```

### `ceil(number)`

Rounds up.

```hcl
ceil(3.1)  # => 4
```

### `floor(number)`

Rounds down.

```hcl
floor(3.9)  # => 3
```

### `max(a, b, ...)` / `min(a, b, ...)`

Returns the largest or smallest.

```hcl
max(1, 3, 2)  # => 3
min(4, 7, 2)  # => 2
```

## 3. Collection Functions

### `contains(list, value)`

Returns `true` if value is in list.

```hcl
contains(["a", "b", "c"], "b")  # => true
```

### `distinct(list)`

Removes duplicates.

```hcl
distinct(["a", "b", "a"])  # => ["a", "b"]
```

### `flatten(list of lists)`

Flattens nested lists.

```hcl
flatten([["a"], ["b", "c"]])  # => ["a", "b", "c"]
```

### `merge(map1, map2, ...)`

Merges multiple maps.

```hcl
merge({a = 1}, {b = 2})  # => {a = 1, b = 2}
```

### `keys(map)` / `values(map)`

Extracts keys or values.

```hcl
keys({a = 1, b = 2})    # => ["a", "b"]
values({a = 1, b = 2})  # => [1, 2]
```

### `zipmap(keys, values)`

Creates a map from keys and values.

```hcl
zipmap(["a", "b"], [1, 2])  # => {a = 1, b = 2}
```

### `slice(list, start, end)`

Returns a sublist (end-exclusive).

```hcl
slice([1, 2, 3, 4], 1, 3)  # => [2, 3]
```

## 4. Type Functions

### `tostring(value)`

Converts number, bool, or list to string.

```hcl
tostring(123)  # => "123"
```

### `tonumber(string)`

Converts string to number.

```hcl
tonumber("42")  # => 42
```

### `can(expression)`

Returns true if expression can be evaluated without error.

```hcl
can(local.foo.bar)  # => false (if `foo` is null)
```

### `try(expr1, expr2, ...)`

Returns the first non-error result.

```hcl
try(var.optional, "default")  # => "default" if var.optional is null
```

## 5. Function Composition and Nesting

You can nest functions to build more advanced expressions.

```hcl
join("-", distinct([for name in var.names : lower(trimspace(name))]))
```

Breakdown:

- `trimspace` removes spaces
- `lower` normalizes case
- `distinct` removes duplicates
- `join` concatenates into a string

Another example:

```hcl
length(split("-", var.id)) > 2 ? "valid" : "invalid"
```
