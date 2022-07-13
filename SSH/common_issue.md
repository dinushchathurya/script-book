### Fix public key authentication issue

```
sudo vim /etc/ssh/sshd_config
```

```
PermitRootLogin no
PubkeyAuthentication yes

#GSSAPIAuthentication yes (commented out)
#GSSAPICleanupCredentials no (commented out)

UsePAM yes
```

```
sudo systemctl restart sshd
```

#### Give chmod permission to the directory

##### check permission

```
ls -ld ~/.ssh
```

```
ls -ld authorized_keys
```

##### Give chmod permission to the directory

```
chmod 0700 /home/your_home/.ssh
```

```
chmod 0600 /home/[username]/.ssh/authorized_keys
```
