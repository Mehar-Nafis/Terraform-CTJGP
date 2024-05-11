### Launching your first AWS EC2 instance using Terraform 
```
cd ~
mkdir EC2-lab && cd EC2-lab/
```
```
vi example.tf
```
Add the given lines, by pressing "INSERT"

##### Note: 
1. Replace your allocated `Region` and `AMI ID` of the same Region.
2. `"Yourname-EC2-1"` with Your Name.
```
provider "aws" {
  profile = "default" # This line is not mandatory.
  region  = "us-east-2"
}

resource "aws_instance" "example" {
  ami           = "ami-07efac79022b86107"
  instance_type = "t2.micro"
  tags = {
    Name = "Yourname-EC2-1"
  }
}
```
Save the file using "ESCAPE + :wq!"
```
terraform init
```
```
terraform fmt
```
```
terraform validate
```
```
terraform plan
```
```
terraform apply
```
```
#List the files
ls 
```
To see what is saved in `terraform.tfstate` use the below command.

```
cat terraform.tfstate
```
Now, Let's Replace the AMI ID with `Amazon Linux AMI 2023` from the same region and see what happens.

`Note:` To get the `Amazon Linux AMI 2023` go to EC2 Instances, click on Launch, and select the `Amazon Linux AMI 2023` AMI and copy the ID and paste in File.
```
vi example.tf
```
Replace the AMI ID, by pressing "INSERT"  
```
provider "aws" {
  profile = "default"
  region  = "us-east-2"
}

resource "aws_instance" "example" {
  ami           = "ami-02a89066c48741345"
  instance_type = "t2.micro"
  tags = {
    Name = "Yourname-TF-1"
  }
}
```

Save the file using "ESCAPE + :wq!"

Now in Terraform Plan Verify the Changes.
```
terraform plan
```
```
terraform apply
```
Once Applied then go to the console and see that the Previous EC2 is being destroyed and new EC2 is getting created.
    
Also verify that the OS is `Amazon Linux AMI 2023`

Again when you cat the `terraform.tfstate` file it shows a new AMI ID.
```
cat terraform.tfstate
```
Use the `terraform destroy` command for cleaning the infrastructure used in this lab
```
terraform destroy
```
Finally, verify that the resources are deleted in the Console.
```
cd ~
rm -rf EC2-lab
```
