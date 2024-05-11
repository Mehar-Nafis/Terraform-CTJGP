## Understanding local values

### Local Values 
```
cd ~
```
```
mkdir lab5 && cd lab5
```
```
vi local.tf
```
Add the given lines, by pressing "INSERT" and replace "ENTER THE AMI VALUE" with actual values
```
provider "aws" {
  region     = "us-east-1"
}

locals {
  custom_tags = {
    Team = "DevOps"
    Company = "CloudThat"
  }
}
resource "aws_instance" "instance1" {
   ami = "******ENTER THE AMI VALUE********"
   instance_type = "t2.micro"
   tags = local.custom_tags
}

resource "aws_instance" "instance2" {
   ami = "******ENTER THE AMI VALUE********"
   instance_type = "t2.small"
   tags = local.custom_tags
}

resource "aws_ebs_volume" "db_ebs" {
  availability_zone = "us-east-1a"
  size              = 8
  tags = local.custom_tags
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
rm -rf lab5
```
