Ansible Assignment-2

Install nginx in your servers(more then 2) and make sure the log files of nginx should not be granted more than 1 GB space on the nodes
Connection Status
![image](https://github.com/parsugit/ansible_practice/assets/132131379/382a0fd3-b503-41e8-82cc-1153aa42cd7d)


**Successfully Installed nginx in three servers.**
1)ansible -m apt -a "name=nginx state=present update_cache=yes" -b all

2)ansible all -m command -a “nginx -v”

![image](https://github.com/parsugit/ansible_practice/assets/132131379/292f337a-4871-4201-8358-63baf0b7dbb1)


**Make sure the log files of nginx should not be granted more than 1 GB space on the nodes**
3)ansible all -b -a "sed -i '3i\       size 1G' /etc/logrotate.d/nginx
4)ansible all -b -a "cat /etc/logrotate.d/nginx "
![image](https://github.com/parsugit/ansible_practice/assets/132131379/2d1c3dff-3162-4546-8e58-ca35855ee89f)

**Remove Default nginx file content**
5)ansible all -b -m shell -a "echo > /etc/nginx/sites-enabled/default"
![image](https://github.com/parsugit/ansible_practice/assets/132131379/0a84e745-681c-4ebd-978a-f7734a1076ac)


**Change content in Default nginx file.**
6)ansible all -b -m shell -a "echo 'server {
    listen 80;
    server_name parasharam.opstree.com;
    root /var/www/content;
    index index.html;

    location / {
        try_files \$uri \$uri/ =404;
    }
}' >> /etc/nginx/sites-available/default"
![image](https://github.com/parsugit/ansible_practice/assets/132131379/15dfea23-91af-4bcd-aba8-726d0fd9003f)


7)create directory (Optional)
ansible all -m file -a "path=/var/www/parasharam state=directory" -b 
ansible all -m file -a "path=/var/www/khushi state=directory" -b 
ansible all -m file -a "path=/var/www/shikha state=directory" -b 
ansible all -m file -a "path=/var/www/raman state=directory" -b 
ansible all -m file -a "path=/var/www/ashish state=directory" -b

8)ansible server2 -m copy -ba "src=/var/www/ dest=/var/www"
9)ansible server2 -ba "ls /var/www/ "

![image](https://github.com/parsugit/ansible_practice/assets/132131379/bc07fe75-3e80-488c-b7c0-2c29ebda0f65)


10)ansible server2 -m ansible.builtin.service -a "name=nginx state=restarted" -b

![image](https://github.com/parsugit/ansible_practice/assets/132131379/073dd45a-e692-4c66-84d8-468bb2359422)


11)ansible server2 -m shell -a "bash /var/www/web_rotate.sh" -b

Create equal number of websites as per your team  members and every members website should be hosted for only 2 hours and after every 2 hours another website should start displaying.
   - First 2 hours <team>.opstree.com should display content of parasharam website
   - Next 2 hours <team>.opstree.com should display content of ashish website
   - Next 2 hours <team>.opstree.com should display content of raman website
   - Next 2 hours <team>.opstree.com should display content of khushi website
   - Next 2 hours <team>.opstree.com should display content of shikha website


Install Apache
Also Configure nginx to run as reverse proxy to apache after completing first point individually.


- Run the ansible commands in such a way that workers nodes are updated one by one and not altogether and also make sure using all type of strategies.
