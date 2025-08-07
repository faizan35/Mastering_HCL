# Chapter 2: Data Types

HCL supports a flexible type system composed of **primitive** and **complex** types. These types are used in variables, attributes, and function arguments across all HCL-based configurations.

## 1. Primitive Types

### a) String

A sequence of characters enclosed in double quotes (`"`):

```hcl
name = "faizan"
```

You can also interpolate expressions in strings using `${}`:

```hcl
message = "Hello, ${var.user_name}"
```

### b) Number

Numbers can be integers or floating-point:

```hcl
port = 8080
threshold = 3.14
```

All numbers are stored internally as floating-point.

### c) Boolean

Boolean values are `true` or `false`:

```hcl
enabled = true
force_delete = false
```

## 2. Complex Types

### a) List

An **ordered sequence** of values of the **same type**.

```hcl
fruits = ["apple", "banana", "cherry"]
ports  = [80, 443, 8080]
```

All elements must be of the same type. Use `tuple` for mixed types.

### b) Tuple

An **ordered sequence** of values of **different types**:

```hcl
mixed_data = ["faizan", 29, true]
```

This is rare but useful when the data is positionally fixed and types vary.

### c) Map

A **key-value pair** structure where keys are strings and values must be of the same type:

```hcl
user_roles = {
  "admin"  = true
  "editor" = false
  "guest"  = false
}
```

You can access values like: `user_roles["admin"]`

### d) Object

Like a `map`, but with **predefined keys and types**, allowing structural validation.

```hcl
user = {
  name  = "faizan"
  age   = 28
  admin = true
}
```

Used when you want **type-safe and predictable structures**.

## 3. Null Values and Nullability

`null` can be used when a value is unset, optional, or unknown:

```hcl
description = null
```

- Useful in **dynamic logic**, conditionals, and function defaults.
- HCL functions like `can()` and `try()` help deal with nulls safely.

Example:

```hcl
display = try(var.description, "Not provided")
```

## 4. Type Conversion Functions

These are **HCL built-in functions** that allow you to convert between types:

| Function     | Description                                          |
| ------------ | ---------------------------------------------------- |
| `tostring()` | Converts number, boolean, or null to string          |
| `tonumber()` | Converts string to number (if valid)                 |
| `tolist()`   | Converts a tuple to a list                           |
| `tomap()`    | Converts a JSON object to HCL map                    |
| `can()`      | Returns `true` if a conversion or access is possible |
| `try()`      | Returns the first successful expression              |

### Examples:

```hcl
str = tostring(100)        # "100"
num = tonumber("3.14")     # 3.14
ok  = can(var.maybe_null)  # true or false
out = try(var.foo, "N/A")  # fallback if var.foo is null or error
```
