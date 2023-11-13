
- name: Install Apache Cassandra and Configure
  hosts: server1
  become: yes
  gather_facts: yes

  vars:
    java_apt_package: openjdk-11-jre
    cassandra_repo_url: "deb https://debian.cassandra.apache.org 41x main"
    cassandra_repo_key_url: "https://downloads.apache.org/cassandra/KEYS"
    cassandra_version: "4.1.3"
    cluster_name: 'NinjaBatch23'
    cassandra_seeds: "172.31.2.4"
    cassandra_listen_address: "172.31.2.4"
    cassandra_rpc_address: "172.31.2.4"
    cassandra_endpoint_snitch: "RackInferringSnitch"
    cassandra_jvm_opts:
      - "-Dcassandra.ignore_dc=true"
      - "-Dcassandra.ignore_rack=true"

  tasks:
    - name: Install Java
      apt:
        name: "{{ java_apt_package }}"
        state: present
        update_cache: yes

    - name: Add Cassandra repository key
      apt_key:
        url: "{{ cassandra_repo_key_url }}"
        state: present

    - name: Add Cassandra repository
      apt_repository:
        repo: "{{ cassandra_repo_url }}"
        state: present

    - name: Download specific Cassandra version
      apt:
        update_cache: yes
        name: "cassandra={{ cassandra_version }}"
        state: present
      tags: install_cassandra

    - name: Start and enable Cassandra service
      systemd:
        name: cassandra
        state: started
        enabled: yes

    - name: Add JVM options to cassandra-env.sh
      blockinfile:
        path: /etc/cassandra/cassandra-env.sh
        insertbefore: EOF
        block: |
          {% for jvm_opt in cassandra_jvm_opts %}
          JVM_OPTS="$JVM_OPTS {{ jvm_opt }}"
          {% endfor %}
      notify: Restart Cassandra

    - name: Copy Cassandra configuration template
      template:
        src: /home/parsu/ansible/cassandra.yaml.j2
        dest: /etc/cassandra/cassandra.yaml
      notify: Restart Cassandra

    - name: Debug variables
      debug:
        var: "{{ item }}"
      with_items:
        - cluster_name
        - cassandra_seeds
        - cassandra_listen_address
        - cassandra_rpc_address
        - cassandra_endpoint_snitch

  handlers:
    - name: Restart Cassandra
      systemd:
        name: cassandra
        state: restarted

      
**output **

![image](https://github.com/parsugit/ansible_practice/assets/132131379/11d36823-7379-48f2-a010-7d284a4f3581)



