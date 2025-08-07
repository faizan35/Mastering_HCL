# Chapter 10: Tooling for HCL

Tooling support is critical for maintaining consistent, error-free HCL code — whether for infrastructure (like Terraform) or custom DSLs.

## 1. Using `hclfmt` for Formatting

`hclfmt` is a Go-based formatter for HCL, similar to `gofmt` for Go or `terraform fmt` in Terraform.

### Install via Go:

```bash
go install github.com/hashicorp/hcl/cmd/hclfmt@latest
```

### Usage:

```bash
hclfmt ./file.hcl
```

### Purpose:

- Enforces consistent indentation, spacing, and line breaks
- Makes diffs cleaner in version control
- Prevents manual formatting errors

## 2. Using `hcl2json` for Conversion

Converts HCL input into equivalent JSON output.

### Install:

```bash
go install github.com/tmccombs/hcl2json@latest
```

### Usage:

```bash
hcl2json < config.hcl > config.json
```

### Use cases:

- Interoperability with JSON-based tools
- Debugging and programmatic processing
- Generating schema-aware machine-readable configs

## 3. Static Analysis and Schema Validation Tools

While native HCL tooling is minimal, tools like Terraform provide schema validation using `terraform validate`.

If you're building your own HCL-based DSL in Go, use:

### HashiCorp HCL Go SDK:

- Modules: `hclparse`, `hclsyntax`, `hcldec`
- Supports:

  - AST parsing
  - Syntax and type checking
  - Custom schema enforcement

### Tools (example for Terraform-based HCL):

- `tflint`: Linting for Terraform HCL
- `checkov`, `tfsec`: Security & compliance scanning
- `conftest`: Policy validation via OPA (can be extended to HCL via JSON)

## 4. Editor Support and Syntax Highlighting

HCL is supported by most major editors:

### Visual Studio Code

- Extension: **HashiCorp Terraform**
- Syntax highlighting
- Snippet completion
- Validation & formatting via `terraform-ls`

### Vim / Neovim

- Plugin: `hashivim/vim-terraform`
- Auto-formatting and syntax support

### JetBrains IDEs

- Terraform plugin (for `.hcl`/`.tf`)
- Full validation, formatting, and introspection

## 5. Integrating HCL into CI/CD Workflows

In infrastructure pipelines or custom CI:

### a) Validate Formatting:

```bash
hclfmt -check ./config.hcl
```

Or with Terraform:

```bash
terraform fmt -check -recursive
```

### b) Syntax Validation:

If using Go SDK:

```go
parser := hclparse.NewParser()
file, diag := parser.ParseHCLFile("config.hcl")
```

Or use `terraform validate` for Terraform-specific files.

### c) Git Pre-Commit Hooks:

```yaml
- repo: https://github.com/antonbabenko/pre-commit-terraform
  hooks:
    - id: terraform_fmt
    - id: terraform_validate
```

### d) GitHub Actions:

Example:

```yaml
- name: Format HCL
  run: terraform fmt -check -recursive
```
