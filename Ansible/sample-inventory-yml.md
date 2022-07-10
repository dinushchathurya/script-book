### Sample Inventory YML

* if there is sepearte certificate for each group

```yaml
webservers:
    hosts:
        - webserver1
        - webserver2
    vars: ansible_ssh_private_key_file: /home/<user-name>/<certificate-file>
dbservers:
    hosts:
        - dbserver1
        - dbserver2
    vars: ansible_ssh_private_key_file: /home/<user-name>/<certificate-file>
gateways:
    hosts:
        - gateway1
        - gateway2
    vars: ansible_ssh_private_key_file: /home/<user-name>/<certificate-file>
```

* If there is only one certificate for all groups

```yaml
webservers:
    hosts:
        - webserver1
        - webserver2
dbservers:
    hosts:
        - dbserver1
        - dbserver2
gateways:
    hosts:
        - gateway1
        - gateway2
all:
    vars:
        ansible_ssh_private_key_file: /home/<user-name>/<certificate-file>
```
