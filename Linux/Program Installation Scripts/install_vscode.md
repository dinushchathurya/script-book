### ONLY FOR DEBIAN-BASED (ubuntu, popos, debian, mint, etc) X64 LINUX SYSTEMS

You can simply run 

```bash
wget -O - https://raw.githubusercontent.com/realKarthikNair/realKarthikNair/main/scripts/vscode.sh | bash
```

OR manually paste

```bash
#!/usr/bin/bash

# remove snap version if exists

sudo snap remove code

# fetch deb version

wget "https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64" --output-document=code.deb

# install 

sudo dpkg -i code.deb

# delete deb file
rm code.deb
```
