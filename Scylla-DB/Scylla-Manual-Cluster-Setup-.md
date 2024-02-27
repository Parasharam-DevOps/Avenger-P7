# Manual Setup of ScyllaDb

![logo-scylla-vertical-RGB](https://github.com/avengers-p7/Documentation/assets/156056709/a8f9319d-2109-4d3a-b8c9-07fd1f08460b)


| **Author** | **Created On** | **Last Updated** | **Document Version** |
| ---------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 13-02-2024 | 13-02-2024 | V1 |

---

# Table of Contents

1. [Introduction](#introduction)
2. [System Requirements](#system-requirements)
3. [Runtime Prerequisites](#runtime-prerequisites)
4. [ScyllaDB Installation Guide](#scylladb-installation-guide)
5. [Configure and Run ScyllaDB](#configure-and-run-scylladb)
    - [Running the scylla_setup Script](#running-the-scylla_setup-script)
    - [Configure ScyllaDB Settings](#configure-scylladb-settings)
6. [Cluster Setup](#cluster-setup)
    - [Prerequisites](#prerequisites)
    - [Node Configuration](#node-configuration)
    - [Cluster Initialization](#cluster-initialization)
    - [Additional Information](#Additional-Information)
7. [Conclusion](#conclusion)
8. [References](#references)

---

# Introduction

Scylla is an open-source NoSQL database that is compatible with Apache Cassandra, but it provides faster performance and lower latency. Scylla is based on the C++ programming language. Scylla is also designed to be scalable, fault-tolerant, and highly available.
The ScyllaDB Manual Setup Guide provides step-by-step instructions for installing, configuring, and setting up ScyllaDB on your system. This guide is intended to help users seamlessly deploy and manage ScyllaDB, a highly performant NoSQL database.

# System Requirements

|   System Requirement              |             Minimum                     |
|-----------------------------------|-----------------------------------------|
| Processor/Instance Type           |         Dual-Core/t2.medium             | 
| RAM                               |            4 Gigabytes            |
| Disk Space                        |              16 GB                      |
| OS Required (Linux Distributions) | Ubuntu 20.04 LTS, Debian, or CentOS 7/8 |

# Runtime Prerequisites

|          Tool            |                Version     | 
| ------------------------ |----------------------------|
|         JDK-17           | ScyllaDB need JDK-11 or later verison.|

# Ports

| Ports         | Description                                                                                | 
| ------------- |--------------------------------------------------------------------------------------------|
| 22            | Port 22 is used to establish an SSH connection to an EC2 instance and access a shell       |
| 443           | It is a standard port for secure communication over the internet between client and server |
| 7199          | Port for ScyllaDB                                                                          |


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

**Configuration Setup**

Refer to ScyllaDB Configuration Guide for detailed setup instructions.[ScyllaDB Configuration Guide](https://www.scylladb.com/download/?platform=ubuntu-22.04&version=scylla-5.2#open-source) 

---

# Configure and Run ScyllaDB

**Running the scylla_setup Script**

This script tunes system settings and determines optimal configurations.

To set up Scylla, execute the following command in your terminal:

    sudo scylla_setup
    sudo systemctl start scylla-server

**Note:**

After the installation of Scylla, it is crucial to run the scylla_setup script. This script provides essential configuration options and displays information about your Scylla installation.

Upon running the script, you may encounter a prompt with a question, such as:

![image](https://github.com/avengers-p7/Documentation/assets/156056709/9f9b14d4-ee03-49bb-8c6b-643125baaed9)


**Run ScyllaDB as a service**

    sudo systemctl start scylla-server

# Configure ScyllaDB Settings

**Edit ScyllaDB configuration file**

    sudo vim /etc/scylla/scylla.yaml

**Update the following parameters**

Update the following parameters:
According to your requirements you can the following parameters.

        listen_address: <ip>
        rpc_address: <ip>
        broadcast_rpc_address: <ip> 
        api_address: <ip>

**listen_address: localhost**

* This is the IP address that Scylla will use to connect to other Scylla nodes in the cluster. In this case, it's set to 'localhost,' indicating that it will listen for connections on the local machine.

**rpc_address: localhost**

* This is the IP address of the interface for client connections, such as Thrift and CQL. Similar to listen_address, it is set to 'localhost' in this configuration.

**broadcast_rpc_address**

* This setting specifies the IP address that Scylla should advertise to other nodes in the cluster for the purpose of client connections. It's typically set to the public IP address of the node so that other nodes can reach it.

**api_address**

* This setting allows Scylla to listen on all available network interfaces for the REST API.
	
     seeds: "172.31.22.109"
     listen_address: "172.31.22.109"
     rpc_address: "172.31.22.109"
 
**Restart ScyllaDB as a service**

    sudo systemctl restart scylla-server
# Cluster Setup

**Prerequisites**

* Ensure that all necessary ports are open. (default port 7199)

* Obtain the IP addresses of all nodes created for the cluster.

* Choose a unique name as cluster_name for all nodes.

**Node Configuration**

* Install Scylla on each node

1. In the scylla.yaml file (located at /etc/scylla/):

  * Set cluster_name to the chosen cluster name.

  * Set seeds to the IP of the first node (only the first node).

  * Configure listen_address, rpc_address, and endpoint_snitch.

2. Using GossipingPropertyFileSnitch, edit the cassandra-rackdc.properties file (located at /etc/scylla/):

  * Set dc to the datacenter name.

  * Set rack to the rack name.

Example (cassandra-rackdc.properties):

      dc=thedatacentername
      rack=therackname
      
# Cluster Initialization

3. After Scylla installation and configuration, edit the scylla.yaml file on all nodes, using the first node as the seed node.

4. Start the seed node:

	      sudo systemctl start scylla-server
   
5. Wait until the seed node is in the 'UN' (Up/Normal) state.

6. Repeat the process for the other nodes, starting each after the previous one is in the 'UN' state.

7. Verify node addition using the nodetool status command.

**Additional Notes**

If using Scylla version earlier than Scylla Open Source 4.3 or Scylla Enterprise 2021.1, update the seeds parameter in each node’s scylla.yaml file to include the IP of at least one more seed node. Refer to the "Older Version Of Scylla" documentation for details.

**Example**
**GossipingPropertyFileSnitch**

Use the GossipingPropertyFileSnitch when working with multi-cluster deployments where the nodes are in various datacenters. It is recommended to use the GossipingPropertyFileSnitch in production installations. This snitch allows ScyllaDB to explicitly define which DC and rack a specific node belongs to. In addition, it reads its configuration from the cassandra-rackdc.properties file, which is located in the /etc/scylla/ directory.

This example demonstrates the installation and configuration of a three-node cluster using GossipingPropertyFileSnitch as the endpoint_snitch, with each node on a different rack.

      Node IPs:
      
      192.168.1.201 (seed)
      
      192.168.1.202
      
      192.168.1.203

**Node Configuration (scylla.yaml):**

      # Node 192.168.1.201
      cluster_name: 'Scylla_cluster_demo'
      seeds: "192.168.1.201"
      endpoint_snitch: GossipingPropertyFileSnitch
      rpc_address: "192.168.1.201"
      listen_address: "192.168.1.201"
      
      # Node 192.168.1.202
      cluster_name: 'Scylla_cluster_demo'
      seeds: "192.168.1.201"
      endpoint_snitch: GossipingPropertyFileSnitch
      rpc_address: "192.168.1.202"
      listen_address: "192.168.1.202"
      
      # Node 192.168.1.203
      cluster_name: 'Scylla_cluster_demo'
      seeds: "192.168.1.201"
      endpoint_snitch: GossipingPropertyFileSnitch
      rpc_address: "192.168.1.203"
      listen_address: "192.168.1.203"
      
**Node Configuration (cassandra-rackdc.properties):**

      # Node 192.168.1.201
      dc=datacenter1
      rack=rack43
      
      # Node 192.168.1.202
      dc=datacenter1
      rack=rack44
      
      # Node 192.168.1.203
      dc=datacenter1
      rack=rack45
      
**Starting Scylla Nodes**

Start Scylla nodes, beginning with the seed node (192.168.1.201). Wait until each node is in a 'UN' state before starting the next.

      sudo systemctl start scylla-server
      
**Verify Cluster Status**

Verify that the nodes have been successfully added to the cluster by using the nodetool status command.

![image](https://github.com/avengers-p7/Documentation/assets/156056709/e9ba9e1e-cd22-4390-874c-8c7d71f92513)


![image](https://github.com/avengers-p7/Documentation/assets/156056709/c15cd3c8-ea53-4e8c-ac73-0c41bda4bb78)



This comprehensive guide provides step-by-step instructions for setting up a ScyllaDB cluster in a single data center, ensuring a smooth and efficient deployment process.

# Additional Information

| ScyllaDB Users |
|----------------|
| - Comcast      |
| - Discord      |
| - Disney+      |
| - Crypto.com   |
| - OpenSea      |
| - Starbucks    |
| - Zillow       |

# Conclusion

The ScyllaDB Manual Setup Guide provides a comprehensive walkthrough for installing, configuring, and initializing ScyllaDB on Ubuntu 22.04.3 LTS Ensure to follow each step carefully to set up your ScyllaDB environment successfully.

# References

| Description                                | Source                                                                                     |
| ------------------------------------------ | ------------------------------------------------------------------------------------------ |
| Format inspiration for the document obtained from this repository. | [Documentation Template](https://github.com/OT-MICROSERVICES/documentation-template/wiki/Software-Template) |
| Comprehensive guide for installing ScyllaDB on Linux. | [ScyllaDB Installation Guide](https://opensource.docs.scylladb.com/stable/getting-started/install-scylla/install-on-linux.html) |
| Step-by-step instructions for configuring ScyllaDB. | [ScyllaDB Configuration Guide](https://www.scylladb.com/download/?platform=ubuntu-22.04&version=scylla-5.2#open-source) |
| Step-by-step Manual Cluster Guide. | [ScyllaDB Cluster Guide](https://opensource.docs.scylladb.com/stable/operating-scylla/procedures/cluster-management/create-cluster.html) |
| ScyllaDB Users | [Scylla-DB-Users](https://discovery.hgdata.com/product/scylla) |
