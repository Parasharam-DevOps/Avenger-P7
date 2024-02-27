# ScyllaDb Documentation


|   Author     |  Created on   |  Version   | Last updated by | Last edited on |
| ------------ | --------------| -----------|---------------- | -------------- |
| Vikram BISHT | 10 Jan 2024   |     v1     | Vikram Bisht    | 19 Jan 2024  |

---
# Table of Contents 
+ [Introduction](#introduction)
+ [Key Features](#Key-Features)
+ [Licensing & Versoning](#Licensing-&-Versoning)
+ [System Requirements](#System-Requirements)
+ [Ports](#Ports)
+ [Runtime Prerequisites](#Runtime-Prerequisites)
+ [ScyllaDB Installation Guide](#ScyllaDB-Installation-Guide)
+ [Configure and Run ScyllaDB](#Configure-and-Run-ScyllaDB)
+ [Conclusion](#Conclusion)
+ [References](#References)
***
# Introduction

ScyllaDB is a high-performance, distributed NoSQL database designed for horizontal scalability and low-latency operations. It was developed as an open-source alternative to Apache Cassandra, but with a focus on improved performance and efficiency. ScyllaDB is written in C++ and is optimized for modern hardware architectures. The database is designed to handle large volumes of data and high-throughput workloads, making it well-suited for applications with demanding performance requirements.

## Key Features

|       Features     |             Description                     |
|--------------------|-----------------------------------------|
| **Scalability:**   |  Easily handle large amounts of data and growing workloads by scaling horizontally.                  | 
| **Flexibility:**   |  Adapt to diverse application needs with a NoSQL database model, offering flexibility in data modeling.          |
| **Performance:**   |  Achieve superior throughput and low-latency performance, making ScyllaDB ideal for high-performance applications. |
| **Fault Tolerance:**   | Ensure high availability and fault tolerance with a distributed architecture that distributes data across multiple nodes. |
| **Elasticity**     | ScyllaDB supports dynamic scaling, allowing you to add or remove nodes from the cluster without downtime.   |

This  Guide gives brief overview about scylladb & provides step-by-step instructions for installing, configuring, and setting up ScyllaDB on your system. This guide is intended to help users seamlessly deploy and manage ScyllaDB, a highly performant NoSQL database.

---

# Licensing

| License Type                         | Description                                   | Commercial Use | Open Source |
| ------------------------------------ | --------------------------------------------- | --------------- |------------- |
| Affero General Public License (AGPL) | Free and open for public use and modification | Yes             | Yes         |

---

# Software Version

|   Software   |  Version   |
| ------------ | -----------|
|     ScyllaDB |    5.4.1   |

---

# System Requirements

|   System Requirement              |             Minimum                     |
|-----------------------------------|-----------------------------------------|
| Processor/Instance Type           |         Dual-Core/t2.medium             | 
| RAM                               |            4 Gigabytes            |
| Disk Space                        |              16 GB                      |
| OS Required (Linux Distributions) | Ubuntu 20.04 LTS, Debian, or CentOS 7/8 |

---

# Ports

| Ports         | Description                                                                                | 
| ------------- |--------------------------------------------------------------------------------------------|
| 22            | Port 22 is used to establish an SSH connection to an EC2 instance and access a shell       |
| 443           | It is a standard port for secure communication over the internet between client and server |
| 9042          | Port for ScyllaDB                                                                          |

---

# Runtime Prerequisites

|          Tool            |                Version     | 
| ------------------------ |----------------------------|
|         JDK-17           | ScyllaDB need JDK-11 or later verison.|

# Architecture  
Here is a snippet view showcasing the use of scylla-db in OT-Microservices.

![image](https://github.com/Parasharam-DevOps/Avenger-P7/assets/132131379/57b0df34-d415-4c50-abc2-240add12e423)


---

# ScyllaDB Installation Guide
### Update Packages

    sudo apt update
    
### Install OpenJDK 17

**OpenJDK for ScyllaDB because ScyllaDB relies on Java for its client-side functionality**

    sudo apt install openjdk-17-jre -y

### Add ScyllaDB APT repository to your system

**Create a directory for APT keyrings**

    sudo mkdir -p /etc/apt/keyrings

**Import ScyllaDB GPG key**

    sudo gpg --homedir /tmp --no-default-keyring --keyring /etc/apt/keyrings/scylladb.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys d0a112e067426ab2

**Download ScyllaDB APT repository configuration file**

    sudo wget -O /etc/apt/sources.list.d/scylla.list http://downloads.scylladb.com/deb/debian/scylla-5.4.list

### Install ScyllaDB packages

**Update the package list to ensure it has the latest information about available packages**

    sudo apt-get update

**Install ScyllaDB packages with the -y flag to automatically answer yes to prompts**

    sudo apt-get install -y scylla

### Verify Installation

    java --version
    
    scylla --version

---

# Configure and Run ScyllaDB

**Running the scylla_setup Script**

This script tunes system settings and determines optimal configurations.

To set up Scylla, execute the following command in your terminal:

    sudo scylla_setup

**Note:**

After the installation of Scylla, it is crucial to run the scylla_setup script. This script provides essential configuration options and displays information about your Scylla installation.

Upon running the script, you may encounter a prompt with a question, such as:

![image](https://github.com/avengers-p7/Documentation/assets/156056709/9f9b14d4-ee03-49bb-8c6b-643125baaed9)


**Run ScyllaDB as a service**

    sudo systemctl start scylla-server

**Edit ScyllaDB configuration file**

    sudo vim /etc/scylla/scylla.yaml

**Update the following parameters**

According to your requirements you can change the following parameters.

	seeds: <ip>
	listen_address: <ip>
	rpc_address: <ip>

**seeds :** 
This is the PRIVATE IP address that Scylla will use to connect to other Scylla nodes in the cluster. Seed nodes are used during startup to bootstrap the gossip process and join the cluster

**listen_address:** 
This is the PRIVATE IP address that Scylla will use to connect to other Scylla nodes in the cluster. In this case, it's set to 'localhost,' indicating that it will listen for connections on the local machine.

**rpc_address:**
This is the PRIVATE IP address of the interface for client connections, such as Thrift and CQL. Similar to listen_address, it is set to 'localhost' in this configuration.
	
     seeds: "172.31.22.109"
     listen_address: "172.31.22.109"
     rpc_address: "172.31.22.109"
 
**Restart ScyllaDB as a service**

    sudo systemctl restart scylla-server

# Getting Started

**Verify Node Status**

To check if your ScyllaDB Node is working fine, use the `nodetool status` command. This command provides information about the nodes in the ScyllaDB cluster:

     nodetool status

**Interact with ScyllaDB using cqlsh command:**

    cqlsh 

cqlsh: This command is used to enter the CQL shell, which is an interactive command-line utility to execute CQL commands against a ScyllaDB database. Once you enter this command, you'll be able to execute CQL queries.

**Create Keyspaces**

	CREATE KEYSPACE employee_db
	WITH REPLICATION = {
	  'class': 'SimpleStrategy',
	  'replication_factor': 1
	};
	CREATE KEYSPACE employee_salary
	WITH REPLICATION = {
	  'class': 'SimpleStrategy',
	  'replication_factor': 1
	};
 
 This CQL command creates a keyspace named employee_db in the ScyllaDB database. A keyspace in ScyllaDB is a namespace that holds tables, similar to a schema in a relational database. In this case, the keyspace is created using the SimpleStrategy replication strategy with a replication factor of 1. Adjust the replication strategy and factor based on your requirements.

**Check Keyspaces**

    DESCRIBE KEYSPACES;
    
This CQL command retrieves a list of all available keyspaces in the ScyllaDB instance. It displays information about the existing keyspaces, including their names and configurations.

**Remove Keyspace**

    DROP KEYSPACE employee_db;
    
**Default Password Login**

    cqlsh -u cassandra -p cassandra
    
This command is a variation of the cqlsh command that includes the -u and -p flags to specify the username (-u cassandra) and password (-p cassandra) for authentication when connecting to the CQL shell. It's using the default credentials cassandra for both the username and password.

These commands allow you to create, remove, and inspect keyspaces in the ScyllaDB database using CQL commands via the CQL shell (cqlsh). Always exercise caution, especially when performing actions like dropping a keyspace, as it irreversibly deletes data.

# Conclusion

The ScyllaDB Manual Setup Guide provides a comprehensive walkthrough for installing, configuring, and initializing ScyllaDB on Ubuntu 22.04.3 LTS Ensure to follow each step carefully to set up your ScyllaDB environment successfully.

# References

| Source                                                                                     | Description                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------ |
| [ScyllaDB Installation Guide](https://opensource.docs.scylladb.com/stable/getting-started/install-scylla/install-on-linux.html) | Comprehensive guide for installing ScyllaDB on Linux. |
| [ScyllaDB Configuration Guide](https://www.scylladb.com/download/?platform=ubuntu-22.04&version=scylla-5.2#open-source) | Step-by-step instructions for configuring ScyllaDB. |
| [Documentation Template](https://github.com/OT-MICROSERVICES/documentation-template/wiki/Software-Template) | Format inspiration for the document obtained from this repository. |
