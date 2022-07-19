### To ping hosts

```
ansible all -i <path to host file> -m ping
```
if ansible host file is existed in default direactory:

```
ansible all -m ping
```
### Get all Ansible hosts

```
ansible all --list-hosts
```

### Gather facts about hosts

```
ansible all -m gather_facts

ansible all -m gather_facts --limit <ip address>
```

### Ping all nodes related to a particular ssh key

```
ansible all -i <path to host file> -m ping --key-file ~/.ssh/<key>
```

### Ping all nodes related to particular user

```
ansible all -u <user-name> -m ping
```
### Ping all nodes related to particular group

```
ansible <group-name> -m ping
```

### Get properties of a host

```
ansible all -m setup
```

### Install packages on a host

```
ansible <group> -u <user> -m yum -a "name=<package-name>" state=present -b
```

### Remove packages on a host

```
ansible <group> -u <user> -m yum -a "name=<package-name>" state=absent -b
```

### Get current user of a host

```
ansible all -m shell -a "whoami"

ansible all -m shell -a "uname -a"
```

### Get current uptime of a host

```
ansible all -m shell -a "uptime"
```

### Check particular user is exists on a host

```
ansible all -m shell -a 'cat /etc/passwd | grep <user-name>'
```

### Create an user on a host

```
ansible all -m user -a "name=<user-name> -b
```

### Run playbook

```
ansible-playbook <playbook-name>

ansible-playbook <playbook-name> --private-key=~/.ssh/<key name>
```

### Get all tasks of a playbook

```
ansible-playbook -i <inventory> <playbook-name> --list-tasks
```

### Get all tags of a playbook

```
ansible-playbook -i <inventory> <playbook-name> --list-tags
```

### Executing Tasks by Tag

```
ansible-playbook -i <inventory> <playbook-name> --tags=setup
```

### Skipping Tasks by Tag

```
ansible-playbook -i <inventory> <playbook-name> --exclude-tags=setup
```

### Starting Execution at Specific Task

```
ansible-playbook -i <inventory> <playbook-name> --start-at-task=<task name>
```

### Limiting Targets for Execution

Many playbooks set up their target as `all` by default, and sometimes you want to limit the group or single server that should be the target for that setup. You can use `-l` (limit) to set up the target group or server in that play:

```
ansible-playbook -l dev -i <inventory> <playbook-name>
```

### Controlling Output Verbosity

```
ansible-playbook -i <inventory> <playbook-name> -v

ansible-playbook -i <inventory> <playbook-name> -vvvv
```