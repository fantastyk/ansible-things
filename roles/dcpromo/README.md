#Purpose
Promotes a domain controller into the designated domain. Requires Domain admin credentials

#Variables
```
domain_name -- domain name  ex. google.com
domain_admin  -- domain admin account
domain_admin_pass -- domain admin password
DSRM_password  -- Directory services recovery password
dns -- should be 127.0.0.1
dns2 -- IP of a second domain controller
```


#Examples
```
- name: Domain Controller
  hosts: dc
  serial: 1
  # tasks:
  vars_files:
    - vars/domain.yml
  tasks:
    - include_role:
        name: dcpromo
      vars:
        domain_name: "{{ domain['domain_name']}}" 
        domain_admin: "{{ domain['domain_admin_user'] }}"
        domain_admin_pass: "{{ domain['domain_admin_pass'] }}"
        DSRM_password: "{{ domain['domain_admin_pass'] }}"
        # TODO: set in variable file - look into expressing with jinja template
        dns: "{{ domain['dns1'] }}"
        dns2: "{{ domain['dns3'] }}"
  tags: dc
  ```
