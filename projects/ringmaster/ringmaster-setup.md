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
- `% brew install ffmpeg htop speedtest-cli wget`



### Python set-up

- `% brew install python3`
- `% newpython3 -m venv "Deep Learning"`
- `% startpy`
- `% pip3 install --upgrade pip`
- `% pip3 install pip-review`
- `% pip-review --interactive`
- `% pip3 install ipython jupyter keras matplotlib numpy opencv-python pandas quandl scikit-learn scipy seaborn tensorflow theano torch torchvision tqdm`



### `git` config

- `% git config --global user.name "YOUR NAME"`
- `% git config --global user.email "YOUR EMAIL"`
- `% git config --global credential.helper osxkeychain`


### `.zshrc`

- `% git clone --depth 1 https://github.com/atheistd/setup ~/Documents/setup`
- `% cp ~/Documents/setup/ringmaster/.zshrc ~/.zshasdf`
- `% chown +x ~/.zshrc`



### Apps

- [Bandwidth+](https://apps.apple.com/in/app/bandwidth/id490461369?mt=12)
- [Xcode](https://apps.apple.com/in/app/xcode/id497799835)
- [Android Debug Bridge](https://developer.android.com/studio/releases/platform-tools.html)
- [Android File Transfer](http://android.com/filetransfer/)
- *optional* [AppCleaner](http://freemacsoft.net/appcleaner/) => **CleanMyMac x**
- *optional* [Atom](http://atom.io/) => **Sublime Text**
- [Brave Browser](https://brave.com/download/)
- CleanMyMac X *> in disk*
- [ClipGrab](https://clipgrab.org/)
- [Dato](https://apps.apple.com/in/app/dato/id1470584107?mt=12)
- [Dropbox](https://www.dropbox.com/downloading)
- [Encrypto](https://apps.apple.com/in/app/encrypto-secure-your-files/id935235287?mt=12)
- [Firefox](https://www.mozilla.org/en-US/firefox/new/)
- [Gemini 2](https://apps.apple.com/in/app/gemini-2-the-duplicate-finder/id1090488118?mt=12)
- [Google Chrome](https://chrome.google.com/)
- [HandBrake](http://handbrake.fr/)
- [IINA](https://iina.io/)
- *optional* [iMovie](https://apps.apple.com/in/app/imovie/id408981434?mt=12) => **FCPX**
- iWork
	- [Keynote](https://apps.apple.com/in/app/keynote/id409183694?mt=12)
	- [Numbers](https://apps.apple.com/in/app/numbers/id409203825?mt=12)
	- [Pages](https://apps.apple.com/in/app/pages/id409201541?mt=12)
- [Intel Power Gadget](https://software.intel.com/en-us/articles/intel-power-gadget/)
- [Keka](http://keka.io/)
- [Keka default helper](https://github.com/aonez/Keka/wiki/Default-application)
- [LastPass](https://apps.apple.com/in/app/lastpass-password-manager/id926036361?mt=12)
- [MacPorts](http://macports.org/)
- [Macs Fan Control](https://www.macupdate.com/app/mac/47386/macs-fan-control)
- [Progressive Downloader](https://macpsd.net/)
- [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)
- [Safari Technology Preview](https://developer.apple.com/safari/technology-preview/)
- [Shazam](https://apps.apple.com/in/app/shazam/id897118787?mt=12)
- [Spotify](http://spotify.com/in/download/other/)
- [Sublime Text 3](http://sublimetext.com/)
- *optional* [TeamViewer](http://teamviewer.com/) => **VNC Viewer**
- [Terminus](https://apps.apple.com/in/app/termius-ssh-client/id1176074088)
- [Tor Browser](http://torproject.org/)
- [Transmission](https://transmissionbt.com/download/)
- [Unsplash Wallpapers](https://apps.apple.com/in/app/unsplash-wallpapers/id1284863847?mt=12)
- [VirtualBox](http://virtualbox.org/wiki/Downloads)
- [VLC](http://www.videolan.org/)
- [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/)
- [WhatsApp](https://apps.apple.com/in/app/whatsapp-desktop/id1147396723?mt=12)



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
>`{"keys": ["ctrl+tab"], "command": "next_view"},`
>`{"keys": ["ctrl+shift+tab"], "command": "prev_view"},`

- [TwoDark](https://packagecontrol.io/packages/Theme%20-%20TwoDark)
- [A File Icon](https://packagecontrol.io/packages/A%20File%20Icon)
