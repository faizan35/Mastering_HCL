# Chapter 11: HCL for Tool Builders

HashiCorp provides a powerful Go SDK that lets you embed HCL into your own tools. You can parse `.hcl` files, validate them against schemas, and convert them into native Go data structures.

## 1. Parsing HCL with Go (`go-hcl`, `hclparse`, `hclsyntax`)

### Required Modules:

```go
import (
  "github.com/hashicorp/hcl/v2"
  "github.com/hashicorp/hcl/v2/hclparse"
  "github.com/hashicorp/hcl/v2/hclsyntax"
)
```

### Basic HCL Parser:

```go
parser := hclparse.NewParser()

file, diags := parser.ParseHCLFile("config.hcl")
if diags.HasErrors() {
  log.Fatalf("Failed to parse HCL: %s", diags.Error())
}
```

`hclparse` handles parsing and syntax validation. The result is an `*hcl.File`.

## 2. Tokenization and Decoding into Go Structs

Use `hcldec` or `gohcl` to decode parsed HCL into strongly typed Go structs.

### Define a Go Struct:

```go
type Config struct {
  Name string `hcl:"name"`
  Port int    `hcl:"port"`
}
```

### Decode:

```go
var cfg Config
ctx := &hcl.EvalContext{}
diags := gohcl.DecodeBody(file.Body, ctx, &cfg)
if diags.HasErrors() {
  log.Fatalf("Decode error: %s", diags.Error())
}
```

## 3. Validation with Go-based HCL Schema

For advanced use cases, define **schemas manually** using `hcldec`.

### Example:

```go
spec := &hcldec.ObjectSpec{
  "enabled": &hcldec.BoolSpec{Required: true},
  "count":   &hcldec.NumberSpec{Required: false},
}
```

Then decode with:

```go
bodyContent, _, _ := file.Body.PartialContent(&hcl.BodySchema{})
result, diags := hcldec.Decode(bodyContent, spec, &hcl.EvalContext{})
```

This method is ideal for building low-level HCL DSLs where the schema is dynamic or versioned.

## 4. Creating Custom Configuration Formats using HCL

You can design your own configuration format using `.hcl` files and Go structs.

### Example: `.appconfig.hcl`

```hcl
name  = "my-app"
port  = 8080
debug = true
```

Go struct:

```go
type AppConfig struct {
  Name  string `hcl:"name"`
  Port  int    `hcl:"port"`
  Debug bool   `hcl:"debug"`
}
```

You can ship a CLI or service that reads this config and acts on it.

## 5. Building a CLI that Reads and Validates HCL Input

### Minimal CLI Example (with Cobra or plain `main.go`):

```go
func main() {
  parser := hclparse.NewParser()
  file, diags := parser.ParseHCLFile("config.hcl")
  if diags.HasErrors() {
    fmt.Fprintf(os.Stderr, "Parse error: %s\n", diags.Error())
    os.Exit(1)
  }

  var config AppConfig
  diags = gohcl.DecodeBody(file.Body, nil, &config)
  if diags.HasErrors() {
    fmt.Fprintf(os.Stderr, "Decode error: %s\n", diags.Error())
    os.Exit(1)
  }

  fmt.Printf("Running %s on port %d\n", config.Name, config.Port)
}
```

Build this into a binary with:

```bash
go build -o mycli main.go
./mycli
```
