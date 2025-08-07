# Chapter 7: Complex Type Systems and Type Constraints

## 1. Overview of Type Systems

HCL uses a **strong, statically-typed system** (especially in HCL2) to validate data structures. Every value in HCL has a **type**, and the language enforces **type compatibility** when assigning or passing values.

### Primary Type Categories:

- **Primitive**: `string`, `number`, `bool`
- **Structural**: `list(type)`, `set(type)`, `map(type)`
- **Compound**: `tuple([types...])`, `object({key = type, ...})`
- **Dynamic**: `any`, `null`

## 2. Strict Typing with Structured Types

### a) Object Types with Nested Fields

Objects can have nested structures, each field explicitly typed:

```hcl
variable "user" {
  type = object({
    name    = string
    age     = number
    address = object({
      city     = string
      zipcode  = string
    })
  })
}
```

This ensures each field is:

- Required
- Of the correct type
- Structured for clarity and validation

**Access example:**

```hcl
local_city = var.user.address.city
```

### b) Tuple Types with Defined Structure

Tuples enforce:

- A fixed number of items
- Types based on **position**, not labels

```hcl
variable "coordinates" {
  type = tuple([number, number])
}
```

**Usage:**

```hcl
x = var.coordinates[0]
y = var.coordinates[1]
```

This is useful for enforcing position-based arguments like `(latitude, longitude)`.

## 3. Type Constraint Definitions

You can enforce strict types on any variable, local, or module input.

### Examples:

**List of strings**

```hcl
variable "tags" {
  type = list(string)
}
```

**Map of bool**

```hcl
variable "access" {
  type = map(bool)
}
```

**Optional with default:**

```hcl
variable "optional_flag" {
  type    = bool
  default = false
}
```

**Object with optional fields using `optional()` (tool-dependent)**

```hcl
variable "user" {
  type = object({
    name    = string
    enabled = optional(bool, true)
  })
}
```

## 4. Schema and Validation Logic

HCL2 supports **custom validation rules** (in tools like Terraform), allowing constraints beyond type checking.

### Example:

```hcl
variable "port" {
  type = number
  validation {
    condition     = var.port >= 1024 && var.port <= 65535
    error_message = "Port must be between 1024 and 65535"
  }
}
```

### Another Example – String pattern:

```hcl
variable "username" {
  type = string
  validation {
    condition     = length(var.username) >= 3
    error_message = "Username must be at least 3 characters"
  }
}
```

This ensures that the user input is valid at runtime.
