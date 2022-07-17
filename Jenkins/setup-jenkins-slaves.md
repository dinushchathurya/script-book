### Setup Jenkins slave node

#### Create User as Jenkins

```
sudo useradd -m jenkins

sudo -u jenkins mkdir /home/jenkins/.ssh
```

#### Login to Jenkins Master and restart Jenkins service

```
sudo service jenkins restart
```

#### Add SSH Keys from Master to Slave 

In Master Node

```
sudo cat ~/.ssh/id_rsa.pub
```

In Slave Node

```
sudo -u jenkins vi /home/jenkins/.ssh/authorized_keys
```

#### Login to master node and try to SSH from Master to Slave

```
ssh jenkins@slave_node_ip
```

In Master Node

```
sudo cp ~/.ssh/known_hosts  /var/lib/jenkins/.ssh
```