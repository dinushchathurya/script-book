### To find SWAP Storage

```
free -m
```

### Disable SWAP

```
swapoff -a
```

### To make it permanent

```
vi /etc/fstab


commnt /dev/mapper/centos-swap swap
```