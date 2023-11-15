Debug variables 
grep -E "(seeds:|listen_address:|rpc_address:|endpoint_snitch:)|^seeds:" /etc/cassandra/default.conf/cassandra.yaml

sudo yum update -y
sudo yum groupinstall -y "Development Tools"
sudo yum install -y python3 python3-pip
pip3 install cqlsh
sudo yum install -y java-11-openjdk-devel

sudo tee /etc/yum.repos.d/cassandra.repo <<EOL
[cassandra]
name=Apache Cassandra Repository
baseurl=https://redhat.cassandra.apache.org/41x/
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://downloads.apache.org/cassandra/KEYS
enabled=1
EOL

sudo yum install -y cassandra-4.1.3


# Server1: Update cassandra.yaml
# SSH into Server1
ssh -i "ashish.pem" ubuntu@ec2-52-53-179-171.us-west-1.compute.amazonaws.com

# Edit cassandra.yaml
sudo vim /etc/cassandra/default.conf/cassandra.yaml

# Add configurations
listen_address: 172.31.5.42
seeds: "172.31.5.42,172.31.4.246"
rpc_address: 172.31.5.42
endpoint_snitch: RackInferringSnitch

# Update cassandra-env.sh
sudo vim /etc/cassandra/default.conf/cassandra-env.sh

# Add JVM Options
JVM_OPTS="$JVM_OPTS -Dcassandra.ignore_dc=true"
JVM_OPTS="$JVM_OPTS -Dcassandra.ignore_rack=true"

# Server2: Update cassandra.yaml
# SSH into Server2
ssh -i "ashish.pem" ubuntu@ec2-18-144-170-232.us-west-1.compute.amazonaws.com

# Edit cassandra.yaml
sudo vim /etc/cassandra/cassandra.yaml

# Add configurations
listen_address: 172.31.4.246
seeds: "172.31.5.42,172.31.4.246"
rpc_address: 172.31.4.246
endpoint_snitch: RackInferringSnitch

# Update cassandra-env.sh
sudo vim /etc/cassandra/default.conf/cassandra-env.sh

# Add JVM Options
JVM_OPTS="$JVM_OPTS -Dcassandra.ignore_dc=true"
JVM_OPTS="$JVM_OPTS -Dcassandra.ignore_rack=true"

# Post-Configuration
# Restart Cassandra on Both Servers
sudo systemctl restart cassandra

# Check Node Status
nodetool status

# Test cqlsh Connection
cqlsh 172.31.5.42
cqlsh 172.31.4.246

# Debug: Test telnet Connection to Cassandra nodes
telnet 172.31.5.42 9042
telnet 172.31.4.246 9042
