## Creating AWS resources using terraform modules
```
cd /home/ubuntu/
```
```
sudo apt install tree -y
```
```
wget https://s3.ap-south-1.amazonaws.com/files.cloudthat.training/devops/terraform-essentials/terraform-modules.tar.gz
```
```
tar -xvf terraform-modules.tar.gz
```
```
cd terraform-modules
```
```
tree
```
Cat all files to see the module structure
```
vi main.tf
```
Add the below code after block `module "my_security_group"`
```
output "secgrpid" {
  description = "Newly created sec grp"
  value       = module.my_security_group.sgid
}
```
```
cat provider.tf
```
**Note:** No change needed in `provider.tf`
```
vi variables.tf 
```
**Note:** Replace the `Region` Default `VPC ID,` `AMI Id` and `Subnet ID` from your Allocated region in `variable.tf` file.
* `Change vpc_id` to default VPC in your region (**Ex:** vpc-0e608033e14b01c3c)
* `Change subnet id` Use any available subnets from AZ `a or b`. (**Ex:** subnet-086dd80df2e64b56b)

Then, Save it

Now, Create a key pair. The same public key will be used in the new EC2 Instance.
```
ssh-keygen -f mykey
```
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
terraform apply -auto-approve
```
**Note:**
* If it is showing any `Error` for `Security group / KeyPair`, It means that they are already existing, Rename it in `variable.tf` file or delete the Keypair/Security Group in the Console.

Once the resources are created. Then, verify all the resources and then destroy them.
```
terraform destroy
```
Once Destroyed, remove the Directory and Zip FIle.
```
cd ~
rm -rf terraform-modules
```
```
rm -rf terraform-modules.tar.gz
```
