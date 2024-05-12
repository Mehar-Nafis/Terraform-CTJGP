## Creating IAM Users, Groups using Terraform.
```
cd /home/ubuntu
```
```
mkdir iam-users && cd iam-users
```
Create a new `iam.tf` file to define your IAM resources.
```
vi iam.tf
```
Copy and paste the below Code to create users and group. 
```
# user
resource "aws_iam_user" "admin1" {
  name = "admin1"
}

resource "aws_iam_user" "admin2" {
  name = "admin2"
}

# group definition
resource "aws_iam_group" "administrators" {
  name = "administrators"
}

resource "aws_iam_policy_attachment" "administrators-attach" {
  name       = "administrators-attach"
  groups     = [aws_iam_group.administrators.name]
  policy_arn = "arn:aws:iam::aws:policy/AdministratorAccess"
}

resource "aws_iam_group_membership" "administrators-users" {
  name = "administrators-users"
  users = [
    aws_iam_user.admin1.name,
    aws_iam_user.admin2.name,
  ]
  group = aws_iam_group.administrators.name
}

output "warning" {
  value = "WARNING: make sure you're not using the AdministratorAccess policy for other users/groups/roles. If this is the case, don't run terraform destroy, but manually unlink the created resources"
}
```
```
vi provider.tf
```
```
provider "aws" {
  region = var.AWS_REGION
}
```
```
vi vars.tf
```
```
variable "AWS_REGION" {
  default = "us-east-2"
}
```
```
terraform init
```
```
terraform fmt
```
```
terraform plan
```
```
terraform apply
```
Once applied, verify the IAM User and group in the console and then Destroy.
```
terraform destroy
```
Once destroyed, remove the Directory.
```
cd ~
rm -rf iam-users
```

