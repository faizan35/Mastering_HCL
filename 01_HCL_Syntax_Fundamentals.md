# Chapter 1: HCL Syntax Fundamentals

## 1. File Structure and Extensions (`.hcl`)

- HCL files typically use the `.hcl` extension (e.g., `main.hcl`, `config.hcl`).
- For tools like Terraform, `.tf` is used (but still HCL under the hood).
- Multiple HCL files can be used in the same directory — they’re **merged at parse time** by the tool reading them (e.g., Terraform).

## 2. Comments

HCL supports three types of comments:

```hcl
# Hash-style comment (most common)
# This is a comment

// C++-style comment
// Also valid in HCL

/* Block-style comment */
resource "example" "demo" {
  /* This is a block comment
     spanning multiple lines */
  name = "value"
}
```

## 3. Blocks

Blocks are the **fundamental unit of structure** in HCL. They look like this:

```hcl
block_type "label1" "label2" {
  attribute_name = "value"
}
```

### Structure

- `block_type`: Identifies what kind of block this is (e.g., `resource`, `provider`, `variable`)
- `label1`, `label2`: Optional identifiers used for grouping or naming
- `{ ... }`: Body of the block, containing **attributes** or nested blocks

### Example:

```hcl
server "web" {
  ip   = "192.168.1.1"
  port = 8080
}
```

## 4. Nested Blocks

You can place blocks inside other blocks for hierarchical structure.

```hcl
application "webapp" {
  server {
    ip   = "192.168.1.1"
    port = 8080
  }

  database {
    engine = "postgres"
    version = "14"
  }
}
```

## 5. Attributes

Attributes are **key-value pairs** inside a block.

```hcl
resource "bucket" "example" {
  name     = "my-bucket"
  location = "us-east-1"
  public   = true
}
```

### Notes:

- The order of attributes **does not matter**
- Attributes can be strings, numbers, booleans, lists, maps, or expressions

## 6. Whitespace and Formatting Rules

- **Whitespace is not significant**, but indentation improves readability.
- HCL encourages indentation with **2 or 4 spaces** per level (spaces only; no tabs).
- Braces `{` should be on the same line as the block definition.
- Use `hclfmt` or `terraform fmt` to auto-format HCL code.

### Good Practice:

```hcl
service "cache" {
  port     = 6379
  enabled  = true
}
```

### Avoid:

```hcl
service
"cache"
{
port=6379
enabled=true
}
```
