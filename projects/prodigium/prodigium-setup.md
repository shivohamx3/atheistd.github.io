# Setup *prodigium* ![prodigium! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/prodigium/prodigium-small.png)



### Ubuntu Server 20.04

- `╰─> cd .ssh`
- `╰─> ssh-copy-id -i ~/.ssh/prodigium.pub infidel@192.168.1.105`

- `$ sudo apt update && sudo apt upgrade -y`
- `$ sudo reboot +0`



### Installing necessary packages and preliminary setup

- `$ sudo apt install aria2 cmatrix curl ffmpeg hdparm htop libpam-google-authenticator nload openssh-server python3 python3-pip rar rsync smartmontools speedtest-cli exfat-fuse exfat-utils unrar unzip vim wget zfsutils-linux zip zsh -y`

- `$ sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl`
- `$ sudo chmod a+rx /usr/local/bin/youtube-dl`

- `$ pip3 install instalooter bpytop`
- `$ instalooter login`

- `$ sudo update-alternatives --config editor`

- `$ sudo reboot +0`



## ZFS related setup


##### ZFS parameters

*/etc/modprobe.d/zfs.conf*

```
options zfs zfs_scan_idle = 0
options zfs zfs_scrub_delay = 0
options zfs zfs_scan_min_time_ms = 5000
```

##### initial zpool and dataset creation

```
sudo zpool create -o ashift=12 grandis raidz2 /dev/sda /dev/sdb /dev/sdc /dev/sdd /dev/sde /dev/sdf /dev/sdg /dev/sdh

sudo zfs create grandis/personal
sudo zfs create grandis/work
sudo zfs create grandis/backup

sudo zfs create grandis/personal/torrents

sudo zfs create grandis/personal/media
sudo zfs create grandis/personal/media/movies
sudo zfs create grandis/personal/media/tv_series
sudo zfs create grandis/personal/media/camera_roll

sudo zfs create grandis/backup/ringmaster
sudo zfs create grandis/backup/flameboi
sudo zfs create grandis/backup/chief
sudo zfs create grandis/backup/phoenix
sudo zfs create grandis/backup/sentinel

sudo zfs create grandis/personal/zpesky

sudo zfs create grandis/work/ml_datasets
sudo zfs create grandis/work/nix_iso

sudo zpool export grandis

sudo zpool import    *trial run to get pool-id*
sudo zpool import -d /dev/disk/by-id <pool-id>
```

##### Setting dataset properties

```
sudo zfs set atime=off grandis
sudo zfs set checksum=sha512 grandis
sudo zfs set compression=zstd-19 grandis
sudo zfs set primarycache=all grandis
sudo zfs set recordsize=1M grandis
sudo zfs set snapdir=visible grandis
sudo zfs set xattr=sa grandis
```

##### Verify created pools

```
clear
zpool status -v
zfs list
```

##### Own mount points

```
sudo chmod 740 -vR /grandis
sudo chown infidel:infidel -vR /grandis
```



### cron job user script

*/grandis/chksums/calc_chksums.sh*

```
#!/usr/bin/env bash

/usr/bin/find /grandis/personal -type f -exec md5sum "{}" + > /grandis/chksums/chk_personal.txt
/usr/bin/find /grandis/work -type f -exec md5sum "{}" + > /grandis/chksums/chk_work.txt
/usr/bin/find /grandis/backup -type f -exec md5sum "{}" + > /grandis/chksums/chk_backup.txt

cd /grandis/chksums/
git add .
git commit -m "$(date)"
```



### `cron jobs`

 - `$ sudo crontab -e`

```
0 0 1,15 * * /usr/sbin/zpool scrub grandis
```

- `$ crontab -e`

```
0 0 10,20 * * /grandis/chksums/calc_chksums.sh
```



### Generate ssh keys for github and gitlab

- `$ eval "$(ssh-agent -s)"`
- `$ mkdir ~/.ssh`
- `$ chmod 700 ~/.ssh`
- `$ cd ~/.ssh`
- `$ ssh-keygen -t ed25519`&nbsp;&nbsp;&nbsp;&nbsp;*github, gitlab*

- `$ chsh -s /usr/bin/zsh infidel`



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

*/etc/pam.d/sshd*
```
auth required pam_google_authenticator.so
```

*/etc/ssh/sshd_config*
```
ChallengeResponseAuthentication yes
```

- `$ sudo systemctl restart sshd`



### SMB set-up

*/etc/samba/smb.conf*
```
[grandis]
	guest ok = no
	comment = grandis
	path = /grandis
	browseable = yes
	writeable = yes
	create mask = 0700
	directory mask = 0700
```

- `$ sudo smbpasswd -a infidel`
- `$ sudo systemctl restart smbd`



### Disable locale env forwarding on ssh

*/etc/ssh/ssh_config* **(comment the line out if you didn’t understand)**
```
# SendEnv LANG LC_*
```

