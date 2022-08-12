### Prerequisites:

<li>Open JDK 8</li>
<li>Minimum CPU’s: 4</li>
<li>ubuntu server with sudo privileges.</li>
<li>Firewall/Inbound port: 22, 8081</li>

### Update the System

```
sudo apt-get update
```

### Install java

```
sudo apt install openjdk-8-jdk
```

### Check Java version

```
java -version
```

### Create a system account for Nexus

```
useradd -M -d /opt/nexus -s /bin/bash -r nexus
```

### Provide the sudo permission to Nexus user

```
echo "nexus ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/nexus
```

### Change the directory

```
cd /opt
```

### Download Nexus

```
wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
```

### Extract the downloaded folder

```
tar -zxvf latest-unix.tar.gz
```

### Rename the extracted Nexus setup folder to nexus

```
mv /opt/nexus-3.37.0-01 /opt/nexus
```

### Provide the permission to Nexus & sonatype-work folder

```
chown -R nexus:nexus /opt/nexus

chown -R nexus:nexus /opt/sonatype-work
```

### Run nexus as service at boot time

```
sudo vim /opt/nexus/bin/nexus.rc
```

### Uncomment & edit the following line

```
run_as_user="nexus"
```

### Change the nexus JVM heap size

```
sudo vim /opt/nexus/bin/nexus.vmoptions
```

then add

```
-Xms1024m
-Xmx1024m
-XX:MaxDirectMemorySize=1024m
-XX:LogFile=./sonatype-work/nexus3/log/jvm.log
-XX:-OmitStackTraceInFastThrow
-Djava.net.preferIPv4Stack=true
```

### To run nexus as service using Systemd

```
sudo vim /etc/systemd/system/nexus.service
```

then add

```
[Unit]
Description=nexus service
After=network.target
[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop
User=nexus
Restart=on-abort
[Install]
WantedBy=multi-user.target
```

### To start & enable nexus service

```
systemctl start nexus

systemctl enable nexus
```

### To check nexus service status

```
systemctl status nexus
```

### To check nexus service logs

```
tail -f /opt/sonatype-work/nexus3/log/nexus.log
``` 

### To open the 8081 port number in UFW firewall

```
ufw allow 8081/tcp
```

### Open Nexus Repository Web Interface

```
http://server-ip:8081
```

### Finding the default password for Nexus

```
cat sonatype-work/nexus3/admin.password
```