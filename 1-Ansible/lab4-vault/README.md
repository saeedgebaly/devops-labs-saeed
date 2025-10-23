# Lab 4 - Securing Sensitive Data with Ansible Vault 

##  Objective
Automate the installation and configuration of MySQL while securing sensitive credentials using **Ansible Vault**.

---

##  Tasks Overview
1. Install MySQL on the managed node.
2. Create a new database named **iVolve**.
3. Create a MySQL user with full privileges on the iVolve database.
4. Secure the database credentials using **Ansible Vault**.
5. Validate the setup by connecting to the database and listing available databases.


---

## Using Ansible Vault

### 1. Encrypt sensitive variables:
```bash
ansible-vault create group_vars/all/vault.yml

#Then add:
vault_mysql_root_password: your_root_password
vault_mysql_user_password: your_user_password

#To edit later:
ansible-vault edit group_vars/all/vault.yml


#Running the Playbook
ansible-playbook -i inventory playbook.yml --ask-vault-pass --ask-become-pass

#At the end of the playbook, the validation task should display:
Database
information_schema
ivolve
performance_schema

