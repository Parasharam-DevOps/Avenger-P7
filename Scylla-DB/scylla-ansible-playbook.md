# Ansible Playbook to Install Scylla-DB 

![logo-scylla-vertical-RGB](https://github.com/avengers-p7/Documentation/assets/156056709/e765857b-fd7e-4478-b59c-1545e0afd131)


| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 28-02-2024 | 29-02-2024 | V1 |

***

# Table of Contents

1. [Introduction](#introduction)
2. [Pre-requisites](#pre-requisites)
3. [Flow Diagram](#flow-diagram)
4. [Steps](#steps)
5. [Evaluate Output](#evaluate-output)
6. [Conclusion](#conclusion)
7. [Contact Information](#contact-information)
8. [Resources and References](#resources-and-references)


   
***
# Introduction 

This document aims to provide a guide for setting up ScyllaDB in a development environment using Ansible automation on AWS. We are
going to Setup a single Node server of Scylladb using dynamic inventory.

***
# Pre-requisites 

| Tool         | Description                                       |
| ------------ | ------------------------------------------------- |
| Ansible      | Version 2.15.5 or later. Used for Ansible roles. |
| AWS Account  | Access to an AWS account for deployment.         |
| Private key  | Required for SSH authentication.                 |

Please ensure you have access to an AWS account for deployment purposes in addition to Ansible and a private key for SSH authentication.

***
# Flow Diagram:
![image](https://github.com/avengers-p7/Documentation/assets/156056709/9e6a4ced-3182-40a9-b772-2ac7021a436c)


***
# Steps

Before going further check the link for Ansible Role  **[Repository-Link](https://github.com/Parasharam-Desai/scylla-ansible-role.git)** 

**Step 1: Dynamic Inventory Setup**(`ansible.cfg`)

Defines inventory settings, and SSH configurations.

```ini
[defaults]
inventory               =       /home/parsu/ansible/aws_ec2.yaml
private_key_file        =       /home/parsu/Downloads/snaatak.pem
remote_user             =       ubuntu
host_key_checking       =       False

[inventory]
enable_plugins          =       aws_ec2
```
**Explanation:**

- `inventory`: Specifies the path to the AWS EC2 inventory file providing details about available hosts.
- `host_key_checking`: Turns off host key checking for simplicity.
- `remote_user`: Sets the remote user for SSH connections to 'ubuntu'.
- `private_key_file`: Specifies the location of the private key file for authentication.
  
> [!NOTE]
>Ensure that for dynamic inventory you have the necessary AWS credentials configured in AWS CLI and attach an IAM role on the master node.

**Step 2:  AWS EC2 Inventory** (`aws_ec2.yml`)


```yaml
---
plugin: aws_ec2
regions:
  - eu-west-3
  
filters:
  instance-state-code: 16

keyed_groups:
  - key: tags
    prefix: tag
```
## Usage

To use this configuration:

1. Make sure you have Ansible installed.
2. Copy the `aws_ec2.yml` configuration file into your Ansible project directory.
3. Configure dynamic inventory in your Ansible server to use the AWS EC2 plugin.
4. Use the configuration with the `ansible-playbook` command, specifying the path to the configuration file.

**Setting up Dynamic Inventory with Ansible and AWS**

To learn how to set up dynamic inventory for Ansible with AWS, please refer to the following documentation: [Blog-Link](https://devopscube.com/setup-ansible-aws-dynamic-inventory/)

**Step 3: Create Ansible Playbook**
Use the provided playbook template.

```bash


##--------------- Ansible Playbook For Install Scylla-DB ---------------##

---
- hosts: tag_Name_scylla
  become: yes
  gather_facts: yes
  vars:
    keyring_path : /etc/apt/keyrings
    cassandra_directory : /etc/scylla/cassandra
    scylla_repo_key_url: "gpg --homedir /tmp --no-default-keyring --keyring /etc/apt/keyrings/scylladb.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys d0a112e067426ab2"
    scylla_repo_url: http://downloads.scylladb.com/deb/debian/scylla-5.4.list
    scylla_repo_dest: "/etc/apt/sources.list.d/scylla.list"

  tasks:
    - name: Update Apt Cache
      apt:
        update_cache: yes

    - name: Create directory for cassandra and keyrings
      file:
        path: "{{ item }}"
        state: directory
        mode: "0777"
      loop:
        - "{{ keyring_path }}"
        - "{{ cassandra_directory }}"

    - name: Install Java
      apt:
        name: "{{ java_apt_package }}"
        state: present
    - name: Import ScyllaDB GPG Key
      become: true
      raw: "{{ scylla_repo_key_url }}"

    - name: Add ScyllaDB Repository
      get_url:
        url: "{{ scylla_repo_url }}"
        dest: "{{ scylla_repo_dest }}"

    - name: Update Apt Cache
      apt:
        update_cache: yes

    - name: Install Scylla
      apt:
        name: scylla
        state: present
      failed_when: false

    - name: Run Scylla
      command: scylla_setup
      args:
        stdin: "YES\nYES\nYES\nYES\nYES\nYES\nYES\nYES\nyes\nYES\nyes\nYES\nyes\nYES\nyes\nYES\nYES\nYES\nYES\nYES\nYES\nYES\nyes"
      register: scylla_setup_output
      failed_when: false

    - name: Debug Scylla setup output
      debug:
        var: scylla_setup_output

    - name: Start and enable scylla service
      systemd:
        name: scylla-server
        state: started
        enabled: yes

    - name: See Nodetool Status
      command: "nodetool status"
      register: status

    - name: Debug Nodetool status
      debug:
        var: status

```

**Step 4: Playbook Execution**

* To Install ScyllaDB on your target servers, you will execute the Ansible playbook using the following command:

```bash
ansible-playbook scylla-playbook.yml
```
***
# Evaluate Output

During output evaluation, utilize the register and debug modules to verify the playbook's functionality.


***
# Conclusion

* This guide demonstrates how to automate the setup of ScyllaDB in a development environment using Ansible. By following these steps, you can efficiently install ScyllaDB on your AWS infrastructure.

***
# Contact Information 

| Name | Email Address |
| ---- | -------------- |
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

***

# Resources and References 

| Description | Source |
| ---- | -------------- |
| Setting up Ansible AWS Dynamic Inventory | [Link](https://devopscube.com/setup-ansible-aws-dynamic-inventory/) |
| ScyllaDB-Manual Setup | [Link](https://github.com/avengers-p7/Documentation/tree/main/OT%20Micro%20Services/Software/ScyllaDB) |
| ScyllaDB Installation Guide | [Link](https://opensource.docs.scylladb.com/stable/getting-started/install-scylla/install-on-linux.html) |
| ScyllaDB Configuration Guide | [Link](https://www.scylladb.com/download/?platform=ubuntu-22.04&version=scylla-5.2#open-source) |
| Documentation Template | [Link](https://github.com/OT-MICROSERVICES/documentation-template/wiki/Software-Template) |
| YAMLLint | [Link](https://www.yamllint.com/) |
