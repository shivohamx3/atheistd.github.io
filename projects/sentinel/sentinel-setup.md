# Setup *sentinel* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/sentinel/sentinel.jpg)




### First setup

- ` ╰─> cd .ssh`
- ` ╰─> ssh-keygen -t rsa -b 4096` `sentinel`
- ` ╰─> ssh-copy-id -i ~/.ssh/sentinel.pub pi@8.0.0.4`
- `$ ssh pi@8.0.0.4`
- `$ sudo apt update && sudo apt upgrade`
- `$ sudo raspi-config`
- `$ sudo reboot +0`




### Installing necessary packages

- `$ vncserver -geometry 1920x1080`
- `$ sudo apt install apache2 curl exfat-fuse exfat-utils ffmpeg firefox-esr git glances gparted neofetch nload samba samba-common-bin speedtest-cli telegram-desktop terminator transmission wget zsh youtube-dl zfs-fuse`
- `$ sudo apt install gcc cmake libncurses5 libncurses5-dev build-essential -y`
- `$ curl -sSL https://install.pi-hole.net | bash`
- `$ pihole -a -p`
- `$ git config --global credential.helper store`
- `$ git config --global core.editor vim`
- `$ git config --global user.name "YOUR NAME"`
- `$ git config --global user.email "YOUR EMAIL"`





### Setup smb disks and directories' permissions

- `% sudo chmod 770 -R /heathen_nd`
- `% sudo usermod -a -G www-data pi`
- `% sudo chown -R -f pi:www-data /heathen_nd`




### Setup vnc-startup & grant read-only permission to `apache`

- `% vim atheistd_startup.sh `<br>

*atheistd_startup.sh*
```#!/bin/sh

# /etc/init.d/atheistd_startup.sh
### BEGIN INIT INFO
# Provides:          atheistd_startup.sh
# Required-Start:    $remote_fs $syslog
# Required-Stop:     $remote_fs $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Start daemon at boot time
# Description:       Enable service provided by daemon.
### END INIT INFO

runuser -l pi -c "vncserver -geometry 1920x1080"
echo "$now" >> /home/pi/log.txt
mount --uuid 7fc85a61-e23a-456b-9ab7-a8733a13426e /heathen_nd
```

- `% chmod +x atheistd_startup.sh`
- `% sud mv atheistd_startup.sh /etc/init.d/atheistd_startup/sh`
- `% sudo update-rc.d atheistd_startup.sh defaults`




### SMB set-up

- `% sudo vim /etc/samba/smb.conf`
> `[heathen]`<br>
> 	`guest ok = no`<br>
>	`comment = heathen_nd`<br>
>	`path = /heathen_nd`<br>
>	`browseable = yes`<br>
>	`writeable = yes`<br>
>	`create mask = 0700`<br>
>	`directory mask = 0700`<br>
<br>
> `[heathen_guest]`<br>
> 	`guest ok = yes`<br>
>	`comment = heathen-guest`<br>
>	`path = /heathen_nd`<br>
>	`browseable = yes`<br>
>	`writeable = yes`<br>
>	`create mask = 0444`<br>
>	`directory mask = 0444`<br>
<br>
>`[pi]`<br>
>	`guest ok = no`<br>
>	`comment = home`<br>
>	`path = /home/pi`<br>
>	`browseable = yes`<br>
>	`writeable = yes`<br>
>	`create mask = 0700`<br>
>	`directory mask = 0700`<br>

- `% sudo smbpasswd -a pi`




### `apache2` & `lighttpd` set-up

- `% sudo vim /etc/apache2/ports.conf`
> `Listen 80`<br>
> `Listen 666`

- `% sudo vim /etc/apache2/apache2.conf`
>`<Directory /heathen_nd>`<br>
>	`Options Indexes FollowSymLinks`<br>
>	`AllowOverride None`<br>
>	`Require all granted`<br>
>`</Directory>`<br>
>
>`<Directory /home/pi>`<br>
>	`Options Indexes FollowSymLinks`<br>
>	`AllowOverride None`<br>
>	`Require all granted`<br>
>`</Directory>`<br>

- `% sudo vim /etc/apache2/sites-available/000-default.conf`
>`<VirtualHost *:80>`<br>
>	`ServerAdmin webmaster@localhost`<br>
>	`DocumentRoot /heathen_nd`<br>
>`</VirtualHost>`
>
>`<VirtualHost *:666>`<br>
>	`ServerAdmin webmaster@localhost`<br>
>	`DocumentRoot /home/pi`<br>
>`</VirtualHost>`<br>

- `% sudo vim /etc/lighttpd/lighttpd.conf`
>`server.port = 200`

- `% rsmbd && rapached && rlighttpd`




### Setup python environment

- `% python3 -m venv custom`
- `% startpy`
- `% pip3 install numpy gpiozero RPi.GPIO matplotlib ipython`




### [remote.it](http://remote.it/) set-up

- `% curl -LkO https://raw.githubusercontent.com/remoteit/installer/master/scripts/auto-install.sh`
- `% chmod +x ./auto-install.sh`
- `% sudo ./auto-install.sh`
- `% sudo connectd_installer`




### Compiling `fish-shell`
- `$ git clone --depth 1 https://github.com/fish-shell/fish-shell`
- `$ cd fish-shell`
- `$ mkdir build && cd build`
- `$ cmake ..`
- `$ make`
- `$ sudo make install`
- `$ echo /usr/local/bin/fish | sudo tee -a /etc/shells`
- `$ chsh -s $(which fish) $whoami`
- `$ fish`




### Panel applets

- System Tray
- Ejecter
- Bluetooth
- Wireless & Wired Network
- Volume Control (ALSA/BT)
- Battery (pi-top / laptop)
- CPU Usage Monitor
- CPU Temperature Monitor
- Spacer
