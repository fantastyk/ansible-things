# Purpose
Configures windows machines to a baseline onfiguration. 

- Sets Timezone
- Activates Windows
- Sets WMI to static port 

# Variables
```properties
local_timezone: sets timezone on machine. Defaults to EST. (tzutil.exe /l to see additional timezones.)
license_key: windows activation key. 

```
# Example
```yaml
- name: Setting Baseline
  hosts: all
  vars_files:
   - vars/domain.yml
  tasks: 
    - include_role: 
        name: windows_baseline

```