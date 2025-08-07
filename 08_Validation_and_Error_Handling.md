# Chapter 8: Validation and Error Handling

HCL allows you to define **custom validation rules** and use **built-in safety functions** to handle errors gracefully during evaluation.

## 1. Conditional Validation

Available in tools built on HCL2 (like Terraform), conditional validation ensures that variable values meet specific criteria before execution proceeds.

### Syntax:

```hcl
variable "port" {
  type = number
  validation {
    condition     = var.port >= 1024 && var.port <= 65535
    error_message = "Port must be between 1024 and 65535"
  }
}
```

### Supported in:

- `variable` blocks
- `module` input variables
- `locals` (via logic)

### Examples:

#### Length check for a string

```hcl
variable "project_name" {
  type = string
  validation {
    condition     = length(var.project_name) >= 3
    error_message = "Project name must be at least 3 characters"
  }
}
```

#### Validate list contents

```hcl
variable "tags" {
  type = list(string)
  validation {
    condition     = alltrue([for tag in var.tags : length(tag) <= 20])
    error_message = "Each tag must be 20 characters or less"
  }
}
```

## 2. Custom Error Messages for Incorrect Input

When a `validation` condition fails, the custom `error_message` is shown to the user.

### Example:

```hcl
variable "environment" {
  type = string
  validation {
    condition     = contains(["dev", "stage", "prod"], var.environment)
    error_message = "Environment must be one of: dev, stage, prod"
  }
}
```

This enhances clarity and reduces debugging time for users of your configuration.

## 3. Fallback and Exception-Safe Logic

Use HCL functions like `try()` and `can()` to handle nulls, errors, or missing attributes **without crashing** the configuration.

### a) `try(expr1, expr2, ...)`

Returns the first expression that succeeds without error.

```hcl
description = try(var.project_description, "No description provided")
```

If `var.project_description` is unset or null, the fallback is used.

### b) `can(expr)`

Returns `true` if the expression is valid and safe to evaluate.

```hcl
is_set = can(var.optional_value)
```

Use it to avoid runtime errors when accessing optional or dynamic fields.

### Combined Example:

```hcl
output "project_tag" {
  value = try(var.tags["project"], "default-tag")
}
```

If the `tags["project"]` key doesn't exist, `"default-tag"` is used safely.
