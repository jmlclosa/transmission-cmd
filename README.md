# transmission-cmd
Custom command for transmission remote cli with auto-organize functionality

## Usage
0. Transmission installed
1. Copy file to /usr/bin directory
2. Grant privileges
```
sudo chmod +x /usr/bin/tra
```
3. Create netrc.transmission file on $HOME to configure transmission authentication
```
machine localhost
login transmission
password transmission
```
4. Create tra.properties file on $HOME to configure where torrents must be auto organized. In this example, if a torrent name contains "Anatomia", torrent will be moved to $FINISHED_DIR/series/anatomia_grey
```
Suits=series/suits
Joven=series/joven_sheldon
Anatomia=series/anatomia_grey
Fear=series/fear_walking_dead
Bang=series/big_bang_theory
```
5. Configure transmission to auto organize torrents on finish.
5.1. Create /usr/local/bin/organize_torrent.sh and give permissions:
```
#!/bin/bash
tra org $TR_TORRENT_ID
```
```
sudo chmod +x /usr/local/bin/organize_torrent.sh
```
5.2. Edit /etc/transmission-daemon/settings.json:
```
    "script-torrent-done-enabled": true,
    "script-torrent-done-filename": "/usr/local/bin/organize_torrent.sh",
```
6. Enjoy :)

## Examples
* List all torrents
```
tra list
```

* Info for a torrent (by ID)
```
tra info 20
```

* Organize torrents based on tra.properties file
```
tra org
```

* Organize a torrent based on tra.properties file
```
tra org 20
```

* Move torrent file/s to finished directory
```
tra move 20
```

* Move torrent file/s to custom directory
```
tra move $HOME/my_videos
```
