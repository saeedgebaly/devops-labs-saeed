# Lab 3 – Structured Configuration Management with Ansible Roles

## Objective
Automate the installation and configuration of **Docker**, **Kubernetes CLI (kubectl)**, and **Jenkins** using **Ansible Roles**.

---

## Project Structure

ansible-lab/
├── inventory
├── playbook.yml
└── roles/
├── docker/
│ └── tasks/main.yml
├── kubectl/
│ └── tasks/main.yml
└── jenkins/
└── tasks/main.yml



Each role is responsible for installing and configuring one tool:
- `docker` → Installs and enables Docker.
- `kubectl` → Installs Kubernetes CLI.
- `jenkins` → Installs and starts Jenkins service.

---

##  How It Works

###Inventory File
Defines the managed node(s):
```ini
[centos-node]
192.168.204.130 ansible_user=saeed


###Playbook File (playbook.yml)
- hosts: centos-node
  become: yes
  roles:
    - docker
    - kubectl
    - jenkins

---
##  How to Run
gih repo clone saeedgebaly/devops-labs-saeed/lab3-roles.git
cd devops-labs-saeed/lab3-roles

-----
## Verification
-Docker
docker --version
systemctl status docker

-Kubctl
kubectl version --client

-Jenkins
systemctl status jenkins

Then open Jenkins in your browser:
http://<managed-node-IP>:8080

------
## Notes

Ensure SSH connectivity between controller (Ubuntu) and managed node (CentOS).

Use --ask-become-pass if sudo password is required.

For CentOS, Jenkins requires Java 17 (Temurin JDK).

Firewall on CentOS must allow port 8080 for Jenkins access:

sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload

