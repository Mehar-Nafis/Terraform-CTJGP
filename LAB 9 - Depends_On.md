## Creating Key Pair and passing the key when Creating an EC2 Instance
```
mkdir depends_on_lab && cd depends_on_lab
```


### Task-1: Creating Key-Pair
```
vi provider.tf
```
```hcl
provider "aws" {
  region = "us-east-1"
}
```
```
vi key.tf
```
```hcl

#Generating the Key pair
resource "tls_private_key" "capstone_key_pair" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

#Storing the Public key in AWS
resource "aws_key_pair" "capstone-key" {
  key_name   = "capstone-key"
  public_key = tls_private_key.capstone_key_pair.public_key_openssh  #Passing the Public Key 
}


#Store the private Key on Local
resource "local_file" "mykey_private" {
  content = tls_private_key.capstone_key_pair.private_key_pem
  filename = "capstone-key"
}

resource "local_file" "mykey_public" {
  content = tls_private_key.capstone_key_pair.public_key_openssh
  filename = "capstone-key.pub"
}

```
### Task-2: Passing the key when Creating an EC2 Instance
```
vi instance.tf
```
```hcl

resource "aws_instance" "ec2" {
  instance_type = "t2.micro"
  ami = "ami-023c11a32b0207432"                                   #ami is of Red HAt Linux
  key_name = "capstone-key"
  depends_on = [ aws_key_pair.capstone-key ]                      #The Key should be created first
  tags = {
    Name = "Ansible Server"}
}
```

```
terraform init
```
```
terraform plan 
```
```
terraform apply -auto-approve
```
```
ssh -i capstone-key ec2-user@IP_ADDRESS
```
You might get the below error

Permissions 0775 for 'capstone-key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "capstone-key": bad permissions
Permission denied (publickey).

Change your file permissions and try again
```
chmod 400 capstone-key
```
```
terraform destroy -auto-approve
```
```
cd .. && rm -rf depends_on_lab
