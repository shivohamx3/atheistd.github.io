# Setup *sentinel* ![sentinel! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/sentinel/sentinel.jpg)



### First setup + disabling `snapd`

- `╰─> ssh-copy-id -i ~/.ssh/sentinel.pub ubuntu@192.168.1.104`

- `$ sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target`
- `$ sudo systemctl disable snapd`
- `$ echo "sentinel" | sudo tee /etc/hostname`
- `$ echo "127.0.1.1 sentinel" | sudo tee -a /etc/hosts`
- `$ sudo timedatectl set-timezone Asia/Kolkata`

> */boot/firmware/usercfg.txt* (Ubuntu) OR */boot/firmware/config.txt* (Pop)

```
hdmi_force_hotplug=1
disable_overscan=1

over_voltage=6
arm_freq=2000
gpu_freq=600
```

- `$ sudo reboot +0`
- `$ sudo apt update && sudo apt upgrade -y`
- `$ sudo reboot +0`



### SSH Setup

> */etc/locale.gen*

Uncomment the line `en_US.UTF-8 UTF-8`

 - `$ sudo locale-gen`

 > */etc/ssh/sshd_config*

Replace `AcceptEnv LANG LC_*` to `AcceptEnv no`
Change `Port 22` to `Port <check in $HOME/.ssh/config>`

 - `$ sudo systemctl restart ssh`



### Installing necessary packages and preliminary setup

- `$ sudo apt update`
- `$ sudo apt install apache2 aria2 cmatrix curl exfat-fuse exfat-utils ffmpeg git glances hdparm htop iotop libpam-google-authenticator nload openssh-server python3 python3-pip rsync samba samba-common-bin smartmontools speedtest-cli transmission-cli transmission-common transmission-daemon unrar unzip vim wget zfsutils-linux zip zsh -y`


- `$ sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp`
- `$ sudo chmod a+rx /usr/local/bin/yt-dlp`

- `$ sudo update-alternatives --set editor /usr/bin/vim.basic`

- `$ sudo reboot +0`

- `$ eval "$(ssh-agent -s)"`
- `$ cd ~/.ssh/ && ssh-keygen -t ed25519`&nbsp;&nbsp;&nbsp;&nbsp;*github, gitlab*
- `$ ssh-add ~/.ssh/github`
- `$ ssh-add ~/.ssh/gitlab`

- `$ git config --global credential.helper store`
- `$ git config --global core.editor vim`
- `$ git config --global user.name "YOUR NAME"`
- `$ git config --global user.email "YOUR EMAIL"`



### Everything ZFS & disk related

```
sudo zfs create libertine/torrents
sudo zfs create libertine/torrents/.incomplete

sudo zfs create libertine/media
sudo zfs create libertine/media/movies
sudo zfs create libertine/media/tv_series
sudo zfs create libertine/media/camera_roll
```

```
sudo zfs set atime=off libertine
sudo zfs set compression=zstd-3 libertine
sudo zfs set primarycache=all libertine
sudo zfs set recordsize=1M libertine
sudo zfs set snapdir=visible libertine
sudo zfs set xattr=sa libertine
```

- `$ sudo usermod -aG ubuntu debian-transmission`
- `$ sudo chmod 755 -R /libertine && sudo chown ubuntu:www-data -R /libertine`
- `$ sudo reboot +0`



### Setup pi-hole + unbound

- `$ git clone --depth=1 https://github.com/pi-hole/pi-hole.git Pi-hole`
- `$ cd "Pi-hole/automated install/"`
- `$ sudo bash basic-install.sh`

- `$ sudo apt install unbound -y` (unbound installation will fail as pihole-FTL is already running on port 53)
- `$ pihole -a -p`

> */etc/unbound/unbound.conf.d/pi-hole.conf*

```
server:

	verbosity: 0

	interface: 127.0.0.1
	port: 5335
	do-ip4: yes
	do-udp: yes
	do-tcp: yes


	do-ip6: no
	prefer-ip6: no

	harden-glue: yes
	arden-dnssec-stripped: yes

	use-caps-for-id: no

	dns-buffer-size: 1472
	refetch: yes
	um-threads: 1

	o-rcvbuf: 1m

	private-address: 192.168.0.0/16
	private-address: 169.254.0.0/16
	private-address: 172.16.0.0/12
	private-address: 10.0.0.0/8
	private-address: fd00::/8
	private-address: fe80::/10
```

- `$ sudo service unbound restart`

- Goto pi-hole dashbord and add `s.youtube.com` to Whitelist.

- `$ sudo reboot +0`


### 2FA for ssh

- `$ google-authenticator`


> Do you want authentication tokens to be time-based (y/n) `y`


> Do you want me to update your "/home/pi/.google_authenticator" file? (y/n) `y`


> Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases
your chances to notice or even prevent man-in-the-middle attacks (y/n) `y`


> By default, a new token is generated every 30 seconds by the mobile app.
In order to compensate for possible time-skew between the client and the server,
we allow an extra token before and after the current time. This allows for a
time skew of up to 30 seconds between authentication server and client. If you
experience problems with poor time synchronization, you can increase the window
from its default size of 3 permitted codes (one previous code, the current
code, the next code) to 17 permitted codes (the 8 previous codes, the current
code, and the 8 next codes). This will permit for a time skew of up to 4 minutes
between client and server.
Do you want to do so? (y/n) `n`


> If the computer that you are logging into isn't hardened against brute-force
login attempts, you can enable rate-limiting for the authentication module.
By default, this limits attackers to no more than 3 login attempts every 30s.
Do you want to enable rate-limiting? (y/n) `y`

- `$ echo 'auth required pam_google_authenticator.so' | sudo tee -a /etc/pam.d/sshd`

> */etc/ssh/sshd_config*

```
ChallengeResponseAuthentication yes
```

- `$ sudo systemctl restart ssh`



### SMB set-up

> */etc/samba/smb.conf*

```
[libertine]
	guest ok = no
	comment = libertine
	path = /libertine
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
- `$ sudo systemctl restart smbd`



### Web servers' set-up

> */etc/apache2/ports.conf*

(DON'T INCLUDE PORT 200 as this file is `apache` specific)
```
Listen 80
Listen 666
```

> */etc/apache2/apache2.conf*

```
<Directory /libertine>
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

> */etc/apache2/sites-available/000-default.conf*

```
<VirtualHost *:80>
	ServerAdmin webmaster@localhost
	DocumentRoot /libertine
</VirtualHost>

<VirtualHost *:666>
	ServerAdmin webmaster@localhost
	DocumentRoot /home/ubuntu
</VirtualHost>
```

> */etc/lighttpd/lighttpd.conf*

```
server.port = 200
```

- `$ sudo /etc/init.d/lighttpd restart` (lighttpd)
- `$ sudo systemctl restart apache2` (apache2)



### `transmission-cli + remote`

- `$ sudo service transmission-daemon stop`

> */var/lib/transmission-daemon/info/settings.json*

```
[...]
	"rpc-whitelist": "127.0.0.1,10.0.0.*",
[...]
	"umask": 2,
[...]
	"download-dir": "/libertine/personal/torrents",
	"download-limit": 500,
[...]
	"incomplete-dir": "/libertine/personal/torrents/.incomplete"
	"incomplete-dir-enabled": true,
[...]
	"download-queue-size": 10,
[...]
```

- `$ sudo service transmission-daemon start`
- `$ transmission-remote -n 'transmission:transmission' -si`


### Set startup script

- `$ crontab -e`

```
0 */2 * * * pihole -up
```

- `$ sudo crontab -e`

```
@reboot /home/ubuntu/scripts/transmission.py

0 0 1,2,3 * * curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
0 0 1,2,3 * * chmod a+rx /usr/local/bin/yt-dlp

0 0 1,14 * * /usr/bin/systemctl stop transmission-daemon.service
1 0 * * * /usr/bin/rsync --recursive --size-only /var/lib/transmission-daemon/.config/transmission-daemon/torrents/*.* /libertine/config_dir
2 0 * * * /usr/bin/chmod 774 -R /libertine && /usr/bin/chown ubuntu:www-data -R /libertine && /usr/bin/find /libertine -type f -exec chmod 660 {} \; && /usr/bin/find /libertine -type f -name "*.DS_Store" -exec rm {} \;
20 0 1,14 * * /usr/sbin/zpool scrub libertine

40 7 * * 1,2,3,4 /usr/bin/systemctl stop transmission-daemon.service
10 17 * * 1,2,3,4 /usr/bin/systemctl restart transmission-daemon.service
```

- `$ crontab -e`

```
0 * * * * /usr/bin/rsync --recursive --size-only /home/ubuntu/.config/transmission/torrents/*.* /libertine/personal/config_dir
```


### Disable locale env forwarding on ssh

> */etc/ssh/ssh_config*

```
# SendEnv LANG LC_*
```
(comment the line out if you didn't understand)



### [remote.it](http://remote.it/) set-up

- `$ curl -LkO https://raw.githubusercontent.com/remoteit/installer/master/scripts/auto-install.sh; chmod +x ./auto-install.sh; sudo ./auto-install.sh`
- `$ sudo connectd_installer`
