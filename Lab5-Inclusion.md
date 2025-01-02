![image](https://github.com/user-attachments/assets/ab402abf-3e35-411a-a1ce-8b6cb09b39d0)

```
cd ~/ansible-labs && mkdir inclusions && cd inclusions
```
```
vi app_vars.yml
```
```
app_name: "MyApplication"
app_port: 8080
```
```
vi db_vars.yml
```
```
db_name: "MyDatabase"
db_user: "dbadmin"
```
```
vi inventory.ini
```
```
localhost ansible_connection=local
```
```
vi playbook.yml
```
```
- name: Demonstrate include_vars 
  hosts: localhost
  gather_facts: false
  vars_files: db_vars.yml

  tasks:
    - name: Print database variables
      debug:
        msg:
          - "Database Name: {{ db_name }}"
          - "Database User: {{ db_user }}"

    # - name: Dynamically include application variables
    #   include_vars: /home/ec2-user/ansible-labs/inclusion/app_vars.yml

    - name: Print application variables
      debug:
        msg:
          - "Application Name: {{ app_name }}"
          - "Application Port: {{ app_port }}"

    - name: Dynamically include application variables
      include_vars: /home/ec2-user/ansible-labs/inclusion/app_vars.yml

```
