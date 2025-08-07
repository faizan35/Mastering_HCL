# Chapter 0: Introduction to HCL

## 1. What is HCL?

**HCL (HashiCorp Configuration Language)** is a domain-specific language (DSL) created by HashiCorp to write human-readable configurations.

### Key characteristics:

- Designed for **infrastructure configuration and orchestration**
- **Human-friendly syntax** (unlike JSON/XML)
- Supports both **declarative** and **expression-based** styles
- Can be parsed into **structured data** (JSON, Go structs)

### Example:

```hcl
resource "aws_instance" "example" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
  tags = {
    Name = "my-instance"
  }
}
```

## 2. HCL vs JSON/YAML

| Feature            | HCL                              | JSON                 | YAML                          |
| ------------------ | -------------------------------- | -------------------- | ----------------------------- |
| Readability        | High (designed for humans)       | Moderate             | High                          |
| Strictness         | Flexible (comments, expressions) | Strict (no comments) | Less strict (prone to errors) |
| Comments           | Supported                        | Not supported        | Supported                     |
| Expression Support | Yes (native logic, functions)    | No                   | Limited (via templating)      |
| Use Cases          | HashiCorp tools                  | APIs, configs        | Kubernetes, CI/CD tools       |

**Verdict:** HCL combines the human-friendliness of YAML with the structure and parsing ability of JSON.

## 3. Where is HCL Used?

HCL is embedded in several HashiCorp tools:

| Tool          | Usage of HCL                       |
| ------------- | ---------------------------------- |
| **Terraform** | Infrastructure as Code (IaC) files |
| **Vault**     | ACL policies, configuration        |
| **Consul**    | Intentions, service definitions    |
| **Nomad**     | Job specifications                 |
| **Packer**    | Image build templates              |

Although designed by HashiCorp, **you can use HCL in your own applications** using the Go HCL SDK.

## 4. HCL Versions: HCL1 vs HCL2

### HCL1 (Deprecated/Legacy)

- Used in early versions of Terraform (0.11 and below)
- Simple key-value format
- No for-loops, conditionals, or functions

### HCL2 (Modern, since Terraform 0.12+)

- Supports:

  - Rich expressions
  - Conditional logic
  - Functions
  - Complex types (list, object, tuple, map)
  - `for`, `if`, `dynamic` blocks

- **Strict typing and validation**
- Powers all current HashiCorp tools

**You should only focus on HCL2.**

## 5. Installing and Using HCL CLI Tools

There is no official standalone `hcl` CLI, but you can use:

### a) `hclfmt` (Formatter)

- Formats `.hcl` files
- Go-based
- Similar to `gofmt` or `terraform fmt`

**Install via Go:**

```bash
go install github.com/hashicorp/hcl/cmd/hclfmt@latest
```

**Usage:**

```bash
hclfmt ./myfile.hcl
```

### b) `hcl2json` (Convert HCL to JSON)

**Install:**

```bash
go install github.com/tmccombs/hcl2json@latest
```

**Usage:**

```bash
hcl2json < config.hcl > config.json
```

Useful for:

- Debugging
- Machine consumption
- Integration with non-HCL tools
