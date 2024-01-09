Installation Of Redis
https://redis.io/docs/install/install-redis/install-redis-on-windows/

Installation of Redis
https://opensource.docs.scylladb.com/stable/getting-started/install-scylla/install-on-linux.html

Must Open two port  ScyllaDB - 9042 Redis- 6379


Config File 
Path - /etc/scylla/scylla.yaml
- seeds: "172.31.28.37"
listen_address: 172.31.28.37
endpoint_snitch: SimpleSnitch
rpc_address: 172.31.28.37

EMPLOYEE API

Create KEYSPACE In ScyllaDB
CREATE KEYSPACE IF NOT EXISTS employee_db
  WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
  
  
Create table under the employee_db KEYSPACE
PATH - migration/000001_create_employee_info_table.down.sql
 CREATE TABLE IF NOT EXISTS employee_info (
    id text, name text, designation text, department text,
    joining_date date, address text, office_location text,
    status text, email text, phone_number text,
    PRIMARY KEY (id, joining_date)
) WITH CLUSTERING ORDER BY (joining_date DESC);
  
CHANGE IP

PATH - employee-api/migration.json
PATH - employee-api/config.yaml



SALARY API 

DESCRIBE KEYSPACES;
USE employee_db;
Create table under the employee_db KEYSPACE
CREATE TABLE IF NOT EXISTS employee_salary (
                                 id text,
                                 process_date text,
                                 name text,
                                 salary float,
                                 status text,
                                 PRIMARY KEY (id, process_date)
) WITH CLUSTERING ORDER BY (process_date DESC);

DESCRIBE TABLES;


CHANGE IP

PATH - src/main/resources/application.yml
PATH - salary-api/migration.json




