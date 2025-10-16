# Lab 5 – Ansible Dynamic Inventory with AWS EC2

##  Overview
This lab demonstrates how to use **Ansible Dynamic Inventory** with AWS EC2 instances using the `amazon.aws.ec2` plugin.

##  Setup Steps

## 1. Install and Activate Virtual Environment
```bash
python3 -m venv ansible-env
source ansible-env/bin/activate
pip install ansible boto3 botocore

## 2. Install Required Collections
ansible-galaxy collection install amazon.aws

## 3. Configure Dynamic Inventory
file: "aws_ec2.yml"
-
plugin: amazon.aws.ec2
regions:
  - us-east-1
filters:
  tag:ivolve: true
keyed_groups:
  - key: tags.ivolve
    prefix: tag
hostnames:
  - public_dns_name

## 4. Test the Inventory
ansible-inventory -i aws_ec2.yml --graph

## 5. Test Connection to EC2
ansible all -i aws_ec2.yml -m ping

- Expected output:
ec2-xx-xx-xx-xx.compute-1.amazonaws.com | SUCCESS => {
    "ping": "pong"
}

## 6. Example Command
ansible -i aws_ec2.yml tag_true -m shell -a "hostname"

# Files

aws_ec2.yml → Dynamic inventory config
ansible.cfg → Basic Ansible configuration
requirements.yml → Optional dependency list

# Notes

Make sure your AWS credentials are configured using aws configure.
Ensure your SSH key has correct permissions (chmod 400 <key>.pem).
