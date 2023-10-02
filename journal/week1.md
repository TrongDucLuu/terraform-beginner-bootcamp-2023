# Terraform Beginner Bootcamp 2023 - Week 1

## Root Module Structure

Our root module structure is as follows:

```
PROJECT_ROOT
│
├── main.tf                 # everything else.
├── variables.tf            # stores the structure of input variables
├── terraform.tfvars        # the data of variables we want to load into our terraform project
├── providers.tf            # defined required providers and their configuration
├── outputs.tf              # stores our outputs
└── README.md               # required for root modules
```

[Standard Module Structure](https://developer.hashicorp.com/terraform/language/modules/develop/structure)

## Terraform and Input Variables

### Terraform Cloud Variables

In terraform we can set two kind of variables:
- Enviroment Variables - those you would set in your bash terminal eg. AWS credentials
- Terraform Variables - those that you would normally set in your tfvars file

We can set Terraform Cloud variables to be sensitive so they are not shown visibliy in the UI.

### Loading Terraform Input Variables

[Terraform Input Variables](https://developer.hashicorp.com/terraform/language/values/variables)

### var flag
We can use the `-var` flag to set an input variable or override a variable in the tfvars file eg. `terraform -var user_ud="my-user_id"`

### var-file flag

- TODO: document this flag
--->
The -var-file flag in Terraform is used to specify a file that contains variable values for a Terraform configuration. This flag allows you to provide values for variables without directly modifying the Terraform configuration files, which can be useful for keeping sensitive or environment-specific data separate from the main configuration.  

### terraform.tvfars

This is the default file to load in terraform variables in blunk

### auto.tfvars

- TODO: document this functionality for terraform cloud
--->
The auto.tfvars file in Terraform serves as a mechanism to automatically load variable values into a Terraform configuration. When Terraform executes, it looks for and automatically loads the variable values from this file unless overridden by another source.

Here's how it functions:

Automatic Variable Assignment: If Terraform detects a file named auto.tfvars in the working directory, it will automatically load the variable values from this file.

Variable Definitions: The auto.tfvars file typically contains variable definitions in the form of variable-value pairs, using the same syntax as Terraform variable definitions in a .tf file.

For example:
```
hcl

region = "us-west-2"
instance_type = "t2.micro"
```
Variable Overrides: These variable values can be overridden by providing them through other means like command-line flags, environment variables, or through variable files specified using the -var-file option.

Using auto.tfvars helps in automatically providing default or commonly used values for variables, making it easier to manage and maintain configurations. However, it's essential to be cautious and ensure that sensitive information like credentials is not stored in this file or any version control system. It's common practice to add auto.tfvars to the .gitignore file to prevent accidental exposure of sensitive data.

### order of terraform variables

- TODO: document which terraform variables takes presendence.
--->
The priority of variable values is such that values specified at higher levels (e.g., CLI flags) will override values specified at lower levels (e.g., default values in the configuration). This allows for flexibility in setting variables based on different contexts without modifying the main configuration.

## Dealing With Configuration Drift

## What happens if we lose our state file?

If you lose your statefile, you most likley have to tear down all your cloud infrastructure manually.

You can use terraform port but it won't for all cloud resources. You need check the terraform providers documentation for which resources support import.

### Fix Missing Resources with Terraform Import

`terraform import aws_s3_bucket.bucket bucket-name`

[Terraform Import](https://developer.hashicorp.com/terraform/cli/import)
[AWS S3 Bucket Import](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket#import)

### Fix Manual Configuration

If someone goes and delete or modifies cloud resource manually through ClickOps. 

If we run Terraform plan is with attempt to put our infrstraucture back into the expected state fixing Configuration Drift