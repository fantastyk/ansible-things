#Purpose
Sets up a generic Windows Failover Cluster with a cloud witness as a quorum disk. 

#Variable
```
domain_name: domain name to create the cluster in 
domain_admin: username to authenticate to domain
domain_admin_pass: password to authenticate to domain. 
cluster_name: cluster name
cluster_ip: cluster IP microsoft failover cluster
storage_account: azure storage account for cloud disk
storage-Key: storage account key to setup cloud disk
cloud_quorum: true or false  - not in use yet
retry_interval_sec: defaults to '10' - ensures that a node waits for a remote cluster to be created
retry_count: defaults to '60' - ensures that a node waits for a remote cluster to be created
```

#Example
```
Sets up Failover Clustering with cloud witness disk
- name: Failover Cluster - Config - StorageSpaces
 hosts: cluster1
 vars_files:
   - vars/domain.yml
 vars:
   ansible_user: nwujastyk@foxhound.com
   ansible_connection: psrp
   ansible_psrp_auth: credssp
   ansible_psrp_credssp_auth_mechanism: ntlm
   ansible_credssp_minimum_version: 5
 tasks: 
   - include_role: 
       name: win_cluster_config
     vars:
       #first_node: true
       domain_name: "{{ domain['domain_name']}}"
       domain_admin: "{{ ansible_user }} "
       domain_admin_pass: "{{ domain['domain_admin_pass'] }}"
       cluster_name: "{{ domain.S2D1['cluster_name'] }} "
       cluster_ip: "{{ domain.S2D1['cluster_ip'] }} "
       storage_account: "{{ domain.S2D1['storage_account'] }}"
       storage_key: "{{ domain.S2D1['storage_key'] }}"
       cloud_quorum: true
 tags: failover
```
