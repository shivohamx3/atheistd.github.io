# Setup *sentinel* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/sentinel/sentinel.jpg)

### First setup

- `$ ssh ubuntu@8.0.0.4`
- `$ sudo reboot +0`
- `$ snap list`
- `$ snap remove <packages>`
- `$ sudo apt autoremove --purge snapd`
- `$ sudo apt update && sudo apt full-upgrade`
- `$ sudo reboot +0`
- ` ╰─> ssh-keygen -t rsa -b 4096`
- ` ╰─> scp ~/.ssh/id_rsa.pub ubuntu@8.0.0.4:/home/ubuntu/.ssh/ringmaster.pub`
- `$ cd .ssh && cat ringmaster.pub >> authorized_keys`



### Installing `xfce`

- `$ sudo apt install xfce4 xfce4-goodies`
- `$ sudo apt install tightvncserver`
- `$ sudo reboot +0`
- `$ vncserver -geometry 1920x1080`
- `$ vncserver -kill :1`
- `$ mv ~/.vnc/xstartup ~/.vnc/xstartup.bak`
- `$ nano ~/.vnc/xstartup`
- ```
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &```
- `$ sudo chmod +x ~/.vnc/xstartup`
- `$ vncserver -geometry 1920x1080`
- `$ sudo passwd`
- `$ sudo reboot +0`



### Installing necessary packages

- `$ vncserver -geometry 1920x1080`
- `$ sudo apt install apache2 chromium-browser curl exfat-fuse exfat-utils ffmpeg firefox fish git glances gparted nload samba samba-common-bin speedtest-cli telegram-desktop transmission wget`
- `$ curl -sSL https://install.pi-hole.net | bash`
- `$ pihole -a -p`
<br>
- `% chsh -s /usr/bin/fish`
- `$ git clone --depth 1 https://github.com/atheistd/setup ~/setup`
- `$ mkdir -p ~/.config/fish/`
- `$ mv ~/setup/sentinel/config.fish ~/.config/fish/`
- `$ mv ~/setup/sentinel/*.sh ~/`
- `$ chmod +x ~/.config/fish/config.fish`
- `$ fish`
- `$ source ~/.config/fish/config.fish`
- `% cd setup`



### Setup smb disks and directories' permissions

- `% cd /media && sudo mkdir heathenDisk`
- `% mdisk`
- `% sudo chmod 777 -R /media/`
- `% sudo chmod 777 -R /home/pi`



### Setup vnc-startup & grant read-only permission to `apache`

- `% cd && sudo chmod -v u=rwx,g=rx,o=r init.sh pi_init.sh`
- `% mkdir init`
- `% mv init.sh init/init.sh`
- `% sudo mv pi_init.sh /etc/init.d/pi_init.sh`
- `% sudo update-rc.d pi_init.sh defaults`



### SMB set-up

- `% sudo nano /etc/samba/smb.conf`
> `[heathenDisk]`<br>
> 	`guest ok = no`<br>
>	`comment = heathenDisk`<br>
>	`path = /media/heathenDisk`<br>
>	`browseable = yes`<br>
>	`writeable = yes`<br>
>	`create mask = 0700`<br>
>	`directory mask = 0700`<br>
>	`spotlight = yes`<br>
>	`vfs objects = catia fruit streams_xattr`<br>
>	`fruit:aapl = yes`<br>
<br>
>`[pi]`<br>
>	`guest ok = no`<br>
>	`comment = d-home`<br>
>	`path = /home/pi`<br>
>	`browseable = yes`<br>
>	`writeable = yes`<br>
>	`create mask = 0700`<br>
>	`directory mask = 0700`<br>
>	`vfs objects = catia fruit streams_xattr`<br>
>	`fruit:aapl = yes`<br>

- `% sudo smbpasswd -a pi`



### `apache2` & `lighttpd` set-up

- `% sudo nano /etc/apache2/ports.conf`
> `Listen 80`<br>
> `Listen 666`

- `% sudo nano /etc/apache2/apache2.conf`
>`<Directory /media/heathenDisk>`<br>
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

- `% sudo nano /etc/apache2/sites-available/000-default.conf`
>`<VirtualHost *:80>`<br>
>	`ServerAdmin webmaster@localhost`<br>
>	`DocumentRoot /media/heathenDisk`<br>
>`</VirtualHost>`
>
>`<VirtualHost *:666>`<br>
>	`ServerAdmin webmaster@localhost`<br>
>	`DocumentRoot /home/pi`<br>
>`</VirtualHost>`<br>

- `% sudo nano /etc/lighttpd/lighttpd.conf`
>`server.port = 200`

- `% rapached && rsmbd && rlighttpd`



### Setup python environment

- `% python3 -m venv custom`
- `% startpy`
- `% pip3 install numpy gpiozero RPi.GPIO matplotlib ipython`



### [remote.it](http://remote.it/) set-up

- `% sudo connectd_installer`



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

