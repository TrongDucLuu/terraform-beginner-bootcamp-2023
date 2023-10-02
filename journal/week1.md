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

The -var-file flag in Terraform is used to specify a file that contains variable values for a Terraform configuration. This flag allows you to provide values for variables without directly modifying the Terraform configuration files, which can be useful for keeping sensitive or environment-specific data separate from the main configuration.

### terraform.tvfars

This is the default file to load in terraform variables in blunk

### auto.tfvars

Using auto.tfvars helps in automatically providing default or commonly used values for variables, making it easier to manage and maintain configurations. However, it's essential to be cautious and ensure sensitive information like credentials is not stored in this file or any version control system. It's common practice to add auto.tfvars to the .gitignore file to prevent accidental exposure of sensitive data.

### order of terraform variables

The priority of variable values is such that values specified at higher levels (e.g., CLI flags) will override values specified at lower levels (e.g., default values in the configuration). This allows for flexibility in setting variables based on different contexts without modifying the main configuration.

It's essential to handle sensitive data carefully, especially when using command-line flags or environment variables, to avoid exposing sensitive information.
