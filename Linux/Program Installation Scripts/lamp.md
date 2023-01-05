### Install lamp stack on Debian based systems (Ubuntu, Linux Mint, Pop!_OS, etc)

You can directly run 

```bash
wget -O - https://github.com/realKarthikNair/realKarthikNair/raw/main/scripts/lamp.sh | bash
```

Or 

```bash
sudo apt update && sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql
sudo mysql_secure_installation
```