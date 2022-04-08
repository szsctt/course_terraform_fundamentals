# course_terraform_fundamentals
Notes from the A Cloud Guru course 'Terraform Fundamentals'

## Terraform fundamentals

### Terraform CLI

The main command is `terraform`, which accepts a variety of subcommands.  

A few commands:

 - `terraform version`: Find the terraform veresion
 - `terraform -chdir=<path_to/tf> <subcommand>`: Switch the working directory and run
 - `terraform init`: Initialise the directory
 - `terraform plan`: Create an execution plan
  - `-out <plan_name>`: Output to a file
  - `-destroy`: Dry-run of destroy  
 - `terraform apply`: Execute plan/apply changes
  - `<plan_name>`: Apply a specific plan
  - `-target=<resource_name>`: Only apply changes to a targeted resource
  - `-var my_variable=<variable>`: Pass a variable via the command line
 - `terraform destroy`: Destroy the managed infrastructure
 - `terraform providers`: Get provider info used in configuration

There is a [cheat sheet](https://acloudguru-content-attachment-production.s3-accelerate.amazonaws.com/1622032650435-terraform-cheatsheet-from-ACG.pdf)

### Configuration languague

The syntax of Terraform consists of :
  - blocks: containers for objects like resources
  - arguments: assign a value to a name
  - expressions: represent a value

The syntax is declarative - it specifies an intended goal, rather than steps to reach a goal to get to that goal.

The syntax of a block is:
```
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
	#Block body
	<IDENTIFIER> = <EXPRESSION> # Arguemnt
}
```

For example

```
resource "aws_vpc" "main" {
	cidr_block = var.base_cidr_block
}
```

Terraform files are plain text files with the `.tf` extension; you can also use a json variant of the language which uses a `.tf.json` file extension.

Text encoding should be UTF-8, usuualy use Unix-style line endings.

Modules are a collecion of `.tf` and/or `.tf.json` files kept together in a directory.  A module consists of the only the top-level confi files in the directory.  A nested directory is treated as a separate module and may not be automatically included.

The root module is the base of the terraform configuration.  The root module is the working directory where terraform is invoked, and may also contain child modules.

Override files can be used to override particular parts of a config file, and are merged with the config file when applied.

Config files can be expressed in HCL or JSON.  There are two key construcuts:

 - An argument assigns a value to a variable:  `image_id = "terra123"`
 - Identifies are things like argument names, block type names, resources, input variables, etc
 - Comments:  `#` or `//` begin a single line comment; `/*` and `*/` begin and end a multi-line comment
 - A block is a container for other content, including other blocks

```
resource "aws_instance" "example" {
	ami = "abc123"

	network_interface {
		# ...
	}
}
```

JSON cofig syntax examples.

A variable:
```
{
	"variable" : {
		"example": {
			"default" : "hello"
		}
	}
}
```

An intance type block:

```
{
	"resource": {
		"aws_instnace": {
			"example" : {
				"instance_type": "t2.micro",
				"ami": "ami-abc123"
			}	
		}
	}
}
```

### Working with resources

Resources are the most imporatnt part of the Terraform language.  Resource blocks describe infrastrcture objects like virtual networks, compute instances, or components like DNS records.  

### Input variables

### Declaring output variables

### Declaring local variables

### Modules

### Module sources

### Using expressions and functions

### Backend configuration

### Working with states

### Managing workspaces

