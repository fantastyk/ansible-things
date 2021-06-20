# Purpose
Role to install the crowdstrike sensor.

# Variables
```
Installer_path  -- *REQUIRED* Where to copy the install file 
CID -- *REQUIRED* This is a customer ID that is provided in the crowdstrike portal
```

# Example Usage
```
- name: Install Crowdstrike Sensor
  hosts: pdc:dc:non_dc
  vars_files: 
   - vars/domain.yml
  vars:
    ansible_become: yes
    ansible_become_method: runas
    ansible_become_user: "{{ domain['domain_admin_user'] }}"
    ansible_become_password: "{{ domain['domain_admin_pass'] }}"
    ansible_become_flags: logon_type=interactive
  tasks: 
    - include_role: 
        name: crowdstrike_sensor
      vars:
        Installer_Path: "D:\\"
        CID: "{{  domain['crowdstrike_cid'] }}"
  tags: crowdstrike
```