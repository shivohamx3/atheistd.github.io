# Setup *prodigium* ![prodigium! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/prodigium/prodigium-small.png)

### Ubuntu Server 20.04

- `╰─> cd .ssh`
- `╰─> ssh-copy-id -i ~/.ssh/prodigium.pub infidel@192.168.1.105`

- `$ sudo apt update && sudo apt upgrade -y`
*/etc/hostname*
```
prodigium
```
*/etc/hosts*
```
127.0.1.1 prodigium.localdomain prodigium
```

- `$ sudo reboot +0`



### Install necessary packages

- `$ sudo apt install aria2 cmatrix curl ffmpeg fonts-firacode hdparm htop libpam-google-authenticator nload openssh-server python3 python3-pip rar rsync smartmontools speedtest-cli unrar unzip vim wget zfsutils-linux zip zsh -y`

- `$ sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl`
- `$ sudo chmod a+rx /usr/local/bin/youtube-dl`

- `$ pip3 install instalooter bpytop`
- `$ instalooter login`



### ZFS related setup

- `$ sudo zpool import`
- `$ sudo zpool import <pool-id>`
- `$ sudo chmod 770 -R /grandis`
- `$ sudo chown -R infidel:infidel /grandis`
- `$ `
- `$ `
- `$ `
- `$ `



### Generate ssh keys for 

- `$ eval "$(ssh-agent -s)"`
- `$ mkdir ~/.ssh`
- `$ chmod 700 ~/.ssh`
- `$ cd ~/.ssh`
- `$ ssh-keygen -t ed25519`
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

- `$ `
- `$ `
- `$ `
- `$ `
- `$ `
- `$ `
- `$ `
- `$ `
- `$ `
- `$ `
- `$ `

