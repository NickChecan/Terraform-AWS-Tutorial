Before executing, it is necessary to install and configure the AWS CLI through the following link
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html

Environment variables for the Terraform AWS provider to consume:
* export AWS_ACCESS_KEY_ID="<YOUR_AWS_ACCESS_KEY_ID>"
* export AWS_SECRET_ACCESS_KEY="<YOUR_AWS_SECRET_ACCESS_KEY>"
* export AWS_DEFAULT_REGION="<YOUR_AWS_DEFAULT_REGION>"

### Initialize and download the provider
$ terraform init

### Apply the configuration
$ terraform apply

### Remove all the resources
$ terraform destroy

### Format the configuration
$ terraform fmt

### Make sure the configuration is syntactically valid and internally consistent
$ terraform validate

### Inspect State
$ terraform show

### Manually Manage State
$ terraform state list

### Display Output
$ terraform output

# State
When you applied your configuration, Terraform wrote data into a file called terraform.tfstate. Terraform stores the IDs and properties of the resources it manages in this file, so that it can update or destroy those resources going forward.

# Terraform Block
The terraform {} block contains Terraform settings, including the required providers Terraform will use to provision your infrastructure. For each provider, the source attribute defines an optional hostname, a namespace, and the provider type. Terraform installs providers from the Terraform Registry by default. In this example configuration, the aws provider's source is defined as hashicorp/aws, which is shorthand for registry.terraform.io/hashicorp/aws.

You can also set a version constraint for each provider defined in the required_providers block. The version attribute is optional, but we recommend using it to constrain the provider version so that Terraform does not install a version of the provider that does not work with your configuration. If you do not specify a provider version, Terraform will automatically download the most recent version during initialization.

# Providers
The provider block configures the specified provider, in this case aws. A provider is a plugin that Terraform uses to create and manage your resources.

The profile attribute in the aws provider block refers Terraform to the AWS credentials stored in your AWS configuration file, which you created when you configured the AWS CLI. Never hard-code credentials or other secrets in your Terraform configuration files. Like other types of code, you may share and manage your Terraform configuration files using source control, so hard-coding secret values can expose them to attackers.

You can use multiple provider blocks in your Terraform configuration to manage resources from different providers. You can even use different providers together. For example, you could pass the IP address of your AWS EC2 instance to a monitoring resource from DataDog.

# Resources
Use resource blocks to define components of your infrastructure. A resource might be a physical or virtual component such as an EC2 instance, or it can be a logical resource such as a Heroku application.

Resource blocks have two strings before the block: the resource type and the resource name. In this example, the resource type is aws_instance and the name is app_server. The prefix of the type maps to the name of the provider. In the example configuration, Terraform manages the aws_instance resource with the aws provider. Together, the resource type and resource name form a unique ID for the resource. For example, the ID for your EC2 instance is aws_instance.app_server.

Resource blocks contain arguments which you use to configure the resource. Arguments can include things like machine sizes, disk image names, or VPC IDs. Our providers reference lists the required and optional arguments for each resource. For your EC2 instance, the example configuration sets the AMI ID to an Ubuntu image, and the instance type to t2.micro, which qualifies for AWS' free tier. It also sets a tag to give the instance a name.

# More Information
* Changes on the AMI requires Terraform to destroy and recreate the EC2 instance
* Outputs will present useful information to the Terraform user

# Saving the state file on the Terraform Cloud
Steps to follow in order to store the configuration file on the Terraform Cloud platform:
* Create an organization on the terraform cloud

### Login to Terraform Cloud
$ terraform login

### Remove the Terraform state file from the local project
$ rm terraform.tfstate

### Configure the environment variables on the workspace/organization
* AWS_SECRET_ACCESS_KEY 
* AWS_ACCESS_KEY_ID