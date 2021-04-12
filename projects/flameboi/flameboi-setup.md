# Setup *flameboi!* ![flameboi! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/flameboi/flameboi-small.png)



### UPDATE!!!

- `$ sudo apt update && sudo apt upgrade -y`
- Reboot



### Installing [Brave Browser](https://brave.com/linux/)



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



### Installing packages

- `$ sudo apt install android-sdk-platform-tools-common aria2 cmatrix curl dolphin exfat-fuse exfat-utils ffmpeg firefox flatpak fonts-firacode git google-chrome-stable handbrake hdparm htop libpam-google-authenticator mediainfo mpv ncdu neofetch nload obs-plugins obs-studio openssh-server python3 python3-pip python3-venv qemu rar rsync smartmontools speedtest-cli sublime-text terminator unrar unzip vim virtualbox vlc wget zfsutils-linux zip zsh -y`

- `$ sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl`
- `$ sudo chmod a+rx /usr/local/bin/youtube-dl`

- `$ pip3 install bpytop`
- `$ pip3 install instalooter && instalooter login`

- `$ sudo zpool import`



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

*/etc/ssh/sshd_config*
```
ChallengeResponseAuthentication yes
```

- `$ sudo systemctl restart sshd`



### OBS NVENC plugin(s)

 - [StreamFX](https://obsproject.com/forum/resources/streamfx-for-obs-studio.578/updates)



### Python

- **REBOOT**

- `$ sudo adduser $USER vboxusers`

- `$ python3 -m venv deeplearning`
- `$ startpy`
- `$ pip3 install --upgrade pip`
- `$ pip3 install pip-review`
- `$ pip-review --interactive`
- `$ deactivate`
- `$ apt search cuda`
- `$ sudo apt install` (check which version is compatible with &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [torch](https://pytorch.org/get-started/locally/)) (**use at-least 11.1, 10.2 will not work well will NV 30XX**)
- `$ startpy`
- `$ pip3 install` [insert torch packages here] `ipython jupyter jupyterthemes keras matplotlib numpy opencv-python pandas quandl scikit-learn scipy seaborn theano tqdm`

*~/.jupyter/custom/custom.css*

```

@font-face {
  font-family: 'Fira Code';
  src: url("https://cdn.rawgit.com/dunovank/jupyter-themes/1e851888/jupyterthemes/fonts/monospace/firacode/firacode.otf") format("opentype");
}

.CodeMirror {
  font-family: 'Fira Code';
  font-variant-ligatures: initial;
}

.cm-string {
    font-variant-ligatures: none;
}

```

- **REBOOT**
