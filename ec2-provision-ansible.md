# Summary

1. Create AWS user (IAM)
2. Install ansible/EC2 dependencies
3. Write ansible code
4. Run ansible to provision


## 1. Create AWS user

https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console

## 2. Install Dependencies

### local software

```sh
sudo apt install python
sudo apt install python-pip
pip install boto boto3 ansible
```

### keys

```sh
ssh-keygen -t rsa -b 4096 -f ~/.ssh/my_aws
```

## 3. Create code

### File structure

```sh
mkdir -p AWS_Ansible/group_vars/all/
cd AWS_Ansible
touch playbook.yml
```

### Make ansible vault to store access/secret keys

```sh
ansible-vault create group_vars/all/pass.yml
New Vault password:
Confirm New Vault password:

# hash password file 
openssl rand -base64 2048 > vault.pass
ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
```

### 

ansible-playbook ec2-creation-playbook-test.yaml --ask-vault-pass --tags create_ec2 --vault-password-file vault.pass

ansible-playbook ec2-creation-playbook-test.yaml --tags create_ec2 --vault-password-file vault.pass

sudo ansible-vault edit group_vars/all/pass.yml --vault-password-file vault.pass

ansible-playbook ec2-module-testing.yaml --vault-password-file vault.pass

aws ec2 describe-images --region us-west-2 --image-ids ami-09975e5a942d87be0

ami-09fe2be72ca884906

aws ec2 describe-images --region ap-southeast-2 --image-ids ami-09fe2be72ca884906

aws ec2 describe-instance-types --filters Name=processor-info.supported-architecture,Values=arm64 --query "InstanceTypes[*].InstanceType" --output text

https://cloud-images.ubuntu.com/locator/ec2/

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html

https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_instance_module.html

https://aws.amazon.com/ec2/pricing/on-demand/

ssh ec2-user@3.25.130.108 -vvv

ssh -i ~/.ssh/my_aws ubuntu@ec2-18-218-148-27.us-east-2.compute.amazonaws.com

ssh -i ~/.ssh/my_aws ec2-user@ec2-3-25-130-108.ap-southeast-2.compute.amazonaws.com -vvv

ssh -i ~/.ssh/my_aws ec2-3-25-130-108.ap-southeast-2.compute.amazonaws.com -vvv

3.106.171.92
3.25.130.108

ssh-keygen -f my_aws.pub -m 'PEM' -e > my_aws.pub.pem

ssh -i ~/.ssh/my_aws.pub.pem ec2-user@ec2-3-25-130-108.ap-southeast-2.compute.amazonaws.com -vvv

chmod 400 my_aws

ssh -i "my_aws" ec2-user@ec2-52-65-63-49.ap-southeast-2.compute.amazonaws.com