# Setup *sentinel* ![sentinel! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/sentinel/sentinel.jpg)



### First setup + disabling `snapd`

- `╰─> ssh-copy-id -i ~/.ssh/sentinel.pub ubuntu@192.168.1.104`

- `$ sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target`
- `$ echo "sentinel" | sudo tee /etc/hostname`
- `$ echo "127.0.1.1 sentinel" | sudo tee -a /etc/hosts`
- `$ sudo timedatectl set-timezone Asia/Kolkata`
- `$ sudo reboot +0`
- `$ sudo apt update && sudo apt upgrade -y`
- `$ sudo reboot +0`



### Installing necessary packages and preliminary setup

- [PlexMediaServer](https://support.plex.tv/articles/235974187-enable-repository-updating-for-supported-linux-server-distributions/)
- `$ sudo apt update`

- `$ sudo apt install apache2 aria2 cmatrix curl exfat-fuse exfat-utils ffmpeg git glances hdparm htop iotop libpam-google-authenticator nload openssh-server plexmediaserver python3 python3-pip rsync samba samba-common-bin smartmontools speedtest-cli transmission-cli transmission-common transmission-daemon unrar unzip vim wget zfsutils-linux zip zsh -y`

- `$ sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl`
- `$ sudo chmod a+rx /usr/local/bin/youtube-dl`

- `$ pip3 install instalooter bpytop`
- `$ instalooter login`

- `$ sudo update-alternatives --config editor`

- `$ sudo reboot +0`

- `$ eval "$(ssh-agent -s)"`
- `$ cd ~/.ssh/ && ssh-keygen -t ed25519 `&nbsp;&nbsp;&nbsp;&nbsp;*github, gitlab*
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

sudo zfs create libertine/zpesky

```

```
sudo zfs set atime=off libertine
sudo zfs set compression=on libertine
sudo zfs set compression=gzip libertine/zpesky
sudo zfs set primarycache=all libertine
sudo zfs set recordsize=1M libertine
sudo zfs set snapdir=visible libertine
sudo zfs set xattr=sa libertine

```

- `$ sudo usermod -aG ubuntu plex`
- `$ sudo chmod 755 -R /libertine && sudo chown ubuntu:www-data -R /libertine`
- `$ sudo reboot +0`



### Setup pi-hole + unbound

- `$ curl -sSL https://install.pi-hole.net | bash`
- `$ sudo apt install unbound -y` (unbound installation will fail as pihole-FTL is already running on port 53)
- `$ pihole -a -p`

*/etc/unbound/unbound.conf.d/pi-hole.conf*

```
server:
    # If no logfile is specified, syslog is used
    # logfile: "/var/log/unbound/unbound.log"
    verbosity: 0

    interface: 127.0.0.1
    port: 5335
    do-ip4: yes
    do-udp: yes
    do-tcp: yes

    # May be set to yes if you have IPv6 connectivity
    do-ip6: no

    # You want to leave this to no unless you have *native* IPv6. With 6to4 and
    # Terredo tunnels your web browser should favor IPv4 for the same reasons
    prefer-ip6: no

    # Use this only when you downloaded the list of primary root servers!
    # If you use the default dns-root-data package, unbound will find it automatically
    #root-hints: "/var/lib/unbound/root.hints"

    # Trust glue only if it is within the server's authority
    harden-glue: yes

    # Require DNSSEC data for trust-anchored zones, if such data is absent, the zone becomes BOGUS
    harden-dnssec-stripped: yes

    # Don't use Capitalization randomization as it known to cause DNSSEC issues sometimes
    # see https://discourse.pi-hole.net/t/unbound-stubby-or-dnscrypt-proxy/9378 for further details
    use-caps-for-id: no

    # Reduce EDNS reassembly buffer size.
    # Suggested by the unbound man page to reduce fragmentation reassembly problems
    edns-buffer-size: 1472

    # Perform prefetching of close to expired message cache entries
    # This only applies to domains that have been frequently queried
    prefetch: yes

    # One thread should be sufficient, can be increased on beefy machines. In reality for most users running on small networks or on a single machine, it should be unnecessary to seek performance enhancement by increasing num-threads above 1.
    num-threads: 1

    # Ensure kernel buffer is large enough to not lose messages in traffic spikes
    so-rcvbuf: 1m

    # Ensure privacy of local IP ranges
    private-address: 192.168.0.0/16
    private-address: 169.254.0.0/16
    private-address: 172.16.0.0/12
    private-address: 10.0.0.0/8
    private-address: fd00::/8
    private-address: fe80::/10
```

- `$ sudo service unbound restart`

- Goto [pi-hole dashbord](http://192.168.1.104:200/admin/groups-domains.php?type=white) and add `s.youtube.com` to Whitelist.

- `$ sudo reboot +0`


### 2FA for ssh

- `$ google-authenticator`


> `Do you want authentication tokens to be time-based (y/n) y`


> `Do you want me to update your "/home/pi/.google_authenticator" file? (y/n) y`


> `Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases
your chances to notice or even prevent man-in-the-middle attacks (y/n) y`


> `By default, a new token is generated every 30 seconds by the mobile app.
In order to compensate for possible time-skew between the client and the server,
we allow an extra token before and after the current time. This allows for a
time skew of up to 30 seconds between authentication server and client. If you
experience problems with poor time synchronization, you can increase the window
from its default size of 3 permitted codes (one previous code, the current
code, the next code) to 17 permitted codes (the 8 previous codes, the current
code, and the 8 next codes). This will permit for a time skew of up to 4 minutes
between client and server.
Do you want to do so? (y/n) n`


> `If the computer that you are logging into isn't hardened against brute-force
login attempts, you can enable rate-limiting for the authentication module.
By default, this limits attackers to no more than 3 login attempts every 30s.
Do you want to enable rate-limiting? (y/n) y`

- `$ echo 'auth required pam_google_authenticator.so' | sudo tee -a /etc/pam.d/sshd`

*/etc/ssh/sshd_config*
```
ChallengeResponseAuthentication yes
```

- `$ sudo systemctl restart sshd`



### SMB set-up

*/etc/samba/smb.conf*
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

*/etc/apache2/ports.conf*
(DON'T INCLUDE PORT 200 as this file is `apache` specific)
```
Listen 80
Listen 666
```

*/etc/apache2/apache2.conf*
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

*/etc/apache2/sites-available/000-default.conf*
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

*/etc/lighttpd/lighttpd.conf*
```
server.port = 200
```

- `$ sudo /etc/init.d/lighttpd restart` (lighttpd)
- `$ sudo systemctl restart apache2` (apache2)



### `transmission-cli + remote`

- `$ sudo service transmission-daemon stop`
- `$ sudo usermod -aG ubuntu debian-transmission`

*/var/lib/transmission-daemon/info/settings.json*

```
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
```

- `$ sudo service transmission-daemon start`
- `$ transmission-remote -n 'transmission:transmission' -si`



### Set startup script

- `$ sudo crontab -e`
```
0 0 1,15 * * /usr/sbin/zpool scrub libertine
0 * * * * /usr/bin/rsync --recursive --size-only /var/lib/transmission-daemon/.config/transmission-daemon/torrents/*.* /libertine/config_dir/
```

- `$ crontab -e`
```
0 * * * * /usr/bin/rsync --recursive --size-only /home/ubuntu/.config/transmission/torrents/*.* /libertine/personal/config_dir
```


### Disable locale env forwarding on ssh

*/etc/ssh/ssh_config*

```
# SendEnv LANG LC_*
```
(comment the line out if you didn't understand)



### Plex setup

- In the [web UI](http://192.168.1.104:32400/web),, go to Settings -> Network -> *List of IP addresses and networks that are allowed without auth* and enter `192.168.1.0/24`.
- Now in the web UI, under Settings -> Scheduled Tasks, set the *Backup Directory* to `/libertine/backup/sentinel/plexmediaserver/common/Library/Application\ Support/Plex\ Media\ Server/Plug-in\ Support/Databases/`



### [remote.it](http://remote.it/) set-up

- `$ curl -LkO https://raw.githubusercontent.com/remoteit/installer/master/scripts/auto-install.sh; chmod +x ./auto-install.sh; sudo ./auto-install.sh`
- `$ sudo connectd_installer`
