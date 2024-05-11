## Understanding Terraform functions 
### Functions
```
cd ~
```
```
mkdir lab6 && cd lab6
```
```
vi functions.tf
```
Add the given lines, by pressing "INSERT" 
```
provider "aws" {
  region     = var.region
}

variable "region" {
  default = "ap-south-1"
}

variable "tags" {
  type = list
  default = ["ec2-1","ec2-2"]
}

variable "ami" {
  type = map
  default = {
    "us-east-1" = "ami-0fc5d935ebf8bc3bc"         ******ENTER THE AMI VALUE********
    "us-west-1" = "ami-060d3509162bcc386"         ******ENTER THE AMI VALUE********
    "ap-south-1" = "ami-09ba48996007c8b50"        ******ENTER THE AMI VALUE********
  }
}

resource "aws_instance" "application-servers" {
   ami = lookup(var.ami,var.region)
   instance_type = "t2.micro"
   count = 2

   tags = {
     Name = element(var.tags,count.index)
   }
}
```

Save the file using "ESCAPE + :wq!"
```
terraform init
```
```
terraform plan
```
```
terraform apply
```
```
terraform destroy
```
```
cd ~
rm -rf lab6
```
