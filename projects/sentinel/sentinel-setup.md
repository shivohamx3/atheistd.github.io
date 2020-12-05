# Setup *sentinel* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/sentinel/sentinel.jpg)




### First setup

- ` ╰─> cd .ssh`
- ` ╰─> ssh-keygen -t rsa -b 4096` `sentinel`
- ` ╰─> ssh-copy-id -i ~/.ssh/sentinel.pub pi@8.0.0.4`
- `$ ssh pi@8.0.0.4`
- `$ sudo apt update && sudo apt upgrade -y`
- `$ sudo raspi-config`
- `$ sudo reboot +0`




### Installing necessary packages

- ` ╰─> vncserver -geometry 1920x1080`
- `$ sudo apt install apache2 curl exfat-fuse exfat-utils ffmpeg firefox-esr git glances gparted neofetch nload samba samba-common-bin speedtest-cli telegram-desktop terminator transmission wget youtube-dl zsh -y`
- `$ sudo apt install build-essential autoconf automake libtool gawk alien fakeroot dkms libblkid-dev uuid-dev libudev-dev libssl-dev zlib1g-dev libaio-dev libattr1-dev libelf-dev raspberrypi-kernel-headers python3 python3-dev python3-setuptools python3-cffi libffi-dev`
- `$ sudo apt install gcc cmake libncurses5 libncurses5-dev build-essential -y`



### Setup vnc-startup

*atheistd_startup.sh*
```
#!/bin/sh

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
now=$(date)
echo "$now" >> /home/pi/startup_time.txt
zpool import 2700552423667074417
```

- `% chmod +x atheistd_startup.sh`
- `% sud mv atheistd_startup.sh /etc/init.d/atheistd_startup/sh`
- `% sudo update-rc.d atheistd_startup.sh defaults`



### Compiling ZFS

- `$ git clone https://github.com/openzfs/zfs`
- `$ cd ./zfs`
- `$ git checkout master`
- `$ sh autogen.sh`
- `$ ./configure`
- `$ make -s -j$(nproc)`
- `$ sudo make install; sudo ldconfig; sudo depmod`
- `$ sudo systemctl enable zfs.target`
- `$ sudo reboot +0`




### Setup smb disks and directories' permissions

- `% sudo chmod 770 -R /heathen_nd`
- `% sudo usermod -a -G www-data pi`
- `% sudo chown -R -f pi:www-data /heathen_nd`


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
	path = /home/pi
	browseable = yes
	writeable = yes
	create mask = 0700
	directory mask = 0700
```

- `% sudo smbpasswd -a pi`




### `apache2` & `lighttpd` set-up

*/etc/apache2/ports.conf*
```
Listen 80
Listen 666
```

*/etc/apache2/ports.conf*
```
<Directory /heathen_nd>
	Options Indexes FollowSymLinks
	AllowOverride None
	Require all granted
</Directory>

<Directory /home/pi>
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
	DocumentRoot /home/pi
</VirtualHost>
```

*/etc/lighttpd/lighttpd.conf*
```
server.port = 200
```

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
