# Setup *flameboi!* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/flameboi/flameboi-small.png)

### UPDATE!!!

- **set DNS to pi-hole server**

- `$ sudo apt update`
- `$ sudo systemctl unmask nvidia-suspend nvidia-hibernate nvidia-resume`
- `$ sudo systemctl enable nvidia-suspend nvidia-hibernate nvidia-resume`
- `$ #sudo apt remove "*nvidia"`
- `$ #sudo apt install system76-driver-nvidia -y`
- `$ sudo apt upgrade -y`
- Reboot

### gnome extensions

- `$ sudo apt install gnome-shell-extensions -y`
* [Simple net speed](https://extensions.gnome.org/extension/1085/simple-net-speed/)
* [BackSlide](https://extensions.gnome.org/extension/543/backslide/)

### Installing necessary packages and preliminary setup

- `$ sudo apt update`
- `$ sudo apt install adb alacritty aria2 barrier bc bison btop build-essential cifs-utils cmake cmatrix curl ethtool exfat-fuse exfat-utils fakeroot fastboot fdisk ffmpeg flex fonts-firacode fonts-fork-awesome git handbrake hdparm htop imagemagick iotop iperf iperf3 libelf-dev libnotify-bin libpam-google-authenticator libssl-dev linux-headers-$(uname -r) lsb-release mediainfo mpv ncurses-dev neofetch neovim nethogs nload nvme-cli obs-plugins obs-studio openssh-server python3 python3-pip qemu qemu-efi-aarch64 qemu-efi-arm qemu-kvm qemu-system-arm qemu-system-x86 rar ripgrep rsync smartmontools speedtest-cli tar tmux transmission-cli unrar unzip valgrind vim virt-manager vlc wakeonlan wget xz-utils yt-dlp zfs-dkms zip zsh zsh-autosuggestions zsh-syntax-highlighting`

- `$ #apt search virtualbox | grep pop`

```
# for window manager
sudo apt install breeze-cursor-theme bspwm dunst feh gtk-chtheme i3lock-fancy libnotify-bin jq lxappearance polybar picom rofi socat sxhkd xcursor-themes 
echo "gtk-application-prefer-dark-theme=true" | tee $HOME/.config/gtk-3.0/settings.ini
```

- `$ sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'`

- `$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
- `$ rustup component add rust-analysis rust-src`

- `$ flatpak install flathub com.bitwarden.desktop com.github.micahflee.torbrowser-launcher com.brave.Browser org.mozilla.firefox com.dangeredwolf.ModernDeck org.ksnip.ksnip org.telegram.desktop com.github.tchx84.Flatseal com.sublimetext.three`

- `$ sudo update-alternatives --set editor /usr/bin/nvim`
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

### Making `alacritty` default terminal emulator

 - `$ gsettings set org.gnome.desktop.default-applications.terminal exec '/usr/bin/alacritty'`
 - `$ sudo update-alternatives --config x-terminal-emulator`
 - `$ #gsettings set org.gnome.desktop.interface clock-show-date true; gsettings set org.gnome.desktop.interface clock-show-seconds true; gsettings set org.gnome.desktop.interface clock-show-weekday true`

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


### Powering off HDDs

*/etc/systemd/system/power-down-hdds-after-wake-up.service*

```
[Unit]
Description=Put HDDs to sleep after waking up from suspend
After=suspend.target hibernate.target hybrid-sleep.target suspend-then-hibernate.target


[Service]
ExecStart=/usr/bin/bash /home/atheistd/.scripts/hdd_sleep.sh
#User=my_user_name
#Environment=DISPLAY=:0

[Install]
WantedBy=suspend.target hibernate.target hybrid-sleep.target suspend-then-hibernate.target
```

> Add the following crojob to root's cron

`@reboot /usr/bin/bash /home/atheistd/.scripts/hdd_sleep.sh`

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
"$HERE/brave" "$@" --force-device-scale-factor=1.25 || true
```

- Do the same for `google-chrome`, but it should look like

```
[...]
exec -a "$0" "$HERE/chrome" "$@" --force-device-scale-factor=1.25
```

### Sublime Text 3

- [SublimeJEDI](https://packagecontrol.io/packages/Jedi%20-%20Python%20autocompletion)
- [TwoDark](https://packagecontrol.io/packages/Theme%20-%20TwoDark)

- Preferences > Settings

```
	"ui_scale": 1.25,
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
	"indent_guide_options":["draw_active"],
	"save_on_focus_lost": true,
	"shift_tab_unindent": true,
	"show_encoding": true,
	"show_line_endings": true,
	"theme": "TwoDark.sublime-theme",
	"auto_complete_triggers": [{"selector": "source.python", "characters": ".",}],
	"ignored_packages": ["Vintage"],
	"font_size": 12,
```

- Preferences > Key Bindings

```
	{"keys": ["ctrl+tab"], "command": "next_view"},
	{"keys": ["ctrl+shift+tab"], "command": "prev_view"},
```
