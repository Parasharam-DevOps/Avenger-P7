# Scylla Ansible Role

|   Author     |  Created on   |  Version   | Last updated by | Last edited on |
| ------------ | --------------| -----------|---------------- | -------------- |
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | 18 Jan 2024   |     Version-1     | Parasharam Desai    | 18 Jan 2024   |



# handlers file for cassandra-tool

- name: Restart scylla
  systemd:
    name: scylla-server
    state: restarted

---
# - name: Gather IP Address
#   setup:
#   register: target_host_info

# - name: Debug Nodetool status
#   debug:
#     var: target_host_info


# Replace scylla yaml file into server

- name: Copy scylla configuration template into ubuntu
  template:
    src: scylla.yaml.j2
    dest: /etc/scylla/scylla.yaml
  notify: Restart scylla

- meta: flush_handlers

- name: Pause for 30 seconds
  pause:
      seconds: 30

- name: See Nodetool Status
  command: "nodetool status"
  register: status

- name: Debug Nodetool status
  debug:
    var: status


# tasks file for scylla-ansible-role
---
# - name: Install Dependencies
#   import_tasks: dependencies.yml

# - name: Install on Debian
#   import_tasks: ubuntu.yml

- name: Configure Scylladb
  import_tasks: config.yml


---
- name: Update Apt Cache
  apt:
    update_cache: yes

- name: Create directory for cassandra and keyrings
  file:
    path: "{{ item }}"
    state: directory
    mode: "0777"
  loop:
    - /etc/apt/keyrings
    - /etc/scylla/cassandra

- name: Install Java
  apt:
    name: "{{ java_apt_package }}"
    state: present

- name: Import ScyllaDB GPG Key
  become: true
  raw: "{{ scylla_repo_key_url }}"

- name: Add ScyllaDB Repository
  get_url:
    url: "{{ scylla_repo_url }}"
    dest: "{{ scylla_repo_dest }}"

- name: Update Apt Cache
  apt:
    update_cache: yes

- name: Install Scylla
  apt:
    name: scylla
    state: present
  failed_when: false

- name: Run Scylla
  command: scylla_setup
  args:
    stdin: "YES\nYES\nYES\nYES\nYES\nYES\nYES\nYES\nyes\nYES\nyes\nYES\nyes\nYES\nyes\nYES\nYES\nYES\nYES\nYES\nYES\nYES\nyes"
  register: scylla_setup_output
  failed_when: false

- name: Debug Scylla setup output
  debug:
    var: scylla_setup_output

- name: Start and enable scylla service
  systemd:
    name: scylla-server
    state: started
    enabled: yes

- name: Pause for 30 seconds
  pause:
      seconds: 30

- name: See Nodetool Status
  command: "nodetool status"
  register: status

- name: Debug Nodetool status
  debug:
    var: status





---
- hosts: tag_Name_scylla
  remote_user: ubuntu
  become: yes
  roles:
    - scylla-ansible-role



---
# vars file for scylla-ansible-role
# Java version
java_apt_package: openjdk-17-jre

scylla_seed_nodes: "{{ groups['tag_Name_scylla'] | map('extract', hostvars, ['ansible_default_ipv4', 'address']) | join(',') }}"
scylla_endpoint_snitch: "GossipingPropertyFileSnitch"
# GossipingPropertyFileSnitch
# Scylladb gpg command

scylla_repo_key_url: "gpg --homedir /tmp --no-default-keyring --keyring /etc/apt/keyrings/scylladb.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys d0a112e067426ab2"
scylla_repo_url: http://downloads.scylladb.com/deb/debian/scylla-5.4.list
scylla_repo_dest: "/etc/apt/sources.list.d/scylla.list"




## Contact Information

|    Name    | Email Address |
| -----------| --------------|
| **[Parasharam Desai](https://github.com/Parasharam-Desai)** | parasharam.desai.snaatak@mygurukulam.co |

---
## Resources and References

| **Source**                                              | **Description**                               |
|---------------------------------------------------------|-----------------------------------------------|
| [Atlassian Feature Branch Workflow Tutorial](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) | Refer to this tutorial for more information on the Feature Branch Workflow. |

