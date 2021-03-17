# Setup *flameboi!* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/flameboi/flameboi-small.png)



### UPDATE!!!

- `$ sudo apt update && sudo apt upgrade -y`



### Swap

- `$ sudo dd if=/dev/zero of=/swapfile bs=1M count=74088185856 status=progress`
- `$ sudo chmod 600 /swapfile`
- `$ sudo mkswap /swapfile`
- `$ sudo swapon /swapfile`
- `$ echo '/swapfile none swap defaults 0 0' | sudo tee -a /etc/fstab` 
- `$ sudo apt install uswsusp -y`
- `$ sudo dpkg-reconfigure -pmedium uswsusp`
- `$ sudo s2disk`



### Installing [Brave Browser](https://brave.com/linux/)



### gnome extensions

- `$ sudo apt install gnome-shell-extensions -y`
* [Simple net speed](https://extensions.gnome.org/extension/1085/simple-net-speed/)



### Installing packages

- `$ sudo apt install adb aria2 cmatrix curl dolphin exfat-fuse exfat-utils ffmpeg firefox flatpak fonts-firacode git handbrake hdparm htop libpam-google-authenticator neofetch nload openssh-server python3 python3-pip qemu rar rsync smartmontools speedtest-cli telegram-desktop terminator transmission unrar unzip vim vlc wget zfsutils-linux zip zsh ncdu -y`

- `$ sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl`
- `$ sudo chmod a+rx /usr/local/bin/youtube-dl`

- `$ pip3 install instalooter bpytop`
- `$ instalooter login`

- `$ sudo zpool import`



### Making `terminator` default terminal emulator

 - `$ gsettings set org.gnome.desktop.default-applications.terminal exec '/usr/bin/terminator'`
 - `$ sudo update-alternatives --config x-terminal-emulator`



### Generate ssh keys

- `$ cd ~/.ssh`
- `$ ssh-keygen -t ed25519 `&nbsp;&nbsp;&nbsp;&nbsp;*github, gitlab, sentinel, prodigium*
- `$ chsh -s /usr/bin/zsh atheistd`



### git config

- `$ git config --global credential.helper store`
- `$ git config --global core.editor vim`
- `$ git config --global user.name "YOUR NAME"`
- `$ git config --global user.email "YOUR EMAIL"`



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



### Python, CUDA & cuDNN setup
* [Install CUDA and cuDNN on Pop!_os](https://support.system76.com/articles/cuda/)
* [Ubuntu 18.04: Install TensorFlow and Keras for Deep Learning](https://www.pyimagesearch.com/2019/01/30/ubuntu-18-04-install-tensorflow-and-keras-for-deep-learning/)
* [Install CUDA](https://gist.github.com/mikaelhg/cae5b7938aa3dfdf3d06a40739f2f3f4#file-cuda-install-md)
* [Official TensorFlow documentation on CUDA on Ubuntu 18.04](https://www.tensorflow.org/install/gpu#ubuntu_1804_cuda_101)
* [Install NVIDIA Graphics Drivers via apt-get](https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07#install-nvidia-graphics-driver-via-apt-get)
* [How to setup NVIDIA GPU laptop with Ubuntu for Deep Learning (CUDA and CuDNN)](https://lazyprogrammer.me/how-to-setup-nvidia-gpu-laptop-with-ubuntu-for-deep-learning-cuda-and-cudnn/)
* [Install the lastest NVIDIA Drivers on Ubuntu](https://www.maketecheasier.com/install-nvidia-drivers-ubuntu/)
* [Brisk guide to install TensorFlow GPU on Linux Machine](https://medium.com/@redowan/no-bullshit-guide-on-installing-tensorflow-gpu-ubuntu-18-04-18-10-238924cc4a6a)
