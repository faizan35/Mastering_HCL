# Mastering HCL (HashiCorp Configuration Language)

# < --- In Progress --- >

## Module 1: Introduction to Infrastructure as Code (IaC) and HCL

### [1.1 Understanding Infrastructure as Code](./Module-01/1.1-Understaning-IaC.md)

- Definition and benefits of IaC
- Role of HCL in IaC workflows
- Overview of HashiCorp tools using HCL (Terraform, Packer, Consul)

### [1.2 HCL Syntax Fundamentals](./Module-01/1.2-HCL-Syntax.md)

#### [1.2.1 Blocks](./Module-01/1.2.1-Blocks.md)

#### [1.2.2 Variables and data types](./Module-01/1.2.2-Variables-data-types.md)

#### [1.2.3 Comments and documentation](./Module-01/1.2.3-Comments-documentation.md)

### [xx HCL in Action (Optional)](./Module-01/xx-HCL-Action.md)

## Module 2: Basic HCL Concepts

### [2.1 More on variables](./Module-02/2.1-More-variables.md)

- Default values and variable interpolation
- Understanding variable precedence
- Special Variables in Terraform

#### [2.2 Lists and Maps](./Module-02/2.2-Lists-Maps.md)

- Creating and manipulating lists
- Utilizing maps for key-value pairs

#### [2.3 Control Flow in HCL](./Module-02/2.3-Control-Flow.md)

- Conditional statements with `if` and `else`
- Loops and iterations
- Best practices for effective control flow

### Module 3: Organizing HCL Code

#### [3.1 Modularization in HCL](./Module-03/3.1-Modularization.md)

- Defining and creating modules
- Module structure and best practices
- Reusable components in HCL

#### [3.2 Managing Configurations](./Module-03/3.2-Managing-Configurations.md)

- Configuration files and their organization
- Creating and managing multiple environments
- Version control with Git and HCL

### Module 4: Advanced HCL Topics

#### [4.1 Functions in HCL](./Module-04/4.1-Functions.md)

- Exploring built-in functions
- Creating custom functions
- Advanced string manipulation and mathematical operations

#### [4.2 Working with Providers](./Module-04/4.2-Working-Providers.md)

- Understanding providers in HCL
- Configuring and using providers (e.g., AWS, Azure)
- Handling multiple providers in a single configuration

#### [4.3 Error Handling and Debugging](./Module-04/4.3-Error-Handling-Debugging.md)

- Debugging techniques in HCL
- Handling errors gracefully
- Best practices for troubleshooting

### Module 5: Real-world HCL Projects

#### [5.1 Building Infrastructure with Terraform](./Module-05/5.1-Building-Infrastructure.md)

- Creating and managing virtual machines
- Networking configurations
- Resource dependencies and outputs

#### 5.2 Creating Custom Machine Images with Packer

- Writing Packer templates in HCL
- Building custom images for different platforms
- Integrating Packer with other HashiCorp tools

### Module 6: Best Practices and Optimization

#### 6.1 HCL Best Practices

- Code readability and maintainability
- Naming conventions
- Documentation standards

#### 6.2 Optimizing HCL Code

- Performance considerations
- Efficient resource usage
- Strategies for code optimization

### Module 7: Application in DevOps Workflows

#### 7.1 Integration with CI/CD

- Incorporating HCL in continuous integration and delivery pipelines

#### 7.2 Infrastructure Orchestration

- Coordinating infrastructure changes with other DevOps processes
