## Data sources

```
cd ~
```
```
mkdir lab6 && cd lab6
```
```
vi data.tf
```

Add the given lines, by pressing "INSERT" 
```
provider "aws" {
  region     = "us-east-2"
}

data "aws_ami" "ami" {
  most_recent = true
  owners = ["amazon"]


  filter {
    name   = "name"
    values = ["amzn2-ami-hvm*"]
  }
}

resource "aws_instance" "ec2instance" {
    ami = data.aws_ami.ami.id
   instance_type = "t2.micro"
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
