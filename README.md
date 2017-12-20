# A template for creating sets of the EC2 instances web and app with nginx in load balancer mode

## Usage:

### Preliminary preparation

#### prepare local environment
```
virtualenv .venv && source .venv/bin/activate
pip install -r requirementes.txt
```
#### make file ~/.boto with AWS credentials:
```
[profile test]
aws_access_key_id=key
aws_secret_access_key=secret
```
#### make file ~/.aws/credential with AWS credentials:
```
[default]
aws_access_key_id=key
aws_secret_access_key=secret
```
#### fill in the variable file inventory/vars/vars_instances.yml substituting your values:
```
aws_profile: "test"
aws_key_name: "aws_key_name"
private_key_file: "/path/to/your_aws_key.pem"
aws_security_group: "aws_security_group"
aws_instance_type: "aws_instance_type" #for free t.micro
aws_ami: "aws_ami"
region: "region" #for example us-west-2
application: "app"
application2: "web"
app01_hostname: "app-01"
app02_hostname: "app-02"
app03_hostname: "app-03"
app04_hostname: "app-04"
web_hostname: "{{ ansible_hostname }}"
web_count: 1
app_count: 1
vpc_subnet_a: "subnet-xxxxxxxx"
vpc_subnet_b: "subnet-xxxxxxxx"
vpc_subnet_c: "subnet-xxxxxxxx"
```


### Creation

#### Run playbook (in verbose mode):
```
ansible-playbook -i inventory/ec2.py instances.yml -e @inventory/vars/vars_instances.yml -vvv 
```
