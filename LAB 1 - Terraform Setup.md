## Creating an EC2 Instance in AWS and Installing Terraform

To begin, log in to AWS Console.

### Task-1: Installing Terraform on Ubuntu operating system

* Manually Launch a `t2.micro` instance with OS version as `Ubuntu` (latest version) in the region of your choice.
* Use tag "`Name : TerraformServer`"
* Create a new Keypair with the Name `Terraform-Keypair-YourName`
* In security groups, include ports `22 (SSH)` and `80 (HTTP)`.
* Configure Storage: 10 GiB
* Launch the Instance.
* Once Launched, Connect to the Instance using `MobaXterm` or `Putty` or `EC2 Instance Connect` with username "`ubuntu`".

Once the EC2 is ready, follow the below Commands to perform lab:
```
sudo hostnamectl set-hostname TerraformServer
bash
```
```
sudo apt update
```
```
sudo apt install wget unzip -y
```
```
wget https://releases.hashicorp.com/terraform/1.8.3/terraform_1.8.3_linux_amd64.zip

```
To know the latest Terraform version - [Install Terraform](https://developer.hashicorp.com/terraform/downloads)
```
unzip terraform_1.8.3_linux_amd64.zip
```
```
ls
sudo mv terraform /usr/local/bin
```
```
rm terraform_1.8.3_linux_amd64.zip
```
```
ls
terraform
```
```
terraform -v
```

### Task-2: Install Required Packages and login to Ubuntu server using Credentials. 
```
sudo apt-get install python3-pip -y
```
```
sudo pip3 install awscli --break-system-packages
```
```
aws configure
```
* When it prompts for Credentials, Enter the Keys as example shown below
  
| `Access Key ID.` | `Secret Access Key ID.` |
| ------------------ | ------------------------- |
| AKIAIOSFODNN7EXAMPLE | wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY |

##### Note: If Credentials are not available generate from AWS IAM Service
Once LoggedIn check the account access
```
aws s3 ls
```
`Or` Use below command to check whether it is authenticated.
```
aws iam list-users
```
### Task-3: Now we are ready to perform the labs
Create directory as Lab1 & create local file
```
mkdir Lab1 && cd Lab1
```
```
vi local.tf
```
```
resource "local_file" "myfile" {

  filename = "/home/ubuntu/test.txt"
  content  = "wel come to terraform"
}
```
```
terraform init
```
```
terraform plan
```
```
terraform apply
```
To check whether the file is created follow the command

```
cd /home/ubuntu
ls
```
```
cat test.txt
```
Once Verified, you can destroy the File by changing it to the Lab1 Directory
```
cd Lab1
```
```
terraform destroy
```
```
cd ~
rm -rf Lab1
```
