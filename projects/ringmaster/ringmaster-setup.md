# Setup *ringmaster* ![beach-ball](https://github.com/atheistd/atheistd.github.io/raw/master/assets/ringmaster/ringmaster.gif)

### Press ⌘/ in Safari

### Give `Full Disk` access to:

- Terminal.app
- `appstoreagent`
- CleanMyMac X.app



### Xcode set-up

- `% xcode-select --install`
	- Give `Developer Tools` access to Terminal.app



### Show all files in Finder.app

- `% defaults write com.apple.finder AppleShowAllFiles YES`
- `% killall Finder`



### Brew

- [`install script`](https://brew.sh/)
- `% brew install aria2 coreutils ffmpeg grep htop neofetch speedtest-cli ssh-copy-id tmux wakeonlan wget && brew install --cask alacritty bitwarden bluestacks brave-browser discord firefox font-fira-code font-fira-mono google-chrome handbrake keka mpv obs steam sublime-text telegram transmission virtualbox virtualbox-extension-pack vivaldi webtorrent android-platform-tools && brew cleanup`



### misc
`% touch ~/.hushlogin`



### `git` config

- `% ssh-keygen -t ed25519 `&nbsp;&nbsp;&nbsp;&nbsp;*github, gitlab, sentinel*

- `% git config --global user.name "YOUR NAME"`
- `% git config --global user.email "YOUR EMAIL"`
- `% git config --global credential.helper osxkeychain`
- `% git config --global core.editor vim`


### Python set-up

- `% brew install python3`
- `% newenv "Deep Learning"`
- `% startpy`
- `% pip3 install --upgrade pip`
- `% pip3 install pip-review`
- `% pip-review --interactive`
- `% pip3 install instalooter ipython jupyter keras matplotlib numpy opencv-python pandas quandl scikit-learn scipy seaborn tensorflow theano torch torchvision tqdm`
- `% instalooter login`



### Apps

- [Android Debug Bridge](https://developer.android.com/studio/releases/platform-tools.html)
- [Android File Transfer](http://android.com/filetransfer/)
- *optional* [AppCleaner](http://freemacsoft.net/appcleaner/) => **CleanMyMac x**
- *optional* [Atom](http://atom.io/) => **Sublime Text**
- CleanMyMac X *> in disk*
- [HandBrake](http://handbrake.fr/)
- [IINA](https://iina.io/)
- *optional* [iMovie](https://apps.apple.com/in/app/imovie/id408981434) => **FCPX**
- iWork
	- [Keynote](https://apps.apple.com/in/app/keynote/id409183694)
	- [Numbers](https://apps.apple.com/in/app/numbers/id409203825)
	- [Pages](https://apps.apple.com/in/app/pages/id409201541)
- [Intel Power Gadget](https://software.intel.com/en-us/articles/intel-power-gadget/)
- [Keka](http://keka.io/)
- [Keka default helper](https://github.com/aonez/Keka/wiki/Default-application)
- [Macs Fan Control](https://www.macupdate.com/app/mac/47386/macs-fan-control)
- [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)
- [Spotify](http://spotify.com/in/download/other/)
- [Sublime Text 3](http://sublimetext.com/)
- [Transmission](https://transmissionbt.com/download/)



### Sublime Text 3

- Preferences > Settings
>`"fade_fold_buttons": true,`<br>
>`"indent_guide_options": ["draw_active"],`<br>
>`"ensure_newline_at_eof_on_save": true,`<br>
>`"save_on_focus_lost": true,`<br>
>`"atomic_save": true,`<br>
>`"auto_complete_delay": 1,`<br>
>`"shift_tab_unindent": true,`<br>
>`"show_encoding": true,`<br>
>`"show_line_endings": true,`

- Preferences > Key Bindings
>`{"keys": ["ctrl+tab"], "command": "next_view"},`<br>
>`{"keys": ["ctrl+shift+tab"], "command": "prev_view"},`

- [TwoDark](https://packagecontrol.io/packages/Theme%20-%20TwoDark)
- [A File Icon](https://packagecontrol.io/packages/A%20File%20Icon)
