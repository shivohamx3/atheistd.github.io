# Setup *sentinel* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/sentinel/sentinel.jpg)

### First setup

- `$ ssh pi@8.0.0.4`
- `$ vncserver -geometry 1920x1080`
- `$ sudo apt update && sudo apt full-upgrade -y`
- `$ sudo passwd`
- `$ sudo raspi-config`
- `$ sudo reboot +0`



### Installing necessary packages

- `$ sudo apt install apache2 connectd curl exfat-fuse exfat-utils ffmpeg firefox-esr fish git glances gparted handbrake nload python3-pip python3-venv samba samba-common-bin speedtest-cli telegram-desktop transmission wget -y`
- `$ curl -sSL https://install.pi-hole.net | bash`
- `$ pihole -a -p`
<br>
- `$ git clone --depth 1 https://github.com/atheistd/setup ~/setup`
- `$ mkdir -p ~/.config/fish/`
- `$ mv ~/setup/sentinel/config.fish ~/.config/fish/`
- `$ mv ~/setup/sentinel/*.sh ~/`
- `$ chmod +x ~/.config/fish/config.fish`
- `$ fish`
- `$ source ~/.config/fish/config.fish`
- `% cd setup`
- `% chsh -s /usr/bin/fish`



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

