# Setup *sentinel* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/sentinel/sentinel.jpg)



### First setup + disabling `snapd`

- ` ╰─> cd .ssh`
- ` ╰─> ssh-keygen -t ed25519 `
- ` ╰─> ssh-copy-id -i ~/.ssh/sentinel.pub ubuntu@192.168.1.104`

- `$ sudo systemctl stop snapd.service`
- `$ sudo systemctl disable snapd.service`
- `$ sudo reboot +0`

- `$ sudo apt update && sudo apt upgrade -y`
- `$ sudo vim /etc/hostname`
- `$ sudo vim /etc/hosts`
> 127.0.1.1 sentinel.localdomain sentinel
- `$ sudo reboot +0`



### Install and setup `xfce` + vnc-server

- `$ sudo apt install xfce4 xfce4-goodies -y` (select dgm3)
- `$ sudo apt install tightvncserver -y`
- `$ vncserver`
- `$ vncserver -kill :1`
- `$ mv ~/.vnc/xstartup ~/.vnc/xstartup.bak`
- `$ vim ~/.vnc/xstartup`
```
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
```
- `$ chmod +x ~/.vnc/xstartup`
- `$ sudo reboot +0`



### Installing necessary packages

- `$ vncserver -geometry 1920x1080`

- `$ sudo apt install apache2 curl exfat-fuse exfat-utils ffmpeg firefox fish git glances gparted neofetch nload rar samba samba-common-bin speedtest-cli telegram-desktop terminator transmission unrar vim wget youtube-dl zfsutils-linux zsh -y`
- `$ eval "$(ssh-agent -s)"`



### Setup smb disks and directories' permissions

*/etc/fstab*
```
UUID=a81d34d0-0502-48f0-9176-634f5becff2f	/heathen_nd	ext4	defaults,errors=remount-ro	0	1
```

- `$ sudo mount -a`
- `$ sudo chmod 770 -R /heathen_nd`
- `$ sudo chown -R ubuntu:www-data /heathen_nd`



### Setup pi-hole

- `$ curl -sSL https://install.pi-hole.net | bash`
- `$ pihole -a -p`



### Setup git

- `$ git config --global credential.helper store`
- `$ git config --global core.editor vim`
- `$ git config --global user.name "YOUR NAME"`
- `$ git config --global user.email "YOUR EMAIL"`



### SMB set-up

*/etc/samba/smb.conf*
```
[heathen]
	guest ok = no
	comment = heathen_nd
	path = /heathen_nd
	browseable = yes
	writeable = yes
	create mask = 0700
	directory mask = 0700
[pi]
	guest ok = no
	comment = home
	path = /home/ubuntu
	browseable = yes
	writeable = yes
	create mask = 0700
	directory mask = 0700
```

- `$ sudo smbpasswd -a ubuntu`



### `apache2` & `lighttpd` set-up

*/etc/apache2/ports.conf*
```
Listen 80
Listen 666
```

*/etc/apache2/apache2.conf*
```
<Directory /heathen_nd>
	Options Indexes FollowSymLinks
	AllowOverride None
	Require all granted
</Directory>
<Directory /home/ubuntu>
	Options Indexes FollowSymLinks
	AllowOverride None
	Require all granted
</Directory>
```

*/etc/apache2/sites-available/000-default.conf*
```
<VirtualHost *:80>
	ServerAdmin webmaster@localhost
	DocumentRoot /heathen_nd
</VirtualHost>
<VirtualHost *:666>
	ServerAdmin webmaster@localhost
	DocumentRoot /home/ubuntu
</VirtualHost>
```

*/etc/lighttpd/lighttpd.conf*
```
server.port = 200
```

- `$ sudo /etc/init.d/lighttpd restart` (lighttpd)
- `$ sudo systemctl restart apache2` (apache2)
- `$ sudo systemctl restart smbd` (samba)



### Set startup script

*/etc/init.d/pi_init.sh*
```
#!/bin/bash
# /etc/init.d/pi_init.sh
### BEGIN INIT INFO
# Provides:          userstartup.sh
# Required-Start:    $remote_fs $syslog
# Required-Stop:     $remote_fs $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Start daemon at boot time
# Description:       Enable service provided by daemon.
### END INIT INFO

su ubuntu -c "/usr/bin/vncserver -geometry 1920x1080"
```
- `$ sudo chmod +x /etc/init.d/pi_init.sh`
- `$ cd /etc/init.d/ && sudo update-rc.d pi_init.sh defaults`

- `$ crontab -e`
```
0 * * * * /usr/bin/rsync --recursive --size-only /home/ubuntu/.config/transmission/torrents/*.torrent /heathen_nd/config_dir/
```


### Disable locale env forwarding on ssh

- `$ /etc/ssh/ssh_config`

<b>replac</b> `SendEnv LANG LC_*` with ` # SendEnv LANG LC_*`
(comment the line out if you didn't understand)



### [remote.it](http://remote.it/) set-up

- `$ curl -LkO https://raw.githubusercontent.com/remoteit/installer/master/scripts/auto-install.sh`
- `$ chmod +x ./auto-install.sh`
- `$ sudo ./auto-install.sh`
- `$ sudo connectd_installer`
