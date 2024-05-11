## Understanding Terraform Import
```
mkdir import_lab && cd import_lab
```
```
vi import.tf
```
Add the given lines, by pressing "INSERT" 
```
provider "aws" {
  region = "us-east-1"
}   

#Execute the below command
#terraform import aws_instance.test_instance <***Resource-ID***>

resource "aws_instance" "test_instance" {
  ami = "<***AMI_ID OF THE EC2 Instance to be IMPORTED***>"
  instance_type = "<***INSTANCE TYPE***>"
  tags = {
    name = "<TAGS if ANY / New Tags can be added as well>"
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
cd ..
```
```
rm -rf import_lab
```
