## Terraform Basics

```tf
provider "aws" {
  profile = "default"
  region  = "us-east-1"
}
resource "aws_instance" "example" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

### Providers

The provider block configures the named provider, in our case aws, which is responsible for creating and managing resources. A provider is a plugin that Terraform uses to translate the API interactions with the service. 

### Resources
The resource the block defines a piece of infrastructure. A resource might be a physical component such as an EC2 instance, or it can be a logical resource such as a Heroku application.

The resource block has two strings before the block: the resource type and the resource name. In the example, the resource type is aws_instance and the name is example. The prefix of the type maps to the provider. In our case, "aws_instance" automatically tells Terraform that it is managed by the "aws" provider.


### Initialize the directory
When you create a new configuration — or check out an existing configuration from version control — you need to initialize the directory with **terraform init.**
Terraform downloads the aws provider and installs it in a hidden subdirectory of the current working directory

### Format and validate the configuration
We recommend using consistent formatting in files and modules written by different teams. The terraform fmt the command automatically updates configurations in the current directory for easy readability and consistency.

Format your configuration. Terraform will return the names of the files it formatted. In this case, your configuration file was already formatted correctly, so Terraform won’t return any file names.

```tf
$ terraform fmt
```
### Validate your configuration

If your configuration is valid, Terraform will return a success message.

```tf
$ terraform validate
```
Success! The configuration is valid.

### Create infrastructure
In the same directory as the example.tf the file you created, run terraform apply.

```tf
$ terraform apply
```

### Inspect state
When you applied your configuration, Terraform wrote data into a file called terraform.tfstate. This file now contains the IDs and properties of the resources Terraform created so that it can manage or destroy those resources going forward.

👉 **Inspect the current state using terraform show.**

### Manually Managing State
Terraform has a built-in command called terraform state for advanced state management. For example, if you have a long state file, you may want a list of the resources in the state, which you can get by using the list subcommand.

```tf
$ terraform state list
aws_instance.example
```
