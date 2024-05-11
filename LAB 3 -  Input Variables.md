## Input Variables


### Task-1: Create EC2 instance using Input variables with default values
```
cd ~
```
```
mkdir variables-lab && cd variables-lab/
```
Now Create Files ie. `provider.tf,` `vars.tf,`  `instance.tf.`
```
vi vars.tf
```
Add the given lines, by pressing "INSERT" also replace your `Region`
```
variable "AMIS"{
  description = "Redhat ami ID for the EC2 Instance"
  default = "ami-0d77c9d87c7e619f9"
}

variable "Instance_type"{
  description = "Instance type for the EC2 Instance"
  default = "t2.micro"
}

variable "AWS_REGION"{
  default = "us-east-2"
}
```
Save the file using "ESCAPE + :wq!"

```
vi provider.tf
```
Add the given lines, by pressing "INSERT" 
```
provider "aws"{
  region = var.AWS_REGION
}
```
Save the file using "ESCAPE + :wq!"
```
vi instance.tf
```
Add the given lines, by pressing "INSERT" Also replace your `region's AMI ID` and `YourName`
```
resource "aws_instance" "terraform_example"{
  ami = var.AMIS
  instance_type = var.Instance_type
  tags = {
    Name = "Variables-Lab3-YourName"
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
Once applied, go to the Console and check that the new EC2 is created using Variables.


### Task-2: Create EC2 instance using Input variables with -var flag

We will be using same configuration file created above but when applying will pass the variable values with **-var** flag to see the precedance

```
terraform apply -var="AMIS=ami-09040d770ffe2224f" -var="Instance_type=t3.micro"
```

### Task-3: Create EC2 instance using Input variables with Environment Variable
Now we will be using same configuration file created above but when applying will pass the variable values from **ENV variables** to see the precedance

```
export TF_VAR_Instance_type="t3.medium"
```
```
printenv
```
```
terraform apply 
```


### Task-4: Implementing map variables that dynamically fetch AMI based on the Linux distro selected
```
vi instance.tf
```
Delete all the existing lines and Add the given code, by pressing "INSERT" and replacing `YourName`

`Note:` To delete all the lines at a time use the commands `Esc+gg+dG` and once cleared then add the new lines.
```
resource "aws_instance" "terraform_example"{
  ami = var.AMIS[var.Linux_distro]
  instance_type = var.Instance_type
  tags = {
    Name = "Variables-Lab3-YourName"
  }
}
```
Save the file using "ESCAPE + :wq!"

Now, Also make changes in the `Vars.tf` file.
```
vi vars.tf
```
Delete all existing lines and Add the given lines, by pressing "INSERT" Also ensure to replace your `Region,` `AMi IDs` of the same region for `redhat,` `ubuntu` and `amazon`

`Note:` To delete all the lines at a time use `Esc+gg+dG`
```
variable "Instance_type"{
  description = "Instance type for the EC2 Instance"
  default = "t2.micro"
}

variable "AWS_REGION"{
  default = "us-east-2"
}

variable "Linux_distro"{
  #description = "Please Enter the Linux distro (redhat, ubuntu, amazon)"
  default = "amazon"
  }

variable "AMIS"{
  type=map(string)
  default={
   redhat="ami-0d77c9d87c7e619f9"
   ubuntu="ami-09040d770ffe2224f"
   amazon="ami-0ddda618e961f2270"
  }
}
```
Save the file using "ESCAPE + :wq!"
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
terraform plan -var 'Linux_distro=redhat' -out myplan
```
```
terraform apply myplan
```
Now create `terraform.tfvars,` file to pass the variable values in it, and  see the precedance
```
vi terraform.tfvars 
```
Add the given lines, by pressing "INSERT" Also replace them with your `AccessKey` and `Secret Access Keys` that you created and downloaded earlier.
```
Linux_distro = "ubuntu"

Instance_type = "t2.large"
```
Save the file using "ESCAPE + :wq!"

```
terraform fmt
```
 ```
terraform apply
```

Use the `terraform destroy` command to clean the infrastructure used in this lab
```
terraform destroy
```
Once Done remove the `variables-lab` Directory.
```
cd ~
rm -rf variables-lab

```

