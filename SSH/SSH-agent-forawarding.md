### List all the available private identities

```
ssh-add -l
```

### Add Priavte Key to SSH Agent

```
ssh-add -K <pem-file-name>
```

### Connect to the server

```
ssh -A <user@server-ip>
```


### How to access instance in Private Subnet using SSH forwarding

<a href="https://trying2adult.com/how-to-use-ssh-agent-forwarding-in-bash-putty-and-mobaxterm-to-connect-to-servers-in-a-private-network/"> Refer this link for more details</a>