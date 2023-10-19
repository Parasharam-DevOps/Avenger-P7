
Setup Spring3HibernateApp (https://github.com/opstree/spring3hibernate) on created infra using ansible playbook by following the below steps:

Install MySQL ,JDK 11 , Tomcat9

![image](https://github.com/parsugit/ansible_practice/assets/132131379/e0701e34-b533-400f-8a07-3d43ce0b9b62)

![image](https://github.com/parsugit/ansible_practice/assets/132131379/2c10613b-6032-4eb5-a063-526386bcd106)

Create the war file for Spring3HibernateApp using maven 

![image](https://github.com/parsugit/ansible_practice/assets/132131379/6a7500b8-9475-468b-82c5-aee6d3aeda4d)

![image](https://github.com/parsugit/ansible_practice/assets/132131379/8a82d9f3-0765-41d9-ae4e-bc89a931d702)

Send the war file created earlier to path "/opt/tomcat/apache-tomcat-7.0.108/webapps/"

Restart tomcat service

opstree/spring3hibernate

A java loaded application for various testing purpose

Website

https://opstree.github.io


