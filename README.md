
# Create a Virtual Machine in the resource group along with virtual networks and subnets. Confirm the logins to VM after deploying the infrastructure.
# Write a custom module for multiple virtual machines deployment with the same configuration.








## first step 
Firstly we have installed teeraform and git in our local system.
Teeraform is used to write the infrastructure as a code and to write the code we use git console.

Rest of the commands we have used in Gitbash 
## Creating Environment 

Here we are creating directories in our system 


1. cd documents/

When you run the "cd documents/" command in Git, it will change the current working directory to the "documents" directory. If the "documents" directory doesn't exist, you will receive an error message.

2.  mkdir dir1
When you run the "mkdir dir1" command in Git Bash, it will create a new directory named "dir1" in the current working directory. If the "dir1" directory already exists, you will receive an error message.

3. cd dir1
When you run the "cd dir1" command in Git Bash, it will change the current working directory to the "dir1" directory. If the "dir1" directory doesn't exist, you will receive an error message.



#Note that Git doesn't have any specific functionality related to these command or navigating the file system. These command is a standard shell command that can be used in any terminal or command prompt, including the Git Bash terminal.

## Teeraform codes
# below are the teeraform commands we used to create instances in AWS

1. teeraform init

meaning :-
The "terraform init" command is a Terraform command used to initialize a Terraform working directory. The command is used to download and install the necessary provider plugins, setup the backend for storing the Terraform state, and configure any other required components.

after running this command

we will make files in dir1

using the vi editor and we will use ".tf" extention to convert the file into teeraform file.



now we have created 5 files 
1. vi main.tf
2. vi outputs.tf
3. vi provider.tf
4. vi teeraforms.tfvars
5. vi vars.tf





## vi main.tf



meaning :-
"main.tf" is a Terraform configuration file that defines the infrastructure as code. It specifies the resources that Terraform should manage and the provider that Terraform should use to interact with those resources. In this file, you can write Terraform code to create, update, or delete various cloud resources, such as virtual machines, networks, and databases.

resource "aws_instance" "my-machine" {
   count = 4   # Here we are creating identical 4 machines.
   ami = var.ami
   instance_type = var.instance_type
   tags = {
      Name = "my-machine-${count.index}"
           }
}


terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}
## vi outputs.tf

vi outputs.tf

meaning :-
The "outputs.tf" file in Terraform is used to declare output values for a Terraform configuration. Output values are a way to expose information about the infrastructure managed by Terraform to external tools or users. The information can include IP addresses, DNS names, and other details about the resources created.

output "ec2_machines" {
 # Here * indicates that there are more than one arn because count is 4
  value = aws_instance.my-machine.*.arn
}
## vi provider.tf

meaning :-
The "provider.tf" file in Terraform is used to configure the provider for Terraform to interact with the cloud infrastructure. The provider is responsible for managing the lifecycle of the resources, such as virtual machines, databases, and network components.


provider "aws" {
  region     = "ap-south-1"
  access_key = "AKIA6JO3MEWCOLIPB6GR"
  secret_key = "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"
}
## vi teeraforms.tfvars

vi terraforms.tfvars

meaning :-
The "terraform.tfvars" file in Terraform is used to store the values of variables in Terraform configurations. The values in this file can be used to set the values of variables in Terraform configurations, allowing you to parameterize your infrastructure as code.

ami = "ami-01a4f99c4ac11b03c"
instance_type = "t2.micro"

## vi .vars.tf

vi vars.tf

meaning :-
The "vars.tf" file in Terraform is used to declare variables for Terraform configurations. Variables are a way to parameterize Terraform configurations and make them more flexible and reusable.
By declaring variables in a "vars.tf" file, you can make your Terraform configurations more flexible and reusable.

# Creating a Variable for ami
variable "ami" {
  type = string
}

# Creating a Variable for instance_type
variable "instance_type" {
  type = string
}
## validate, plan and apply commands

teeraform validate
The "terraform validate" command is a Terraform command used to validate the syntax of the Terraform configuration files. The command is used to check that the Terraform configuration files are well-formed and free of syntax errors.

teeraform plan 
The "terraform plan" command is a Terraform command used to create an execution plan. The command is used to preview the changes that will be made to the infrastructure when Terraform applies the changes.

teeraform apply 
The terraform apply command is used to apply changes to an infrastructure managed by Terraform. When you run the terraform apply command, Terraform will compare the current state of the infrastructure with the desired state defined in your Terraform configuration files.