# HashiCorp Configuration Language (HCL) Learning Syllabus

## Chapter 0: Introduction to HCL

- What is HCL?
- HCL vs JSON/YAML
- Where is HCL used? (Overview: Terraform, Nomad, Consul, Vault, Packer)
- HCL Versions: HCL1 vs HCL2
- Installing and using HCL CLI (`hclfmt`, `hcl2json`, etc.)

## Chapter 1: HCL Syntax Fundamentals

- File structure and extensions (`.hcl`)
- Comments (`#`, `//`, `/* */`)
- Blocks

  - Structure: `block_type "label1" "label2" { ... }`
  - Nested blocks

- Attributes

  - Key-value pairs
  - Attribute ordering and formatting

- Whitespace and formatting rules

## Chapter 2: Data Types

- Primitive types

  - String
  - Number
  - Boolean

- Complex types

  - List
  - Tuple
  - Map
  - Object

- Null values and nullability
- Type conversion functions

## Chapter 3: Expressions

- Expression syntax: `${ ... }` and direct use
- Operators

  - Arithmetic: `+`, `-`, `*`, `/`, `%`
  - Comparison: `==`, `!=`, `<`, `>`, `<=`, `>=`
  - Logical: `&&`, `||`, `!`

- String interpolation and concatenation
- Conditional expressions: `condition ? true_val : false_val`

## Chapter 4: Loops and Dynamic Constructs

- `for` expressions

  - List comprehensions: `[for item in list : item.attr]`
  - Map comprehensions

- Filtering using `if` in comprehensions
- Dynamic blocks (explained as an HCL pattern)

## Chapter 5: Variables and Locals

- Input variables

  - Declaring and referencing variables
  - Variable types and default values

- Locals

  - Defining intermediate expressions
  - Scoping and reuse

- Overriding values (conceptual, not tool-specific)

## Chapter 6: Functions

- String functions

  - `length`, `substr`, `replace`, `split`, `join`, `trim`, `lower`, `upper`

- Numeric functions

  - `abs`, `ceil`, `floor`, `max`, `min`

- Collection functions

  - `contains`, `distinct`, `flatten`, `merge`, `keys`, `values`, `zipmap`, `slice`

- Type functions

  - `tostring`, `tonumber`, `can`, `try`

- Function composition and nesting

## Chapter 7: Complex Type Systems and Type Constraints

- Overview of type systems
- Strict typing with:

  - Object types with nested fields
  - Tuple types with defined structure

- Type constraint definitions
- Schema and validation logic

## Chapter 8: Validation and Error Handling

- Conditional validation
- Custom error messages for incorrect input
- Fallback and exception-safe logic using `try()` and `can()`

## Chapter 9: File Inclusion and Templates

- Reading external files using `file()`
- Using `templatefile()` for dynamic configuration
- Embedding configuration templates
- Working with `filebase64()`, `jsondecode()`, and `yamldecode()`

## Chapter 10: Tooling for HCL

- Using `hclfmt` for formatting
- Using `hcl2json` for conversion
- Static analysis and schema validation tools
- Editor support and syntax highlighting
- Integrating HCL into CI/CD workflows

## Chapter 11: HCL for Tool Builders

- Parsing HCL with Go (`go-hcl`, `hclparse`, `hclsyntax`)
- Tokenization and decoding into Go structs
- Validation with Go-based HCL schema
- Creating custom configuration formats using HCL
- Building a CLI that reads and validates HCL input
