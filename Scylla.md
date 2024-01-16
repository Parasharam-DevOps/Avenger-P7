# Manual Setup of ScyllaDb


|   Author     |  Created on   |  Version   | Last updated by | Last edited on |
| ------------ | --------------| -----------|---------------- | -------------- |
| Parasharam Desai | 10 Jan 2024   |     v1     | Vikram Bisht    | Vikram Bisht   |

---

# Introduction

Welcome to the ScyllaDB Installation Guide! ScyllaDB is a highly performant and scalable NoSQL database that combines the best features of Apache Cassandra with innovative optimizations, resulting in superior throughput and lower latency. Designed for high-performance applications, ScyllaDB provides seamless scalability and fault tolerance, making it an excellent choice for various use cases.

## Key Features

* **Scalability:** Easily handle large amounts of data and growing workloads by scaling horizontally.
* **Flexibility:** Adapt to diverse application needs with a NoSQL database model, offering flexibility in data modeling.
* **Performance:** Achieve superior throughput and low-latency performance, making ScyllaDB ideal for high-performance applications.
* **Fault Tolerance:** Ensure high availability and fault tolerance with a distributed architecture that distributes data across multiple nodes.

The ScyllaDB Manual Setup Guide provides step-by-step instructions for installing, configuring, and setting up ScyllaDB on your system. This guide is intended to help users seamlessly deploy and manage ScyllaDB, a highly performant NoSQL database.

---

# Licensing

| License Type                         | Description                                   | Commercial Use | Open Source |
| ------------------------------------ | --------------------------------------------- | --------------- |------------- |
| Affero General Public License (AGPL) | Free and open for public use and modification | Yes             | Yes         |

---

# Software Overview

|   Software   |  Version   |
| ------------ | -----------|
|     ScyllaDB |    5.4.1   |

---

# System Requirements

|   System Requirement              |             Minimum                     |
|-----------------------------------|-----------------------------------------|
| Processor/Instance Type           |             t2.medium                   | 
| RAM                               |      4 Gigabytes or Dual-Core           |
| Disk Space                        |              16 GB                      |
| OS Required (Linux Distributions) | Ubuntu 20.04 LTS, Debian, or CentOS 7/8 |

---

# Important Ports

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

---

# ScyllaDB Installation Guide
### Update Packages
    sudo apt update
    
### Install OpenJDK 17
OpenJDK for ScyllaDB because ScyllaDB relies on Java for its client-side functionality.

    sudo apt install openjdk-17-jre -y

###  Add ScyllaDB APT repository to your system.

###  Create a directory for APT keyrings
    sudo mkdir -p /etc/apt/keyrings

###  Import ScyllaDB GPG key
    sudo gpg --homedir /tmp --no-default-keyring --keyring /etc/apt/keyrings/scylladb.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys d0a112e067426ab2

###  Download ScyllaDB APT repository configuration file
    sudo wget -O /etc/apt/sources.list.d/scylla.list http://downloads.scylladb.com/deb/debian/scylla-5.4.list

## Install ScyllaDB packages

### Update the package list to ensure it has the latest information about available packages
    sudo apt-get update

### Install ScyllaDB packages with the -y flag to automatically answer yes to prompts
    sudo apt-get install -y scylla

### Verify Installation
    java --version
    scylla --version

---

## Configure and Run ScyllaDB
This script tunes system settings and determines optimal configurations.

### Running the scylla_setup Script
To set up Scylla, execute the following command in your terminal:

    sudo scylla_setup

#### Note:
After the installation of Scylla, it is crucial to run the scylla_setup script. This script provides essential configuration options and displays information about your Scylla installation.

Upon running the script, you may encounter a prompt with a question, such as:

![image](https://github.com/avengers-p7/Documentation/assets/156056709/9f9b14d4-ee03-49bb-8c6b-643125baaed9)


### Run ScyllaDB as a service
    sudo systemctl start scylla-server

### Configure ScyllaDB Settings
Edit the configuration file:

    sudo vim /etc/scylla/scylla.yaml

Update the following parameters:
According to your requirements you can the following parameters.

	seeds: <ip>
	listen_address: <ip>
	rpc_address: <ip>

##### seeds : 
This is the PRIVATE IP address that Scylla will use to connect to other Scylla nodes in the cluster. Seed nodes are used during startup to bootstrap the gossip process and join the cluster

##### listen_address: 
This is the PRIVATE IP address that Scylla will use to connect to other Scylla nodes in the cluster. In this case, it's set to 'localhost,' indicating that it will listen for connections on the local machine.

##### rpc_address: 
This is the PRIVATE IP address of the interface for client connections, such as Thrift and CQL. Similar to listen_address, it is set to 'localhost' in this configuration.
	
     seeds: "172.31.22.109"
     listen_address: "172.31.22.109"
     rpc_address: "172.31.22.109"
 

### Restart ScyllaDB as a service

    sudo systemctl restart scylla-server

# Getting Started

### Verify Node Status

To check if your ScyllaDB Node is working fine, use the `nodetool status` command. This command provides information about the nodes in the ScyllaDB cluster:

     nodetool status

### Interact with ScyllaDB using cqlsh command:

    cqlsh 

Enter ScyllaDB
cqlsh: This command is used to enter the CQL shell, which is an interactive command-line utility to execute CQL commands against a ScyllaDB database. Once you enter this command, you'll be able to execute CQL queries.

### Create Keyspaces

	CREATE KEYSPACE employee_db
	WITH REPLICATION = {
	  'class': 'SimpleStrategy',
	  'replication_factor': 3
	};
	CREATE KEYSPACE employee_salary
	WITH REPLICATION = {
	  'class': 'SimpleStrategy',
	  'replication_factor': 3
	};
 
 This CQL command creates a keyspace named employee_db in the ScyllaDB database. A keyspace in ScyllaDB is a namespace that holds tables, similar to a schema in a relational database. In this case, the keyspace is created using the SimpleStrategy replication strategy with a replication factor of 1. Adjust the replication strategy and factor based on your requirements.

### Check Keyspaces
    DESCRIBE KEYSPACES;
    
This CQL command retrieves a list of all available keyspaces in the ScyllaDB instance. It displays information about the existing keyspaces, including their names and configurations.
### Remove Keyspace
    DROP KEYSPACE employee_db;
    
### Default Password Login
    cqlsh -u cassandra -p cassandra
    
This command is a variation of the cqlsh command that includes the -u and -p flags to specify the username (-u cassandra) and password (-p cassandra) for authentication when connecting to the CQL shell. It's using the default credentials cassandra for both the username and password.

These commands allow you to create, remove, and inspect keyspaces in the ScyllaDB database using CQL commands via the CQL shell (cqlsh). Always exercise caution, especially when performing actions like dropping a keyspace, as it irreversibly deletes data.

# Conclusion

The ScyllaDB Manual Setup Guide provides a comprehensive walkthrough for installing, configuring, and initializing ScyllaDB on Ubuntu 22.04.3 LTS Ensure to follow each step carefully to set up your ScyllaDB environment successfully.
# References
	
|  Source                  |                Description | 
| ------------------------ |----------------------------|
| https://opensource.docs.scylladb.com/stable/getting-started/install-scylla/install-on-linux.html | ScyllaDB, Installation Guide |
|(https://www.scylladb.com/download/?platform=ubuntu-22.04&version=scylla-5.2#open-source) | ScyllaDB Configuration Guide |
| https://github.com/OT-MICROSERVICES/documentation-template/wiki/Software-Template                | Document format followed from this link     |
