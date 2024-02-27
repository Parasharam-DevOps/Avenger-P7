# ScyllaDB Configuration and User Management
---

### Uncomment Part in ScyllaDB Configuration File

#### UNCOMMENT THIS PART IN GIVEN PATH
#### PATH - sudo vim /etc/scylla/scylla.yaml
    authenticator: AllowAllAuthenticator
    authenticator: PasswordAuthenticator


#### RESTART SERVICE
---
    sudo systemctl restart scylla-server.service


#### CHECK STATUS
  ---
    sudo systemctl status scylla-server.service
#### IF STATUS IS INACTIVE START THE SERVICE
---
    sudo systemctl start scylla-server.service
#### SWITCH INTO CASSANDRA USER
---
Replace 172.31.42.239 with your ScyllaDB instance IP.
    cqlsh 172.31.42.239 -u cassandra -p cassandra
#### CREATE USER
---
    CREATE USER scylladb WITH PASSWORD 'password' SUPERUSER;


#### GRANT PERMISSIONS ON KEYSPACE
---
    GRANT ALL PERMISSIONS ON KEYSPACE employee_db TO scylladb;


#### LIST USERS
---
    LIST USERS;


#### CHANGE USER PASSWORD
---
    ALTER USER scylladb WITH PASSWORD 'new_password';
