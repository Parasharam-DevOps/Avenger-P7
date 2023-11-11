Debug variables 
grep -E "(seeds:|listen_address:|rpc_address:|endpoint_snitch:)|^seeds:" /etc/cassandra/cassandra.yaml

# Server1: Update cassandra.yaml
# SSH into Server1
ssh -i "ashish.pem" ubuntu@ec2-52-53-179-171.us-west-1.compute.amazonaws.com

# Edit cassandra.yaml
sudo vim /etc/cassandra/cassandra.yaml

# Add configurations
listen_address: 172.31.5.42
seeds: "172.31.5.42,172.31.4.246"
rpc_address: 172.31.5.42
endpoint_snitch: RackInferringSnitch

# Update cassandra-env.sh
sudo vim /etc/cassandra/cassandra-env.sh

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
sudo vim /etc/cassandra/cassandra-env.sh

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
