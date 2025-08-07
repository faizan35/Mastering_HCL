# Chapter 4: Loops and Dynamic Constructs

HCL supports loop-like behavior via **`for` expressions** and **dynamic blocks**. These constructs help generate collections or configuration structures programmatically.

## 1. `for` Expressions

A `for` expression creates a new list or map by transforming or filtering existing collections.

### Syntax (List Comprehension):

```hcl
[for item in list : transformed_item]
```

### a) List Comprehensions

Transform a list of strings into uppercase:

```hcl
locals {
  names        = ["faizan", "john", "alice"]
  upper_names  = [for n in local.names : upper(n)]
}
```

**Result**:

```hcl
["FAIZAN", "JOHN", "ALICE"]
```

You can also apply transformations:

```hcl
[for i in [1, 2, 3] : i * 2]  # => [2, 4, 6]
```

### b) Map Comprehensions

Transform a map into a new map:

```hcl
locals {
  original = {
    a = 1
    b = 2
    c = 3
  }

  doubled = {
    for k, v in local.original :
    k => v * 2
  }
}
```

**Result**:

```hcl
{
  a = 2
  b = 4
  c = 6
}
```

## 2. Filtering Using `if` in Comprehensions

You can add a filter clause using `if` inside `for` expressions.

### Example (filter even numbers):

```hcl
[for n in [1, 2, 3, 4, 5] : n if n % 2 == 0]
```

**Result**:

```hcl
[2, 4]
```

### Example (filter and transform):

```hcl
[for name in ["faizan", "admin", "guest"] : upper(name) if name != "guest"]
```

**Result**:

```hcl
["FAIZAN", "ADMIN"]
```

## 3. Dynamic Blocks (HCL Pattern)

Dynamic blocks allow you to **generate nested blocks** based on complex data structures.

This is not part of raw HCL language spec but is a common **pattern** in tools like Terraform.

### Example:

```hcl
variable "tags" {
  default = {
    Name   = "web-server"
    Owner  = "faizan"
  }
}

resource "example" "server" {
  dynamic "tag" {
    for_each = var.tags
    content {
      key   = tag.key
      value = tag.value
    }
  }
}
```

### Explanation:

- `dynamic "tag"`: dynamically generates `tag { key = ..., value = ... }` blocks
- `for_each = var.tags`: iterates over the map
- `content { ... }`: defines the body of the generated block

Use dynamic blocks when:

- You need to generate child blocks conditionally or repeatedly
- Static declaration is too verbose or not possible
