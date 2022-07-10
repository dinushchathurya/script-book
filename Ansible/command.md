### To ping hosts

```
ansible all -i <path to host file> -m ping
```
if ansible host file is existed in default direactory:

```
ansible all -m ping
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