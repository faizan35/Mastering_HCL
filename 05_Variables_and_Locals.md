# Chapter 5: Variables and Locals

Variables and locals are used to **parametrize and modularize** HCL configurations. They help avoid duplication, enable reuse, and support flexible configuration patterns.

## 1. Input Variables

### a) Declaring Variables

Input variables are typically declared in a dedicated file (e.g., `variables.hcl`, `variables.tf`).

**Syntax:**

```hcl
variable "region" {
  type    = string
  default = "us-east-1"
}
```

You can optionally include:

- `description`
- `validation` rules
- `sensitive = true`

### b) Referencing Variables

Use `var.<name>` to access the value:

```hcl
provider "aws" {
  region = var.region
}
```

You can reference them in any expression.

### c) Variable Types

You can declare the type explicitly:

```hcl
variable "names" {
  type = list(string)
}

variable "settings" {
  type = object({
    enabled = bool
    count   = number
  })
}
```

If not specified, the type is inferred from the default or input.

### d) Default Values

If a variable has a `default`, it becomes optional. Otherwise, the system will prompt for a value or raise an error.

```hcl
variable "environment" {
  default = "dev"
}
```

## 2. Locals

**`locals`** allow you to define reusable expressions or intermediate computed values within your config.

### Syntax:

```hcl
locals {
  project_name = "crm"
  full_name    = "${local.project_name}-${var.environment}"
}
```

- Refer to local values using `local.<name>`
- Common for formatting, computation, or aliasing deeply nested values

### Example:

```hcl
locals {
  service_port = var.base_port + 100
  tags = {
    owner = "faizan"
    app   = "web"
  }
}
```

You can use them like:

```hcl
resource "aws_instance" "web" {
  tags = local.tags
}
```

## 3. Overriding Values (Conceptual)

Although this behavior depends on the tool (e.g., Terraform), the concept is:

- **Default values** are used when no input is provided
- **Explicit inputs** override defaults
- **Variable files**, **command-line arguments**, or **environment variables** can be used to provide overrides

**Conceptual example:**

```hcl
variable "replicas" {
  type    = number
  default = 1
}
```

If you pass `replicas = 3` from a file or input method, it overrides the default.
