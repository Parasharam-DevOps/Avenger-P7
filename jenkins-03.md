Assignment 3:
Topics Covered:  (Configuring Agents, Various Methods, Distributing Loads, Executors, Assigning Nodes)
     Assignment on configuring Nodes
        Configure a Ubuntu node using execution of command on the master method. 
        - Make sure at any point of time maximum 5 jobs can be executed on this node.
        - Assign this node to Assignment 2: Part 1 
        Configure a RHEL node using  Launch slave agents via SSH method. 
        - Make sure at any point of time maximum 2 jobs can be executed on this node.
        - Assign this node to Assignment 2: Part 2
        Configure a CentOS node using Launch slave agents via SSH method. 
        - Make sure at any point of time maximum 3 jobs can be executed on this node.
        - Assign this node to Assignment 3
        Configure a Windows node using method of your choice
        - Download one sample application of .NET and build it on Windows Node.


## Set-up Ubuntu Node

su - jenkins and copy the id_rsa.pub ssh key of into user in ubuntu authorized keys 

Download this file and create workspace folder and install java for Command line connection

sudo apt install openjdk-11-jre

mkdir /home/ubuntu/workspace/

take public ip of node server then paste master public key in ubuntu server

sudo wget http://18.144.27.234:8080/jnlpJars/slave.jar This public Ip is jenkins master server not a ubuntu server 


#### Configuration

![image](https://github.com/parsugit/ansible_practice/assets/132131379/f0764bee-8ac2-4466-9f83-b6d9c3f2b0e1)

##Connection Status

![image](https://github.com/parsugit/ansible_practice/assets/132131379/bf0d7a9d-2eba-4140-8cdf-419efa089376)


#### Assign A-02 Part-A

![image](https://github.com/parsugit/ansible_practice/assets/132131379/a5416b96-ef0c-4a12-8fcf-245f1fae69f6)

## Execution Part Output
![image](https://github.com/parsugit/ansible_practice/assets/132131379/c34db0d1-0188-4875-8f7d-825197bc1668)





## Set-up RHEL Node

Method - via ssh

create workspace folder

sudo yum install java-11-openjdk-devel

mkdir /home/ubuntu/workspace/

#### Configuration 

![image](https://github.com/parsugit/ansible_practice/assets/132131379/1f2a2cf0-b250-4f99-b531-fb96db4f74bc)

##Connection Status

![image](https://github.com/parsugit/ansible_practice/assets/132131379/befc296a-18f3-4452-8314-35370afa16bd)



#### Assign A-02 Part-B

![image](https://github.com/parsugit/ansible_practice/assets/132131379/07b0a249-0eb4-4472-a228-de6337e49105)

## Execution Part Output

![image](https://github.com/parsugit/ansible_practice/assets/132131379/4d435e32-f2a2-4601-947e-aa2639e20534)
