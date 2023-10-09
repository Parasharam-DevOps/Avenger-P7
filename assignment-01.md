
ANSIBLE ASSIGNMENT-1

UserManager:

1. Create a group:
   
   ansible server1 -m group -a "name=team1"
   
![image](https://github.com/parsugit/ansible_practice/assets/132131379/1ecdfb9f-f9e4-4fb1-8097-4f1bb860d670)

   

3. Add the user Nitish to the team1 group and create the home directory:

   ansible server1 -m user -a "name=Nitish group=team1 createhome=yes" -b

   ![image](https://github.com/parsugit/ansible_practice/assets/132131379/4a69d059-caa5-47ed-a582-6c80159da19d)



4. Ensure the user Nitish has read, write, and execute access to the home directory:

   ansible server1 -m file -a "path=/home/Nitish owner=Nitish group=team1 mode=0755" -b

   ![image](https://github.com/parsugit/ansible_practice/assets/132131379/88123be6-22e1-4d08-82bd-256798bf763b)



6. Ensure that all users of the same team have read and execute access to the home directory of fellow team members:

   # For the 'team' directory
   
   ansible server1 -m file -a "path=/home/Nitish/team owner=Nitish group=team1 mode=0770 state=directory"
   ![image](https://github.com/parsugit/ansible_practice/assets/132131379/2f52a4d0-b2c4-4cc6-adc5-b7a408458fd1)


   # For the 'ninja' directory

   ansible server1 -m file -a "path=/home/Nitish/ninja owner=Nitish group=team1 mode=0777 state=directory" -b

   ![image](https://github.com/parsugit/ansible_practice/assets/132131379/3b6028f8-afd7-40e7-9c24-485992021d10)



These ad hoc commands perform the same tasks as the tasks defined in your Ansible playbook but are executed individually on the command line.

Additional Features:

Change user Shell -

    ansible server1 -m user -a "name=Nitish shell=/bin/bash" -b
 ![image](https://github.com/parsugit/ansible_practice/assets/132131379/c92102be-1033-4a6b-88dd-72f45382bbb1)


Change user password -

    ansible server1 -m user -a "name=Nitish password='{{ '12345' | password_hash('sha512') }}'" -b
 ![image](https://github.com/parsugit/ansible_practice/assets/132131379/fca4c1a5-ff90-4eb3-9b84-aff8e0a1b3c1)


Delete user -

    ansible server1 -m user -a "name=Nitish state=absent remove=true " -b
 ![image](https://github.com/parsugit/ansible_practice/assets/132131379/75c6e16e-026c-46e6-9438-ea3b880d06f2)


Delete Group - 

    ansible server1 -m group -a "name=team1 state=absent " -b
   ![image](https://github.com/parsugit/ansible_practice/assets/132131379/87145cfa-43ff-489f-8883-aec2693e30d3)

List user or Team - 

    ansible server1 -m shell -a "getent group" -b
   ![image](https://github.com/parsugit/ansible_practice/assets/132131379/544d3cf9-9081-48a7-a710-f32432a34832)

    
    ansible server1 -m shell -a "getent passwd" -b
   ![image](https://github.com/parsugit/ansible_practice/assets/132131379/55193641-8f73-4778-bb41-a75db8abcd92)
