# Setup *flameboi!* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/flameboi/flameboi-small.png)



### UPDATE!!!

- **set DNS to pi-hole server**

- `$ sudo apt update`
- `$ sudo systemctl unmask nvidia-suspend nvidia-hibernate nvidia-resume`
- `$ sudo systemctl enable nvidia-suspend nvidia-hibernate nvidia-resume`
- `$ sudo apt remove "*nvidia"`
- `$ sudo apt install system76-driver-nvidia -y`
- `$ sudo apt upgrade -y`
- Reboot



### Installing [Brave Browser](https://brave.com/linux/)



### [VNC](https://www.realvnc.com/en/connect/download/viewer/)



### [Sublime Text 3](https://www.sublimetext.com/docs/3/linux_repositories.html)

- [SublimeJEDI](https://packagecontrol.io/packages/Jedi%20-%20Python%20autocompletion)
- [TwoDark](https://packagecontrol.io/packages/Theme%20-%20TwoDark)

- Preferences > Settings

```
	"font_face": "Fira Code",
	"font_options":["subpixel_antialias"],
	"atomic_save": true,
	"auto_complete_delay": 1,
	"caret_extra_width": 1,
	"color_scheme": "Packages/Theme - TwoDark/TwoDark.tmTheme",
	"draw_shadows": false,
	"ensure_newline_at_eof_on_save": true,
	"fade_fold_buttons": true,
	"highlight_modified_tabs": true,
	"ignored_packages":["Vintage"],
	"indent_guide_options":["draw_active"],
	"save_on_focus_lost": true,
	"shift_tab_unindent": true,
	"show_encoding": true,
	"show_line_endings": true,
	"theme": "TwoDark.sublime-theme",
	"auto_complete_triggers": [{"selector": "source.python", "characters": "."}],
```

- Preferences > Key Bindings

```
	{"keys": ["ctrl+tab"], "command": "next_view"},
	{"keys": ["ctrl+shift+tab"], "command": "prev_view"},
```



### gnome extensions

- `$ sudo apt install gnome-shell-extensions -y`
* [Simple net speed](https://extensions.gnome.org/extension/1085/simple-net-speed/)
* [BackSlide](https://extensions.gnome.org/extension/543/backslide/)



### Installing necessary packages and preliminary setup

- `$ sudo apt install adb alacritty aria2 bash brave-browser breeze-cursor-theme bspwm cifs-utils cmatrix curl dolphin dunst exfat-fuse exfat-utils fastboot feh ffmpeg firefox flatpak fonts-firacode fonts-fork-awesome git google-chrome-stable handbrake hdparm htop i3lock i3lock-fancy iotop iperf jq lemonbar libnotify-bin libpam-google-authenticator libxcb-ewmh2 mediainfo mpv neofetch nload obs-plugins obs-studio openssh-server pcmanfm picom polybar python3 python3-pip python3-tk python3-venv qemu qemu-efi-aarch64 qemu-efi-arm qemu-system-arm qemu-system-x86 rar rofi rsync smartmontools socat speedtest-cli sublime-text sxhkd terminator tmux unrar unzip vim virt-manager virtualbox vlc wget xdo xorg zfsutils-linux zip zsh -y`
- `$ flatpak install flathub com.bitwarden.desktop`

- `$ sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl`
- `$ sudo chmod a+rx /usr/local/bin/youtube-dl`

- `$ pip3 install bpytop`
- `$ pip3 install instalooter`

- `$ sudo update-alternatives --set editor /usr/bin/vim.basic`
- `$ sudo zpool import`

##### virtualization-related steps

- `$ sudo adduser $USER vboxusers`
- `$ sudo adduser $USER libvirt`
- `$ sudo adduser $USER kvm`

*/etc/libvirt/qemu.conf*

```
user = "atheistd"
[...]
roup = "atheistd"

```

- `$ sudo systemctl restart libvirtd`



### Making `terminator` default terminal emulator

 - `$ gsettings set org.gnome.desktop.default-applications.terminal exec '/usr/bin/terminator'`
 - `$ sudo update-alternatives --config x-terminal-emulator`
 - `$ gsettings set org.gnome.desktop.interface clock-show-date true; gsettings set org.gnome.desktop.interface clock-show-seconds true; gsettings set org.gnome.desktop.interface clock-show-weekday true`



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

- `$ echo 'auth required pam_google_authenticator.so' | sudo tee -a /etc/pam.d/sshd`

> */etc/ssh/sshd_config*

```
ChallengeResponseAuthentication yes
```

- `$ sudo systemctl restart sshd`



### OBS NVENC plugin(s)

 - [StreamFX](https://obsproject.com/forum/resources/streamfx-for-obs-studio.578/updates)



### Python

- **REBOOT**

- `$ cd $HOME && python3 -m venv deeplearning`
- `$ startpy`
- `$ pip3 install --upgrade pip`
- `$ pip3 install pip-review`
- `$ pip-review --interactive`
- `$ deactivate`
- `$ apt search cuda`
- `$ sudo apt install` (check which version is compatible with &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [torch](https://pytorch.org/get-started/locally/)) (**use at-least 11.1, 10.2 will not work well will NV 30XX**)
- `$ startpy`
- `$ pip3 install` [insert torch packages here] `ipython jupyter jupyterlab keras matplotlib nnfs numpy opencv-python pandas quandl scikit-learn scipy seaborn theano tqdm`



### Use `$HOME/.xinitrc` for starting bspwm from `gdm`

*/usr/share/xsessions/bspwm.desktop*

```
[Desktop Entry]
Name=bspwm
Comment=Binary space partitioning window manager
Exec=/home/atheistd/.xinitrc
Type=Application
```



### Chrome-based browser scaling at 2160p native monitor resolution

- Open `/etc/alternatives/brave-browser` and add the argument `--force-device-scale-factor=1.25` so it looks like

```
[...]
"$HERE/brave" "$@"  --force-device-scale-factor=1.25 || true
```

- Do the same for `google-chrome`, but it should look like

```
[...]
exec -a "$0" "$HERE/chrome" "$@" --force-device-scale-factor=1.25
```
