### Fetch latest Chrome debian package, install it and delete the package from system

You can directly run 

```bash
wget -O - https://github.com/realKarthikNair/realKarthikNair/raw/main/scripts/chrome.sh | bash
```

Or 


```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

sudo dpkg -i google-chrome-stable_current_amd64.deb

rm google-chrome-stable_current_amd64.deb
```