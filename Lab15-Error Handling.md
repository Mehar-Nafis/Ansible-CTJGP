## Error Handling



Create another playbook named second.yaml as below
```
vi second.yml
```
```
---
- hosts: all
  gather_facts: no
  become: yes
  tasks:
    - name: install common packages
      yum:
        name: [wge, url]
        state: present
      register: out
      ignore_errors: yes  # This will ensure the playbook continues even if the task fails

    - name: list result of previous task
      debug:
        msg: "{{ out.rc }}"

   
```
Execute the playbook second.yaml
```
ansible-playbook second.yml
```

verify the installed packages on managed node by following commands#
```
ansible all -m command -a "yum list wget curl" -b
```
