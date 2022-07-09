### Connect to Ansible node using SSH

Step 1: 

Create SSH Key Pair
```
ssh-keygen
```

Step 2:

Add SSH Key to remote machine
```
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@remote_ip
```

Step 3:

SSH to remote server
```
ssh user@remote_ip
```
