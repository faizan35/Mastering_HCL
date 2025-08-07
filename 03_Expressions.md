# Chapter 3: Expressions

In HCL, expressions allow you to compute values using variables, literals, operators, and functions. Expressions are used within attributes, conditionals, loops, and interpolated strings.

## 1. Expression Syntax

Expressions in HCL can be written:

### a) Directly

```hcl
timeout = 30 * 2
enabled = var.enable_logging
```

### b) Inside Interpolation

```hcl
greeting = "Hello, ${var.username}"
```

Note: `${}` is optional in modern HCL2 if the expression is used alone.

## 2. Operators

### a) Arithmetic Operators

| Operator | Meaning        | Example  | Result |
| -------- | -------------- | -------- | ------ |
| `+`      | Addition       | `2 + 3`  | `5`    |
| `-`      | Subtraction    | `5 - 2`  | `3`    |
| `*`      | Multiplication | `4 * 2`  | `8`    |
| `/`      | Division       | `8 / 2`  | `4.0`  |
| `%`      | Modulo         | `10 % 3` | `1`    |

All numbers are floating-point internally.

### b) Comparison Operators

| Operator | Meaning          | Example  | Result |
| -------- | ---------------- | -------- | ------ |
| `==`     | Equal            | `5 == 5` | `true` |
| `!=`     | Not equal        | `4 != 2` | `true` |
| `<`      | Less than        | `3 < 5`  | `true` |
| `>`      | Greater than     | `7 > 1`  | `true` |
| `<=`     | Less or equal    | `5 <= 5` | `true` |
| `>=`     | Greater or equal | `6 >= 5` | `true` |

### c) Logical Operators

| Operator | Meaning | Example         | Result  |        |     |         |        |
| -------- | ------- | --------------- | ------- | ------ | --- | ------- | ------ |
| `&&`     | AND     | `true && false` | `false` |        |     |         |        |
| \`       |         | \`              | OR      | \`true |     | false\` | `true` |
| `!`      | NOT     | `!true`         | `false` |        |     |         |        |

Use parentheses to enforce evaluation order.

## 3. String Interpolation and Concatenation

### a) Interpolation

```hcl
user = "Faizan"
message = "Hello, ${user}"
```

You can also use expressions:

```hcl
port = 8080
msg  = "Service running on port ${port + 1}"
```

### b) Concatenation

Use the `join()` function or the `format()` function for complex cases:

```hcl
joiner = "user-" + var.username
```

Alternatively:

```hcl
full = "${var.prefix}-${var.name}"
```

## 4. Conditional Expressions

Use the **ternary operator** for inline conditions:

```hcl
env = var.is_prod ? "production" : "development"
```

Nested example:

```hcl
level = var.count > 5 ? (var.count > 10 ? "high" : "medium") : "low"
```

Avoid nesting deeply, as it affects readability.
