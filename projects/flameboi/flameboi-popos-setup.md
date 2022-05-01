# Setup *flameboi!* (Pop_OS) ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/flameboi/flameboi-small.png)

### Removing `snapd` and other junk.
- `$ sudo systemctl stop snapd.service`
- `$ sudo systemctl disable snapd.service`
- ```$ apt list --installed | grep gnome thunderbird aisleriot cheese deja-dup libreoffice rhythmbox remmina seahorse shotwell simple-scan```
- `$ sudo reboot`
- `$ sudo apt update && sudo apt upgrade`


### Installing necessary packages

- `$ sudo apt update && sudo apt upgrade -y`

- `$ sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target`
- `$ sudo passwd`
- `$ sudo apt install openssh-server -y`
- `$ sudo reboot`
### Installing [Brave Browser](https://brave-browser.readthedocs.io/en/latest/installing-brave.html#linux)
### `gnome` extensions
- `$ sudo apt install gnome-shell-extensions -y`
* [Chromium extension](https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep)


* [Vitals](https://extensions.gnome.org/extension/1460/vitals/)
* [Caffeine](https://extensions.gnome.org/extension/517/caffeine/)
> - Add `terminator`, `brave`, `transmission` and `firefox` to Caffeine
> - Turn on `Use higher precision` `Hide zero values` in Vitals
> - `Caffeine` `RunCat` `Vitals` `Simple net speed`
### Install necessary packages
- ```$ sudo apt install apache2 conky curl exfat-fuse exfat-utils ffmpeg fish git glances gnome-shell-extensions gparted handbrake htop libpam-google-authenticator nload samba samba-common-bin smartmontools speedtest-cli telegram-desktop terminator transmission wget youtube-dl zsh zfsutils-linux -y```




### Install necessary packages

- ```$ sudo apt install conky curl exfat-fuse exfat-utils ffmpeg fish git glances gnome-shell-extensions gparted handbrake htop libpam-google-authenticator nload smartmontools speedtest-cli telegram-desktop terminator transmission vim wget youtube-dl zfsutils-linux zsh fonts-firacode -y```
- `$ sudo zpool import `




### `git` config
- `$ git config --global credential.helper store`
- `$ git config --global core.editor vim`
- `$ git config --global user.name "YOUR NAME"`
- `$ git config --global user.email "YOUR EMAIL"`
- `$ chsh -s /usr/bin/fish atheistd`
- `$ git clone git@github.com:atheistd/fish_prompt ~/Documents/`

### 2FA for SSH
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
- `$ sudo vim /etc/pam.d/sshd`
> `auth required pam_google_authenticator.so`
- `$ sudo vim /etc/ssh/sshd_config`
<b>remove</b> `ChallengeResponseAuthentication no`
`ChallengeResponseAuthentication yes`
- `$ sudo systemctl restart sshd`




### Python, CUDA & cuDNN setup
* [Install CUDA and cuDNN on Pop!_os](https://support.system76.com/articles/cuda/)
* [Ubuntu 18.04: Install TensorFlow and Keras for Deep Learning](https://www.pyimagesearch.com/2019/01/30/ubuntu-18-04-install-tensorflow-and-keras-for-deep-learning/)
* [Install CUDA](https://gist.github.com/mikaelhg/cae5b7938aa3dfdf3d06a40739f2f3f4#file-cuda-install-md)
* [Official TensorFlow documentation on CUDA on Ubuntu 18.04](https://www.tensorflow.org/install/gpu#ubuntu_1804_cuda_101)
* [Install NVIDIA Graphics Drivers via apt-get](https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07#install-nvidia-graphics-driver-via-apt-get)
* [How to setup NVIDIA GPU laptop with Ubuntu for Deep Learning (CUDA and CuDNN)](https://lazyprogrammer.me/how-to-setup-nvidia-gpu-laptop-with-ubuntu-for-deep-learning-cuda-and-cudnn/)
* [Install the lastest NVIDIA Drivers on Ubuntu](https://www.maketecheasier.com/install-nvidia-drivers-ubuntu/)
* [Brisk guide to install TensorFlow GPU on Linux Machine](https://medium.com/@redowan/no-bullshit-guide-on-installing-tensorflow-gpu-ubuntu-18-04-18-10-238924cc4a6a)
