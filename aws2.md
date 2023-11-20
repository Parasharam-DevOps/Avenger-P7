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

Create in such a way that both vpc networks can communicate with each other. 

![image](https://github.com/parsugit/ansible_practice/assets/132131379/7e014200-4a0e-47f7-a19f-601076a66a7b)

**Output**

Service ---> Management

![image](https://github.com/parsugit/ansible_practice/assets/132131379/805d94f1-4063-4619-8ad6-65e9e5f04575)


Management ---> Service

![image](https://github.com/parsugit/ansible_practice/assets/132131379/63b139d9-9b36-40e5-a27b-8e48266c3a22)



**Load Balancer**

![image](https://github.com/parsugit/ansible_practice/assets/132131379/5835bc6d-a9d7-4e18-89d5-f8199badefb6)


Then setup nginx in service vpc under private subnet and use another nginx as a reverse proxy which can forward traffic from load balancer to nginx web hosting.

Private Server Config

server {
  listen 80;
  server_name example.com;

  location / {
      proxy_pass http://backend-server-1;
  }

  location /app2/ {
      proxy_pass http://backend-server-2;
  }
}

Middleware nginx config:

root@ip-10-0-140-62:/etc/nginx/sites-enabled# cat default

server {
listen 80;
server_name localhost;
location / {
    proxy_pass http://10.0.28.86;
}
}



**Output**

![image](https://github.com/parsugit/ansible_practice/assets/132131379/d77a3a93-202b-4f16-af1c-02f0d2e1b2de)


Day2:
You need to manage 
route tables of both the networks in such a way that only your teammates ip addresses should be allowed to igw rest should be deny.
Also manage Nacl group in such a way that it should allow traffic on specific port ranges to subnetworks.

"""While you are doing work on instance, some how your key 🗝️ is lost somewhere or currupted, client raising this issue as p0 and ask us for recover the key or kindly setup new key so that they can login the server atleast."""

**To resolve this issue i refered this blog: And relaunch new ec2 using existing instance AMI**

https://www.quora.com/How-can-you-recover-the-keys-of-an-EC2-instance














