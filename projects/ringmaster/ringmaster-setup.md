# Setup *ringmaster* ![beach-ball](https://github.com/shivohamx3/shivohamx3.github.io/raw/master/assets/ringmaster/ringmaster.gif)


### Xcode set-up

- `% xcode-select --install`
	- Give `Developer Tools` access to `Alacritty.app`



### Brew

- [`install script`](https://brew.sh/)
- `% brew update && brew upgrade && brew install aria2 coreutils ffmpeg grep htop neofetch speedtest-cli ssh-copy-id tmux wakeonlan watch wget && brew install --cask alacritty android-platform-tools bitwarden brave-browser firefox google-chrome handbrake homebrew/cask-fonts/font-fira-code homebrew/cask-fonts/font-fira-mono keka macs-fan-control mpv obs sublime-text telegram transmission virtualbox virtualbox-extension-pack webtorrent && brew cleanup`



### Show all files in Finder.app

- `% defaults write com.apple.finder AppleShowAllFiles YES`
- `% killall Finder`



### Press ⌘/ in Safari



### ~Terminal~ Alacritty Setup

- `% git clone https://github.com/alacritty/alacritty.git && cd alacritty`
- `% sudo tic -xe alacritty,alacritty-direct extra/alacritty.info`
- `% cd .. && rm -rf alacritty`



### Python set-up

- `% pip3 install --upgrade pip`
- `% pip3 install --user --upgrade pip-review`
- `% pip-review --interactive`
- `% pip3 install --user --upgrade ipython jupyter keras matplotlib numpy opencv-python pandas quandl scikit-learn scipy seaborn tensorflow theano torch torchaudio torchvision tqdm yt-dlp`



### Apps

- [IINA](https://iina.io/)
- [Intel Power Gadget](https://software.intel.com/en-us/articles/intel-power-gadget/)
- [Keka default helper](https://github.com/aonez/Keka/wiki/Default-application)



###### `git` config (optional if using `setup.git`)

- `% ssh-keygen -t ed25519 `&nbsp;&nbsp;*github, gitlab, sentinel*
(optional if already imported ssh keys)

- `% git config --global user.name "YOUR NAME"`
- `% git config --global user.email "YOUR EMAIL"`
- `% git config --global credential.helper osxkeychain`
- `% git config --global core.editor vim`
