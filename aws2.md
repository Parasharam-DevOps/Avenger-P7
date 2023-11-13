"""Suppose client has a new requirement of setup service in one network and setup its management in another network. Client needs a setup of nginx as a web page hosting, but he has an issue as he needs a basic cache system + who can handle the requests smoothly + manages the requests according + need a middleware layer which helps them easily debug the service issue. So he called DevOps."""

"""You understood the problem statement and told them you would create 2 networks for management and service. For the middleware problem statement we need nginx again but as a reverse proxy."""

Kindly do the following day wise setup:

Day1: 
Create 2 vpc networks with min requirements
1 public subnet (management vpc and service vpc)
1 private subnet (management vpc)
2 private subnet (service vpc)
1 database private subnet (service vpc)
1 middleware private subnet (service vpc)


**Middleware VPC**

![image](https://github.com/parsugit/ansible_practice/assets/132131379/5b9f8061-1b2c-4860-818f-2c5d2720e1a9)

**Service VPC**

![image](https://github.com/parsugit/ansible_practice/assets/132131379/1fb60519-8946-4a9b-867f-d3afdcb3ec7f)

**VPC Peering**

![image](https://github.com/parsugit/ansible_practice/assets/132131379/7e014200-4a0e-47f7-a19f-601076a66a7b)


Create in such a way that both vpc networks can communicate with each other. Then setup nginx in service vpc under private subnet and use another nginx as a reverse proxy which can forward traffic from load balancer to nginx web hosting.

**Load Balancer**
![image](https://github.com/parsugit/ansible_practice/assets/132131379/5835bc6d-a9d7-4e18-89d5-f8199badefb6)





"""Client has another concern about security of the network, as not all resources should be allowed to each resource, so kindly restrict the rest of the traffic in route tables and Nacl".

**Output**

![image](https://github.com/parsugit/ansible_practice/assets/132131379/d77a3a93-202b-4f16-af1c-02f0d2e1b2de)


Day2:
You need to manage 
route tables of both the networks in such a way that only your teammates ip addresses should be allowed to igw rest should be deny.
Also manage Nacl group in such a way that it should allow traffic on specific port ranges to subnetworks.

"""While you are doing work on instance, some how your key 🗝️ is lost somewhere or currupted, client raising this issue as p0 and ask us for recover the key or kindly setup new key so that they can login the server atleast."""

Day3:
Kindly find the possible ways through which we can login to the server , you can do this 
Either by volume mounting
Either by doing configuration changes through user data.
Or by creating your own server key as temporary key to login there.

Kindly perform all three one by one and analyse the result.

NOTE: 
All traffic should be blocked only specific ports and IP addresses should be allowed.
No secret and access keys, only roles and policy
No root login. 

GOOD TO DO: 
If above part is done then only perform this scenario. CloudFront can cache objects and serve them directly to users (viewers), reducing the load on your Application Load Balancer. CloudFront can also help to reduce latency and even absorb some distributed denial of service (DDoS) attacks. So if you need these benefits with less load on LB and basic ddos protection kindly attach cloudfront network in front of load balancer on http traffic forwarding.
























+------------------------------------+
|          Management VPC            |
|                                    |
|  +--------------------------+      |
|  | Public Subnet (10.0.0.0/24)|      |
|  |   - Security Group (SG1)  |      |
|  |      - Allow SSH (22)      |      |
|  +--------------------------+      |
|  +--------------------------+      |
|  | Private Subnet (10.0.1.0/24)|     |
|  |   - Security Group (SG2)  |      |
|  |      - Deny All Traffic   |      |
|  +--------------------------+      |
+------------------------------------+
                 |
                 |
                 V
+------------------------------------+
|           Service VPC              |
|                                    |
|  +--------------------------+      |
|  | Public Subnet (10.1.0.0/24)|      |
|  |   - Security Group (SG3)  |      |
|  |      - Allow HTTP (80)     |      |
|  +--------------------------+      |
|  +--------------------------+      |
|  | Private Subnet 1 (10.1.1.0/24)|   |
|  |   - Security Group (SG4)  |      |
|  |      - Allow Traffic from SG3|  |
|  +--------------------------+      |
|  +--------------------------+      |
|  | Private Subnet 2 (10.1.2.0/24)|   |
|  |   - Security Group (SG5)  |      |
|  |      - Allow Traffic from SG3|  |
|  +--------------------------+      |
|  +--------------------------+      |
|  | Database Subnet (10.1.3.0/24)|    |
|  |   - Security Group (SG6)  |      |
|  |      - Allow Database Port|      |
|  +--------------------------+      |
|  +--------------------------+      |
|  | Middleware Subnet (10.1.4.0/24)|  |
|  |   - Security Group (SG7)  |      |
|  |      - Allow Traffic from SG3|  |
|  +--------------------------+      |
+------------------------------------+

Flow of Traffic:
1. External users access the public subnet of the Service VPC (SG3 allows HTTP traffic).
2. Nginx installed in the public subnet forwards requests to the appropriate private subnets based on the request type.
3. Private Subnets 1, 2, and Middleware Subnet have their respective Nginx instances handling specific application logic.
4. Database Subnet contains the database server accessible only from the specific application subnets (SG6 allows database port traffic).

Proxying:
- The Nginx instance in the public subnet acts as a reverse proxy, directing requests to the appropriate backend Nginx servers in private subnets based on the request type.
- Security Groups (SG4, SG5, SG7) allow traffic only from the public subnet (SG3), ensuring proper communication between the proxy and backend servers.

Note: 
- Security groups and NACLs are not detailed fully for brevity. In a real setup, you'd define specific rules for incoming and outgoing traffic for each component.
- The specific configurations for Nginx, load balancing, and application logic are not included in this representation but would be essential for the setup.

