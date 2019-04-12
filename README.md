## install **xcode**
    xcode-select --install


## install **brew**
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

## install a few **basics**
    brew cask install iterm2 git openssl readline sqlite3 xz zlib pyenv pyenv-virtualenv tree
- *iterm2*: Better terminal
- *git*: version mangement
- *opelssl*, readline, sqlite3 xz zlib: required for pyenv
- *pyenv*: easily manage python version
- *pyenv-virtualenv*: setup local environmants per project  
- *tree*: tree view in terminal


## Beatuify **iTerm2**
    cd ~/Downloads
    curl -o "Atom One Dark.itermcolors" https://raw.githubusercontent.com/nathanbuchar/atom-one-dark-terminal/master/scheme/iterm/One%20Dark.itermcolors
    curl -o "Atom One Light.itermcolors" https://raw.githubusercontent.com/nathanbuchar/atom-one-dark-terminal/master/scheme/iterm/One%20Light.itermcolors

Go to iTerm settings, create new profile, import colorscheme.

After that we will add some additional options for the terminal

    cd ~
    curl -O https://raw.githubusercontent.com/TobiasDax/mac-dev-setup/master/.bash_profile
    curl -O https://raw.githubusercontent.com/TobiasDax/mac-dev-setup/master/.bash_prompt
    curl -O https://raw.githubusercontent.com/TobiasDax/mac-dev-setup/master/.aliases

## Configure **Git**
    git config --global user.name "Your Name Here"
    git config --global user.email "your_email@youremail.com"
add some color to git commands

    cd ~
    curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig
setup .gitignore

    cd ~
    curl -O https://raw.githubusercontent.com/TobiasDax/mac-dev-setup/master/.gitignore
    git config --global core.excludesfile ~/.gitignore

## Install **mas**
CLI Tool for Mac AppStore

    brew install mas
Open the AppStore and Login with your Credentials.

## Install third party **programms**
    brew cask install \
      atom \
      google-chrome \
      firefox \
      skype \
      skype-for-business \
      vlc \
      handbrake \
      microsoft-teams \
      lingo \
      adobe-creative-cloud \
      google-drive-file-stream \
      franz \
      spotify \
      tunnelblick \
      betterzip

## Install AppStore **Apps**
LastPass, Feedly, Trello, Remotedesktop, OneDrive, Clockify, Slack, Paste2, Taurine, LittleIpsum, Spark Mail, Magnet (spectacle is a good alternative, install with cdbrew cask install spectacle`)

    mas install \
      926036361 \
      865500966 \
      1278508951 \
      1295203466 \
      823766827 \
      1364502317 \
      803453959 \
      967805235 \
      960276676 \
      405772121 \
      1176895641 \
      441258766

install updates

    mas upgrade

## Add Spacing to the **Dock**
With a lot of different tools we also need some order in the Dock, you can create an empty space inside your mac Dock with the following command:

    defaults write com.apple.dock persistent-apps -array-add '{tile-data={}; tile-type="spacer-tile";}'

to reload the Dock type

    killall Dock

## Install **Fira Code** Font
    brew tap caskroom/fonts
    brew cask install font-fira-code
setup Fira Code as default font in iTerm2 and Atom

## Install **nvm** & **node**
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
    nvm install node

## Install **QuickLook** Plugins
Some great plugins for the QuickLook (Spacebar) function

    brew cask install qlcolorcode qlstephen qlmarkdown quicklook-json qlimagesize webpquicklook suspicious-package quicklookase qlvideo


## Setup Projects folder

    cd ~/Documents
    mkdir Projects

## Setup **SSH**
#### Generating Key and using it for GitHub/GitLab
generate ssh key

    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

start ssh agent

    eval "$(ssh-agent -s)"

edit `~/.ssh/config` File

    ssh-add -K ~/.ssh/id_rsa

Add SSH Key to GitHub/GitLab

#### Creating and using Host aliases to easily connect to Server
You need a private SSH Key, and have the public key setup at the server ready for connecting
the public Key needs to have permission set to `sudo chmod 600`

edit `~/.ssh/config` File

    Host ALIAS
      HostName DOMAIN/ IP
      IdentityFile ~/.ssh/KEY_NAME
      User USERNAME

## Using **Git**

nano in Git verwenden

    git config --global core.editor "nano"

cloning repository

    git clone git@github.com:TobiasDax/mac-dev-setup.git

status checken

    git status

Datei hinzufügen

    git add FILE

Commit erstellen

    git commit -m "created my own Readme"

Branch erstellen

    git checkout -b <my branch name>

Push to branch

    git push origin yourbranchname

Maste or Branch pullen

    git pull origin master

Git rebasen

    https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request

## **Tips**
- you can setup the location for screenshots by manually opening the .app and choosing a new folder

## Resources
- https://hackernoon.com/macbook-dev-setup-5890e61a8f0a
- https://github.com/nicolashery/mac-dev-setup
- https://www.lifewire.com/add-custom-and-standard-doc-spacers-to-mac-2260861
- https://github.com/sindresorhus/quick-look-plugins
- https://dev.to/therealdanvega/new-macbook-setup-for-developers-2nma
- https://github.com/mas-cli/mas
- https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- https://superuser.com/questions/503844/git-on-mac-how-to-set-nano-as-the-default-text-editor
- https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request
