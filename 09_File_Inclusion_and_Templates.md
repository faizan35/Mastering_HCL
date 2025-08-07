# Chapter 9: File Inclusion and Templates

HCL supports reading and embedding external content such as plain text, templates, JSON, and YAML into your configuration dynamically.

## 1. Reading External Files using `file()`

### Syntax:

```hcl
file("path/to/file.txt")
```

This reads the contents of the file as a raw string.

### Example:

```hcl
data "template_file" "example" {
  template = file("${path.module}/scripts/setup.sh")
}
```

Used for:

- Including shell scripts
- Injecting static content (e.g., licenses, notices)
- Referencing local documentation or text blobs

## 2. Using `templatefile()` for Dynamic Configuration

This function reads a file and performs variable interpolation using a provided map.

### Syntax:

```hcl
templatefile("template_path", { key1 = val1, key2 = val2 })
```

### Template Example (`script.tpl`):

```bash
#!/bin/bash
echo "Environment: ${env}"
echo "Version: ${version}"
```

### HCL Usage:

```hcl
locals {
  rendered = templatefile("${path.module}/script.tpl", {
    env     = var.environment
    version = "1.2.3"
  })
}
```

The `${env}` and `${version}` placeholders are replaced with values from the map.

## 3. Embedding Configuration Templates

You can use templates to:

- Inject configurations into cloud-init, systemd, Nginx, etc.
- Configure complex software (e.g., Nomad jobs, Consul agents)

### Example (embedded Nginx config):

```hcl
resource "local_file" "nginx" {
  content  = templatefile("${path.module}/nginx.tpl", {
    port = 8080
  })
  filename = "${path.module}/nginx.conf"
}
```

**Template (`nginx.tpl`):**

```nginx
server {
  listen ${port};
  location / {
    proxy_pass http://localhost:${port};
  }
}
```

## 4. Working with `filebase64()`, `jsondecode()`, and `yamldecode()`

### a) `filebase64(path)`

Reads a file and encodes it as Base64 — often used for binary content.

```hcl
encoded_cert = filebase64("${path.module}/cert.pem")
```

### b) `jsondecode(string)`

Parses a JSON-formatted string into HCL data structures (map/list).

```hcl
locals {
  raw_json = file("${path.module}/config.json")
  config   = jsondecode(local.raw_json)
}
```

### c) `yamldecode(string)`

Same as `jsondecode`, but for YAML content.

```hcl
locals {
  yaml_data = yamldecode(file("${path.module}/values.yaml"))
}
```

**Returns:** a native HCL map or list based on the file content.
