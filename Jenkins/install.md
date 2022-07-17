### Update Packages

```
sudo apt update
```

### Install JDK

```
sudo apt install openjdk-11-jdk
```

### Check is Java installed successfully

```
java -version
```

### Add Repository key to the system

```
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
```
### Append debian package repo address to the system

```
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'


echo deb http://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
```

### Update Ubuntu package

```
sudo apt update
```

### Install Jenkins

```
sudo apt install jenkins -y
```

### Check Jenkins Server Status

```
systemctl status jenkins
```

### Adjusting Firewall

```
sudo ufw allow proto tcp from <IP RANGE> or <IP ADDRESS> to any port 8080

or

sudo ufw allow 8080
```

### Copy Initial password

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```