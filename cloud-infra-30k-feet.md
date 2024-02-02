# Cloud Infra Design 30k Feet

| **Author**           | **Created On** | **Last Updated** | **Document Version** |
| -------------------- | -------------- | ---------------- | -------------------- |
| **Parasharam Desai** | 29-01-2024     | 29-01-2024       | V1                   |

# Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Cloud Infra Design Details](#cloud-infra-design-details)
4. [Infrastructure Diagram](#infrastructure-diagram)
5. [Contact Information](#contact-information)
6. [Resources and References](#resources-and-references)

***
# Introduction

The Cloud Infra Design 30k Feet documentation provides an in-depth overview of the Production, Development, Quality Assurance infrastructure hosted on AWS for the OT-Microservices project. This modern and modular architecture prioritizes scalability and efficiency, utilizing AWS services to establish a reliable, scalable, and high-performance foundation.


***
# Prerequisites
| Tool                  | Description                                  |
|-----------------------|----------------------------------------------|
| AWS Management Console | Required for provisioning AWS resources.     |

***
# Cloud Infra Design Details

To create the infrastructure, I used the following services on AWS and implemented them in Production, Development, and Quality Assurance.

| Service         | Item                  | Description                                         |
|-----------------|-----------------------|-----------------------------------------------------|
| **Region**      | **Europe**            |           Frankfurt (eu-central-1)                  |
| **Availability Zone**          | **eu-central-1a**         | Primary availability zone for the region. |
| **VPC**         | **OT-Micro-Dev-Vpc**      | VPC for Development Infrastructure              |
| **Subnets**     | **Public Subnet-1**   | Hosts the Bastion Host for secure access.           |
|                 | **Private Subnet-1**  | Hosts the Frontend application components.         |
|                 | **Private Subnet-2**  | Hosts the Attendance, Employee, and Salary APIs.    |
|                 | **Private Subnet-3**  | Hosts PostgreSQL, Scylla, and Redis databases.      |
| **Route Table**  | **Public-rt**        | Associates with Public Subnet-1 for internet access.|
|                 | **Private-rt**       | Associates with Private Subnet-1, Subnet-2, and Subnet-3.|
| **Internet Gateway** | **Igw**              | Internet Gateway for OT-Micro-Dev-Vpc.           |
| **NACL**        | **Nacl-1**           | Associates with Private Subnet-1.                  |
|                 | **Nacl-2**           | Associates with Private Subnet-2.                  |
|                 | **Nacl-3**           | Associates with Private Subnet-3.                  |
| **Security Groups** | **Bastion-sg**    | Security Group for Bastion.                       |
|                 | **Frontend-sg**      | Security Group for Frontend.                       |
|                 | **ATT-sg**           | Security Group for Attendance API.                 |
|                 | **EMP-sg**           | Security Group for Employee API.                   |
|                 | **Sal-sg**           | Security Group for Salary API.                     |
|                 | **PSql-sg**          | Security Group for PostgreSQL.                     |
|                 | **Scylla-sg**        | Security Group for Scylla database.                |
|                 | **Redis-sg**         | Security Group for Redis database.                 |
| **NAT Gateway** | **ALB**              | NAT Gateway for private subnet internet access.|
| **Application Load Balancer** | **ALB** |ALB for Frontend Traffic Distribution| 
| **Auto Scaling Group**         | **ASG** | Auto Scaling Group responsible for dynamically adjusting the number of instances for the frontend and API services based on demand.| 
***
# Infrastructure Diagram

**Production Environment**

![Cloud-Infra-30k feet - Page 1](https://github.com/avengers-p7/Documentation/assets/156056709/615999ae-ada0-4987-ae47-97f68e00f282)

**Development Environment**

![Cloud-Infra-30k feet - Page 1 (1)](https://github.com/avengers-p7/Documentation/assets/156056709/a49eb6c0-2a20-4917-af50-d3cff4dae50e)


**Quality Assurance**

![Cloud-Infra-30k feet - Page 1 (3)](https://github.com/avengers-p7/Documentation/assets/156056709/0e75cc96-30aa-48e4-8985-e62074c8eac5)



# Description

Here's a flow summary of the infrastructure 

**User Access:**

* Users connect to the infrastructure through the internet.

**Public Subnets:**

* Public subnets host components that need direct internet access.
* The Bastion Host resides in the public subnet to facilitate secure access.

**Private Subnets:**
* Frontend application components are hosted in one private subnet.
* Attendance, Employee, and Salary APIs are hosted in separate private subnets.
* PostgreSQL, Scylla, and Redis databases are hosted in another private subnet.

**Security Groups:**

* Different security groups are defined for various components.
  
* Bastion-sg for the Bastion Host.
* Frontend-sg for Frontend components.
* ATT-sg, EMP-sg, and Sal-sg for respective APIs.
* PSql-sg, Scylla-sg, and Redis-sg for database components.

**NACLs (Network Access Control Lists):**

* NACLs are associated with specific private subnets to control inbound and outbound traffic at the subnet level.

**Internet Gateway & NAT Gateway:**

* Internet Gateway (Igw) facilitates internet access for the VPC.
* NAT Gateway allows instances in private subnets to initiate outbound traffic to the internet.

**Route Tables:**

* Public-rt is associated with the public subnet for internet access.
* Private-rt is associated with private subnets, allowing communication within the VPC.

**ALB (Application Load Balancer):**

* ALB is configured for distributing frontend traffic across multiple targets, ensuring high availability.

**Auto Scaling Group (ASG):**
* ASG dynamically adjusts the number of instances for frontend and API services based on demand.

**Region and Availability Zone:**

* The infrastructure is deployed in the Europe region, specifically in the Frankfurt (eu-central-1) region.
* Availability zones (eu-central-1a) are utilized for redundancy and fault tolerance.
* Availability zones (eu-central-1b) are utilized for redundancy and fault tolerance.

**VPC (Virtual Private Cloud):**

* Separate VPCs are created for Development, Production, and Quality Assurance environments.
* This flow summary outlines the path of user access, the organization of components in public and private subnets, the role of security groups, NACLs, internet and NAT gateways, routing, and the use of load balancing and auto-scaling for ensuring scalability and availability of services.


***

# Contact Information

| Name               | Email Address                               |
| ------------------ | ------------------------------------------- |
| Parasharam Desai   | parasharam.desai.snaatak@mygurukulam.co     |

***
# Resources and References

|     Description                  | References  
| ---------------------------------| ------------------------------------------------------------------- |
|     Documentation Template       | https://github.com/OT-MICROSERVICES/documentation-template/wiki/Application-Template |
