**Install Scylla-DB On Debian/Ubuntu**

1.Install a repo file and add the ScyllaDB APT repository to your system.

    sudo mkdir -p /etc/apt/keyrings
    
    sudo gpg --homedir /tmp --no-default-keyring --keyring /etc/apt/keyrings/scylladb.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys d0a112e067426ab2
    
    sudo wget -O /etc/apt/sources.list.d/scylla.list http://downloads.scylladb.com/deb/debian/scylla-5.4.list


2.Install ScyllaDB packages

    sudo apt-get update
    
    sudo apt-get install -y scylla
