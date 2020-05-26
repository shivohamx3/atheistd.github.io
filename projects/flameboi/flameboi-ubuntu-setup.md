# Setup *flameboi!* (Ubuntu 18.04) ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/flameboi/flameboi-small.png)

### Removing `snapd` and other junk.

- `$ sudo apt autoremove --purge snapd -y `
- ```$ apt list --installed | grep gnome thunderbird aisleriot cheese deja-dup libreoffice rhythmbox remmina seahorse shotwell simple-scan```
- `$ sudo reboot`
- `$ sudo apt update && sudo apt upgrade`
- `$ sudo passwd`
- `$ sudo apt install openssh-server -y`
- `$ sudo reboot`



### Installing [Brave Browser](https://brave-browser.readthedocs.io/en/latest/installing-brave.html#linux)



### `gnome` extensions

- `$ sudo apt install gnome-shell-extensions -y`
* [Chromium extension](https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep)
* [RunCat](https://extensions.gnome.org/extension/2986/runcat/)
* [Simple net speed](https://extensions.gnome.org/extension/1085/simple-net-speed/)
* [Vitals](https://extensions.gnome.org/extension/1460/vitals/)
* [Caffeine](https://extensions.gnome.org/extension/517/caffeine/)

> - Add `terminator`, `brave`, `transmission` and `firefox` to Caffeine
> - Turn on `Use higher precision` `Hide zero values` in Vitals
> - `Caffeine` `RunCat` `Vitals` `Simple net speed`



### Install necessary packages

- ```$ sudo apt install apache2 conky curl exfat-fuse exfat-utils ffmpeg fish git glances gnome-shell-extensions gparted handbrake htop nload samba samba-common-bin speedtest-cli telegram-desktop terminator transmission wget```
<br>[remote.it](http://remote.it) ⤵
- `$ curl -LkO https://raw.githubusercontent.com/remoteit/installer/master/scripts/auto-install.sh`
- `$ chmod +x ./auto-install.sh`
- `$ sudo ./auto-install.sh`
- `$ sudo connectd_installer`
- [`conky` tutorial](https://www.youtube.com/watch?v=QB8cjKpdVQY&t=619s) - [`conky` theme](https://www.deviantart.com/seajey/art/Conky-Seamod-v0-1-283461046)



### `git` config

- `$ git config --global credential.helper store`
- `$ git config --global core.editor nano`
- `$ git config --global user.name "YOUR NAME"`
- `$ git config --global user.email "YOUR EMAIL"`
- `$ chsh -s $(which fish) $whoami`
- `$ git clone --depth 1 https://github.com/atheistd/setup ~/setup`
- `$ mkdir -p ~/.config/fish/`
- `$ mv ~/setup/sentinel/config.fish ~/.config/fish/ && chmod +x ~/.config/fish/config.fish`
- `$ mv ~/setup/flameboi/*.fish ~/.config/fish/config.fish && chmod +x ~/.config/fish/*.fish`
- `$ fish`



### `e-mail` client

- [Mailspring](https://getmailspring.com/download)



### Python, CUDA & cuDNN setup

* [Install CUDA and cuDNN on Pop!_os](https://support.system76.com/articles/cuda/)
* [Ubuntu 18.04: Install TensorFlow and Keras for Deep Learning](https://www.pyimagesearch.com/2019/01/30/ubuntu-18-04-install-tensorflow-and-keras-for-deep-learning/)
* [Install CUDA](https://gist.github.com/mikaelhg/cae5b7938aa3dfdf3d06a40739f2f3f4#file-cuda-install-md)
* [Official TensorFlow documentation on CUDA on Ubuntu 18.04](https://www.tensorflow.org/install/gpu#ubuntu_1804_cuda_101)
* [Install NVIDIA Graphics Drivers via apt-get](https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07#install-nvidia-graphics-driver-via-apt-get)
* [How to setup NVIDIA GPU laptop with Ubuntu for Deep Learning (CUDA and CuDNN)](https://lazyprogrammer.me/how-to-setup-nvidia-gpu-laptop-with-ubuntu-for-deep-learning-cuda-and-cudnn/)
* [Install the lastest NVIDIA Drivers on Ubuntu](https://www.maketecheasier.com/install-nvidia-drivers-ubuntu/)
* [Brisk guide to install TensorFlow GPU on Linux Machine](https://medium.com/@redowan/no-bullshit-guide-on-installing-tensorflow-gpu-ubuntu-18-04-18-10-238924cc4a6a)



### macOS emulator [*Darling*](https://www.darlinghq.org/)



### `sudo apt clean`
