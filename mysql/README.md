# Remove MySQL completely (on MacOS)
*Here is instruction for removing mysql completely on `Mac OS` (if you need)*

> **Note:** Use `mysqldump` to backup your databases

### 1. Check MySQL processes and kill them
```
ps -ax | grep mysql // Check processes
sudo mysqld stop // or sudo brew services stop mysql
```

### 2. Analyze MySQL on HomeBrew
```
brew remove mysql
brew cleanup
```

### 3. Remove files from your mac:
```
sudo rm /usr/local/mysql
sudo rm -rf /usr/local/var/mysql
sudo rm -rf /usr/local/mysql*
sudo rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
sudo rm -rf /Library/StartupItems/MySQLCOM
sudo rm -rf /Library/PreferencePanes/My*
```

### 4. Unload previous MySQL Auto-Login
```
launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```

### 5. Remove previous MySQL Preferences
```
rm -rf ~/Library/PreferencePanes/My*
sudo rm -rf /Library/Receipts/mysql*
sudo rm -rf /Library/Receipts/MySQL*
sudo rm -rf /private/var/db/receipts/*mysql*
```

### 6. Restart your computer just to ensure any MySQL processes are killed
