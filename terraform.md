# Contents

- [Resources](#Resources)
- [Concepts](#Concepts)
- [HCL - HashiCorp Configuration Language](#HCL - HashiCorp Configuration Language)
- [File Structure](#File Structure)
- [Main TF file](#Main TF file)
- [Blocks](#Blocks)
    - [Terraform](#Blocks#Terraform)
    - [Provider](#Blocks#Provider)
    - [Resource](#Blocks#Resource)
    - [Data](#Blocks#Data)
    - [Variable](#Blocks#Variable)
    - [Output](#Blocks#Output)
    - [Module](#Blocks#Module)
    - [Locals](#Blocks#Locals)
- [Basic Programming](#Basic Programming)
    - [Variables](#Basic Programming#Variables)
    - [Interpolation](#Basic Programming#Interpolation)
    - [Conditionals](#Basic Programming#Conditionals)
    - [Loops](#Basic Programming#Loops)
    - [Functions](#Basic Programming#Functions)
    - [Modules](#Basic Programming#Modules)
- [CLI](#CLI)
- [Providers](#Providers)

TERRAFORM
:terraform:

# Resources

[Tutorials | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/tutorials)

[Custom Framework Providers | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/tutorials/providers-plugin-framework)

# Concepts

Terraform is a tool for provisioning and managing infrastructure as code. The main concepts of Terraform include:
    * Resources: Representations of infrastructure components, such as virtual machines, databases, and networking components.
    * Providers: Plugins for Terraform that interact with specific infrastructure providers, such as AWS, GCP, Azure, or other.
    * State: Terraform keeps track of the current state of the infrastructure it manages, and uses this information to determine what actions to take. State file is a JSON file that Terraform uses to keep track of the current state of the infrastructure and to make decisions about what actions to take when changes are made.
    * Configuration files: Terraform uses configuration files written in the HashiCorp Configuration Language (HCL) to define the desired state of the infrastructure. These files define the infrastructure resources and the relationships between them.
    * Modules: Modules allow for the reuse of common resource configurations, and can be called multiple times within a single configuration file. They are essentially reusable units of Terraform code that can be shared between projects and teams.
    * Variables: Variables allow for easy parameterization of resource configurations, making it easier to maintain and manage different environments.
    * Outputs: Outputs allow you to export information about the infrastructure Terraform manages, such as the IP address of a virtual machine.
    * CLI: A command-line interface for executing Terraform commands and interacting with the infrastructure.

Overall Terraform is a powerful tool that helps to manage infrastructure resources in a consistent and predictable way, allowing to automate the provisioning and management of infrastructure resources.

# HCL - HashiCorp Configuration Language

The HashiCorp Configuration Language (HCL) is the language used to write Terraform configuration files.

Here are the links to the official HashiCorp documentation for HCL:
    * [Overview - Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language)
        * [Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/tutorials/configuration-language)
    * [Syntax - Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language/syntax/configuration)
    * [Functions - Configuration Language | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/language/functions)

The documentation provides examples and explanations for all the features of HCL, including:
    * Basic syntax and structure of HCL configuration files
    * Resources and data sources
    * Providers and provider configuration
    * Input and output variables
    * Conditional and looping constructs
    * Expressions and functions
    * And many more

# File Structure

This is just one example of how you can structure a Terraform project, and the actual structure may vary depending on your specific needs:

```
my_project/
  |- main.tf
  |- variables.tf
  |- outputs.tf
  |- modules/
      |- module_1/
          |- main.tf
          |- variables.tf
          |- outputs.tf
      |- module_2/
          |- main.tf
          |- variables.tf
          |- outputs.tf
  |- .terraform/
      |- plugins/
  |- terraform.tfstate
```

    * `main.tf`: The main Terraform configuration file, where you define your infrastructure resources, providers, and modules.
    * `variables.tf`: A Terraform configuration file where you define variables that can be used throughout your Terraform configuration. This helps you make your code more flexible and reusable.
    * `outputs.tf`: A Terraform configuration file where you define outputs that can be displayed after Terraform runs. This makes it easier to understand the end state of your infrastructure.
    * `modules/`: A directory where you can store Terraform modules that can be used throughout your project.
    * `.terraform/`: A hidden directory where Terraform keeps its state and plugins.
    * `terraform.tfstate`: A JSON file that Terraform uses to store the current state of your infrastructure. This file is updated each time Terraform runs and is used to determine the changes that need to be made when you run Terraform again.

Plugins installed on one OS may not work on another OS, and you may need to recompile the plugins or use the provider source option to manage the plugins across different operating systems. This is because the plugins are compiled for specific architectures (e.g. x86, ARM), and the underlying dependencies and libraries may be different between the two operating systems.

If you want to use the same plugins on multiple operating systems, you would need to install the plugins for each operating system where Terraform will be used. Alternatively, you can use Terraform's "provider source" option to specify the location of a provider binary, which can be a local file or a remote URL. This way, you can manage the provider binaries independently of Terraform, and use the same binary across multiple operating systems.

# Main TF file

In Terraform, the main configuration file is typically named main.tf, and it is used to define the resources you want to manage with Terraform. The following are some of the common blocks that can be used in the main.tf file:

# Blocks

These are the most common blocks used in Terraform configurations, but there are others as well. 

## Terraform

    terraform: The Terraform block is a top-level block in Terraform configuration files that provides options for controlling various aspects of Terraform's behavior. Some of the options that can be set in the Terraform block include:
        required_providers: This option specifies a map of provider names to version constraints, indicating which providers Terraform should install if they're not already available.
        required_version: This option specifies the minimum version of Terraform that's required to run the configuration.
        backend: This option sets the backend for storing Terraform state. Terraform supports multiple backends, including local, S3, and Azure.
```
terraform {
  required_providers {
    aws = "~> 2.0"
  }

  required_version = ">= 0.14"

  backend "s3" {
    bucket = "my-terraform-state-bucket"
    key    = "path/to/my/state/file"
    region = "us-west-2"
  }
}
```

## Provider

    provider: Specifies the provider for the resources you want to manage. For example, you can use the AWS provider to manage AWS resources.
```
provider "aws" {
  region = "us-west-2"
}
```

## Resource

    resource: Defines a resource that you want to manage with Terraform. A resource can be a virtual machine, a database, a network interface, etc.
```
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

Resource blocks have two strings before the block: the resource type and the resource name. The prefix of the type maps to the name of the provider. `aws_` is the provider, `instance` is the type, and `example` is the name. This makes the recourse ID: `aws_instance.example`

Resource blocks contain arguments which are used to configure the resource. Provider reference documents the required and optional arguments for each resource: [Provider reference](https://developer.hashicorp.com/terraform/language/providers)

## Data

    data: Specifies data sources used to look up information about external resources or configurations.
```
data "aws_ami" "example" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-2.0.*"]
  }
}
```

## Variable

    variable: Defines a variable that can be used in your Terraform configuration. Variables allow you to parameterize your Terraform configuration and make it more reusable.
```
variable "instance_type" {
  type        = string
  default     = "t2.micro"
  description = "The type of EC2 instance to launch"
}
```

## Output

    output: Defines an output value that can be accessed after Terraform has finished executing. Output values can be used to pass information between Terraform configurations or to display information to the user.
```
output "public_ip" {
  value = aws_instance.example.public_ip
}
```

## Module

    module: Defines a module, which is a self-contained unit of Terraform configuration. Modules allow you to organize and reuse Terraform configurations.
```
module "example" {
  source = "terraform-aws-modules/vpc/aws"
  
  name = "my-vpc"
  cidr = "10.0.0.0/16"
}
```

## Locals

    locals: Defines local values that can be used within the Terraform configuration. Locals can be used to simplify complex expressions or to define values that are used multiple times within the same module.
```
locals {
  instance_count = var.instance_count
  instance_type  = var.instance_type
}

resource "aws_instance" "example" {
  count  = local.instance_count
  ami    = var.ami
  type   = local.instance_type
}
```


# Basic Programming

Terraform configuration files use the HashiCorp Configuration Language (HCL), which is a declarative language that includes some basic programming features. Here are some of the programming features available in Terraform:

Below are the main programming features available in Terraform. While Terraform is not a full-fledged programming language, these features do allow you to create complex infrastructure configurations and automate deployment processes.

You can find the reference for all the Terraform concepts in the Terraform documentation: https://www.terraform.io/docs/index.html

The Terraform documentation provides comprehensive information on all aspects of Terraform, including:
    * Variables: https://www.terraform.io/docs/configuration/variables.html
    * Interpolation: https://www.terraform.io/docs/configuration/interpolation.html
    * Conditionals: https://www.terraform.io/docs/configuration/expressions.html#conditionals
    * Loops: https://www.terraform.io/docs/configuration/expressions.html#for-expressions
    * Functions: https://www.terraform.io/docs/configuration/functions.html
    * Modules: https://www.terraform.io/docs/configuration/modules.html

In addition to the above, the Terraform documentation provides information on other aspects of Terraform, including providers, resources, provisioners, and more.

## Variables

Terraform supports defining variables that can be reused throughout the configuration. You can define variables with default values, and also specify the type of the variable (e.g. string, number, list, etc.).

```
variable "aws_region" {
  type        = string
  description = "The AWS region to launch the EC2 instance in."
  default     = "us-west-2"
}

variable "instance_type" {
  type        = string
  description = "The EC2 instance type to launch."
  default     = "t2.micro"
}

provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = var.instance_type
}
```
In this example, two variables are defined: aws_region and instance_type. The variable block is used to define variables in Terraform and the type and description arguments are used to specify the type of the variable and provide a brief description of its purpose. The default argument is used to specify a default value for the variable, which will be used if a value is not provided when the Terraform configuration is applied.

The variables are then referenced in the provider and resource blocks using the var prefix. The aws_region variable is used to set the region argument in the provider block, and the instance_type variable is used to set the instance_type argument in the resource block.

This is just one example of how variables can be used in Terraform, but they can be used in a variety of other ways as well, such as passing values from the command line, or reading values from a file. The ability to reuse values across your configuration makes it easy to manage complex infrastructure and make changes without having to modify many different parts of your code.

## Interpolation

Terraform supports string interpolation, which allows you to embed variables and expressions within strings. Interpolation is done using the ${...} syntax.

```
variable "instance_count" {
  type        = number
  description = "The number of EC2 instances to launch."
  default     = 1
}

provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  count       = var.instance_count
  ami         = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "instance-${count.index + 1}"
  }
}
```
In this example, an EC2 instance resource is defined with a count argument set to var.instance_count. The value of var.instance_count is obtained from the instance_count variable defined earlier. The tags argument is used to add tags to the EC2 instances, and the Name tag is set using interpolation. The ${count.index + 1} expression is used to generate a unique name for each EC2 instance, where count.index is a special Terraform variable that returns the current index of the resource being created.

Interpolation expressions are evaluated during the Terraform run and allow you to dynamically generate values based on other values in your configuration. Interpolation is a powerful feature that makes it easy to create reusable and flexible Terraform configurations.

## Conditionals

Terraform supports conditional statements using the if expression. This allows you to specify different behaviors depending on the values of variables or other expressions.

```
variable "environment" {
  type        = string
  description = "The environment to deploy the instances to (dev or prod)."
  default     = "dev"
}

provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami         = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "instance-dev"
  }

  # Only add the Environment tag for the prod environment
  tags = {
    Name     = "instance-prod"
    Environment = "prod"
  }
}
```

In this example, Terraform creates an EC2 instance and adds two tags to it. By default, the Name tag is set to instance-dev. However, if the value of the environment variable is prod, an additional Environment tag is added with a value of prod. This is achieved using the tags block, which is repeated twice with different values. Terraform evaluates the condition environment == "prod" and only applies the second tags block if the condition is true.

Conditionals in Terraform allow you to control the behavior of your resources based on certain conditions. You can use conditionals to add or remove resources, set values, or even perform complex operations. This makes it easy to customize your Terraform configurations for different use cases, environments, or scenarios.

## Loops

Terraform supports the for_each expression, which allows you to repeat a set of operations for each item in a list.


```
variable "instance_count" {
  type        = number
  description = "The number of instances to launch."
  default     = 1
}

provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  count = var.instance_count

  ami         = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "instance-${count.index}"
  }
}
```
In this example, Terraform launches multiple EC2 instances by using the count argument in the aws_instance resource block. The number of instances to launch is determined by the instance_count variable, which has a default value of 1. Terraform uses the count.index expression to create a unique Name tag for each instance.

Loops in Terraform allow you to repeat a block of code multiple times. This is useful for creating many similar resources, such as instances, load balancers, or subnets. The count argument can be set to a number, a list, or a map, depending on the use case. You can use loops to automate the deployment of infrastructure and simplify your Terraform configurations.

## Functions

Terraform provides a set of built-in functions that can be used in expressions, such as string manipulation functions, mathematical functions, and data type conversion functions.
```
variable "image_id" {
  type = string
}

locals {
  formatted_image_id = format("ami-%s", substring(var.image_id, 0, 8))
}

resource "aws_instance" "example" {
  ami = local.formatted_image_id
  instance_type = "t2.micro"
}
```

In this example, Terraform uses the substring and format functions to manipulate the value of the image_id variable. The substring function extracts the first 8 characters of the image_id string, and the format function creates a new string by using the ami- prefix and the shortened image_id. The resulting string is assigned to the formatted_image_id local variable, which is used as the ami argument for the aws_instance resource.

Functions in Terraform allow you to perform complex operations on values and data, such as string manipulation, mathematical operations, or conditional statements. You can use functions to simplify your Terraform configurations and improve the readability of your code. Some common functions in Terraform include format, substr, length, upper, lower, floor, ceil, max, min, abs, and element.

You can find the complete list of functions in Terraform in the Terraform documentation: https://www.terraform.io/docs/configuration/functions.html.

In the documentation, you can find the syntax and usage for each function, along with examples of how to use them in your Terraform configurations. The functions are organized by category, including string functions, number functions, conditional functions, list functions, set functions, map functions, and more.

## Modules

Terraform modules provide a way to organize and share code between configurations. Modules can be defined in Terraform configuration files and reused across multiple projects.

Modules in Terraform are self-contained packages of Terraform configurations that are reusable and can be managed as a group. Modules allow you to organize your Terraform code, promote code reuse, and simplify large infrastructure deployments.

Here's an example of how to use modules in Terraform:

```
module "network" {
  source = "./network"

  vpc_cidr = "10.0.0.0/16"
  public_subnet_cidrs = ["10.0.1.0/24", "10.0.2.0/24"]
  private_subnet_cidrs = ["10.0.3.0/24", "10.0.4.0/24"]
}

module "web_server" {
  source = "./web_server"

  vpc_id = module.network.vpc_id
  public_subnet_ids = module.network.public_subnet_ids
  instance_type = "t2.micro"
  ami = "ami-0c55b159cbfafe1f0"
}
```

In this example, there are two modules: the network module and the web_server module. The network module creates a virtual private cloud (VPC) and subnets, and the web_server module creates EC2 instances in the public subnets of the VPC.

The module blocks in the Terraform configuration specify the source of the modules, and the input variables for the modules. The source of the module can be a local directory or a remote repository. The input variables allow you to customize the behavior of the modules and pass data between modules.

Modules in Terraform are a powerful tool for managing infrastructure as code, and can help you structure your Terraform configurations for easier management and maintenance.

# CLI

Terraform provides several subcommands that you can use to manage and interact with Terraform configurations.

`terraform <subcommand>` Here are some of the most commonly used subcommands:
    * `init`: Initializes Terraform and downloads the required provider plugins. This is usually the first command you run after writing your Terraform configuration. It also creates a file .terraform.lock.hcl specifying the exact provider versions used, so you can control when to update them.
    * `fmt`: automatically updates configurations in the current dir for readability and consistency.
    * `validate`: validate syntax of the configuration
    * `plan`: Generates and shows an execution plan for your Terraform configuration. This command allows you to preview the changes that Terraform will make to your infrastructure before you actually apply those changes.
    * `apply`: Applies the changes to your infrastructure described in your Terraform configuration. This command creates or updates the infrastructure resources based on the Terraform configuration. Terraform prompts you for "yes" before applying.
    * `show`: Shows the Terraform state or plan. This is useful for inspecting the current state of your infrastructure or the execution plan. It reads from the terraform.tfstate file. This file is sensitive.
        * `terraform state list` advanced command to manage state - list resources.
    * `refresh`: Refreshes the state of your Terraform configuration and updates it with the current state of your infrastructure. This is useful if you have made changes to your infrastructure outside of Terraform.
    * `import`: Imports existing resources into Terraform's state. This allows you to manage existing infrastructure with Terraform.
    * `validate`: Validates the syntax of your Terraform configuration and reports any errors. This is a good command to run before applying changes to your infrastructure, to ensure that your Terraform configuration is well-formed and error-free.
    * `destroy`: Destroys the resources described in your Terraform configuration. This is a destructive operation and should be used with caution.

# Providers

Providers are written in Go, using Terraform Plugin SDK.

Plugin development Docs: [Home - Plugin Development | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/plugin)

Tutorials: [Custom SDK Providers | Terraform | HashiCorp Developer](https://developer.hashicorp.com/terraform/tutorials/providers)

When writing Terraform providers, here are some important elements to consider:

    Provider Configuration: Terraform uses providers to interact with external resources, and it is important to properly configure the provider in the Terraform code.

    Resource Types: Each provider supports a set of resource types, and it is crucial to understand the available resource types and how to create and configure them in Terraform code.

    Data Sources: Data sources allow Terraform to retrieve information from external sources and use it in Terraform code. It is important to understand how to use data sources and retrieve the necessary information for Terraform code.

    Testing: Writing tests for Terraform providers is essential for ensuring the provider code is functioning correctly and producing the expected results.

    Provider Plugins: Terraform providers can be distributed as plugins, and it is important to understand the plugin installation process and how to properly configure the plugins in Terraform code.

    Resource Graph: Terraform uses a resource graph to determine the order in which resources should be created and managed. It is important to understand how the resource graph is constructed and how it impacts the execution of Terraform code.

    Provider State: Terraform providers maintain a state file to keep track of the resources they manage, and it is important to understand how this state is stored and managed, and how to properly update it in Terraform code.
