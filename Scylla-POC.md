**Install Scylla-DB On Debian/Ubuntu**

1.Install a repo file and add the ScyllaDB APT repository to your system.

    sudo mkdir -p /etc/apt/keyrings
    
    sudo gpg --homedir /tmp --no-default-keyring --keyring /etc/apt/keyrings/scylladb.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys d0a112e067426ab2
    
    sudo wget -O /etc/apt/sources.list.d/scylla.list http://downloads.scylladb.com/deb/debian/scylla-5.4.list


2.Install ScyllaDB packages

    sudo apt-get update
    
    sudo apt-get install -y scylla
    
3.Configure and Run ScyllaDB

1.Configure the following parameters in the /etc/scylla/scylla.yaml configuration file.

    seeds - The IP address of the first node. Other nodes will use it as the first contact point to discover the cluster topology when joining the cluster.

    listen_address - The IP address that ScyllaDB uses to connect to other nodes in the cluster.

    rpc_address - The IP address of the interface for client connections (Thrift, CQL).

2.Run the scylla_setup script to tune the system settings and determine the optimal configuration.

    sudo scylla_setup

The script invokes a set of scripts to configure several operating system settings; for example, it sets RAID0 and XFS filesystem.

The script runs a short (up to a few minutes) benchmark on your storage and generates the /etc/scylla.d/io.conf configuration file. When the file is ready, you can start ScyllaDB. ScyllaDB will not run without XFS or io.conf file

3.Run ScyllaDB as a service (if not already running)

    sudo systemctl start scylla-server

Now you can start using ScyllaDB. Here are some tools you may find useful.

Run nodetool:

The Blog I Refered : https://opensource.docs.scylladb.com/stable/getting-started/install-scylla/install-on-linux.html

    nodetool status

Run cqlsh:

    cqlsh

Getting Started

1.Creating a Keyspace & Table In Scylla

    CREATE KEYSPACE IF NOT EXISTS employee_db
      WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
      
2.To see keyspace run the below command

    DESCRIBE KEYSPACES;

  
3.Create table under the employee_db KEYSPACE

     CREATE TABLE IF NOT EXISTS employee_info (
        id text, name text, designation text, department text,
        joining_date date, address text, office_location text,
        status text, email text, phone_number text,
        PRIMARY KEY (id, joining_date)
    ) WITH CLUSTERING ORDER BY (joining_date DESC);
  
2.To see table run the below command

    DESCRIBE TABLES;
    
