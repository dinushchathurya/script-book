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

### SSH to remote server using specific SSH Key

```
ssh -i ~/.ssh/<key> <ip of the remote server>
```

### Set Passphrase

```
eval $(ssh-agent) 

ps aux | grep 2362

ssh-add
```

### Create Alias

```
alias ssha='eval $(ssh-agent) && ssh-add'

then 

ssha
```