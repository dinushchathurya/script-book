### Create SSH Key 

```
ssh-keygen -t <type> -C "<comment>"

ssh keygen-t ed25519 -C "My defualt key"
```

### Get content created key 

```
cat <path>/<key_name>

cat .ssh/id_ed25519.pub
```

### Copy key to server

```
ssh-copy-id -i ~/<path>/<key_name> <ip of the server>

ssh-copy-id -i ~/.ssh/id_ed25519.pub 172.16.250.133
```