# macOS Dev Setup

This document describes how I set up my developer environment on a new MacBook or iMac. We will set up popular programming languages (for example [Node](http://nodejs.org/) (JavaScript), [Python](http://www.python.org/), and [Ruby](http://www.ruby-lang.org/)). You may not need all of them for your projects, although I recommend having them set up as they always come in handy.

The document assumes you are new to Mac, but can also be useful if you are reinstalling a system and need some reminder. The steps below were tested on **macOS High Sierra** (10.13), but should work for more recent versions as well.

**Contributing**: If you find any mistakes in the steps described below, or if any of the commands are outdated, do let me know! For any other suggestions, please understand if I don't include everything. This guide was originally written for some friends getting started with programming on a Mac, and as a personal reference for myself. I'm trying to keep it simple!

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Security](#security)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Git](#git)
- [Visual Studio Code](#visual-studio-code)
- [Vim](#vim)
- [Python](#python)
- [Node.js](#nodejs)
- [Ruby](#ruby)
- [Heroku](#heroku)
- [PostgreSQL](#postgresql)
- [Redis](#redis)
- [Elasticsearch](#elasticsearch)
- [Projects folder](#projects-folder)
- [Apps](#apps)

## System update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > About This Mac** then **Software Update...**.

## System preferences

If this is a new computer, there are a couple of tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock

## Security

I recommend checking that basic security settings are enabled. You will be happy to have done so if ever your Mac is lost or stolen.

In **Apple Icon > System Preferences**:

- Users & Groups: If you haven't already set a password for your user during the initial set up, you should do so now
- Security & Privacy > General: Require password immediately after sleep or screen saver begins (you can keep a grace period of a couple minutes if you prefer, but I like to know that my computer locks as soon as I close it)
- Security & Privacy > FileVault: Make sure FileVault disk encryption is enabled
- iCloud: If you haven't already done so during set up, enable Find My Mac

## iTerm2

### Install

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/).

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm2 > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Under the section **General** set **Working Directory** to be **Reuse previous session's directory**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

When done, hit the red "X" in the upper left (saving is automatic in macOS preference panes). Close the window and open a new one to see the size change.

### Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

First let's add some color. There are many great color schemes out there, but if you don't know where to start you can try [Atom One Dark](https://github.com/nathanbuchar/atom-one-dark-terminal). Download the iTerm presets for the theme by running:

```
cd ~/Downloads
curl -o "Atom One Dark.itermcolors" https://raw.githubusercontent.com/nathanbuchar/atom-one-dark-terminal/master/scheme/iterm/One%20Dark.itermcolors
curl -o "Atom One Light.itermcolors" https://raw.githubusercontent.com/nathanbuchar/atom-one-dark-terminal/master/scheme/iterm/One%20Light.itermcolors
```

Then, in **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Color Presets... > Import...**, find and open the **Atom One Dark.itermcolors** file we just downloaded. Repeat these steps for **Atom One Light.itermcolors**.  Now open **Color Presets...** again and select **Atom One Dark** to activate the dark theme (or choose the light them if that's your preference).

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on macOS and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile), [.bash_prompt](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt), [.aliases](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

```
cd ~
curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile
curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt
curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases
```

With that, open a new terminal tab (**Cmd+T**) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

Now we have a terminal we can work with!

(Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles).)

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for macOS is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Developer Tools** for **Xcode**. These include compilers that will allow you to build things from source. You can install them directly from the terminal with:

```
xcode-select --install
```

Once that is done, we can install Homebrew by copy-pasting the installation command from the [Homebrew homepage](http://brew.sh/) inside the terminal:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Follow the steps on the screen. You will be prompted for your user password so Homebrew can set up the appropriate permissions.

Once installation is complete, you can run the following command to make sure everything works:

```
brew doctor
```

### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

```
brew install <formula>
```

To see if any of your packages need to be updated:

```
brew outdated
```

To update a package:

```
brew upgrade <formula>
```

Homebrew keeps older versions of packages installed, in case you want to rollback. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

```
brew cleanup
```

To see what you have installed (with their version numbers):

```
brew list --versions
```

### Homebrew Services

A nice extension to Homebrew is [Homebrew Services](https://github.com/Homebrew/homebrew-services). It will automatically launch things like databases when your computer starts, so you don't have to do it manually every time.

Homebrew Services will automatically install itself the first time you run it, so there is nothing special to do.

After installing a service (for example a database), it should automatically add itself to Homebrew Services. If not, you can add it manually with:

```
brew services <formula>
```

Start a service with:

```
brew services start <formula>
```

At anytime you can view which services are running with:

```
brew services list
```

## Git

macOS comes with a pre-installed version of [Git](http://git-scm.com/), but we'll install our own through Homebrew to allow easy upgrades and not interfere with the system version. To do so, simply run:

```
brew install git
```

When done, to test that it installed fine you can run:

```
which git
```

The output should be `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig) file to your home directory:

```
cd ~
curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig
```

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

```
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```

They will get added to your `.gitconfig` file.

On a Mac, it is important to remember to add `.DS_Store` (a hidden macOS system file that's put in folders) to your project `.gitignore` files. You also set up a global `.gitignore` file, located for instance in your home directory (but you'll want to make sure any collaborators also do it):

```
cd ~
curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitignore
git config --global core.excludesfile ~/.gitignore
```

## Visual Studio Code

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but if you're just getting started and looking for something simple that works, [Visual Studio Code](https://code.visualstudio.com/) is a pretty good option.

Go ahead and [download](https://code.visualstudio.com/Download) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shortcut on the macOS Dock for both for Visual Studio Code and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

Just like the terminal, let's configure our editor a little. Go to **Code > Preferences > Settings**. In the very top-right of the interface you should see an icon with brackets that appeared **{ }** (on hover, it should say "Open Settings (JSON)"). Click on it, and paste the following:

```json
{
  "editor.tabSize": 2,
  "editor.rulers": [80],
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  "workbench.editor.enablePreview": false
}
```

Feel free to tweak these to your preference. When done, save the file and close it.

Pasting the above JSON snippet was handy to quickly customize things, but for further setting changes feel free to search in the "Settings" panel that opened first (shortcut **Cmd+,**). When you're happy with your setup, you can save the JSON to quickly restore it on a new machine.

If you remember only one keyboard shortcut in VS Code, it should be **Cmd+Shift+P**. This opens the **Command Palette**, from which you can run pretty much anything.

Let's open the command palette now, and search for `Shell Command: Install 'code' command in PATH`. Hit enter when it shows up. This will install the command-line tool `code` to quickly open VS Code from the terminal. When in a projects directory, you'll be able to run:

```
cd myproject/
code .
```

VS Code is very extensible. To customize it further, open the **Extensions** tab on the left.

Let's do that now to customize the color of our editor. Search for the [Atom One Dark Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onedark) extension, select it and click **Install**. Repeat this for the [Atom One Light Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onelight).

Finally, activate the theme by going to **Code > Preferences > Color Theme** and selecting **Atom One Dark** (or **Atom One Light** if that is your preference).

## Vim

Although VS Code will be our main editor, it is a good idea to learn some very basic usage of [Vim](http://www.vim.org/). It is a very popular text editor inside the terminal, and is usually pre-installed on any Unix system.

For example, when you run a Git commit, it will open Vim to allow you to type the commit message.

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, **Insert** (by pressing `i`) and **Normal** (by pressing `Esc` to exit Insert mode), will be the part that feels most unnatural. Also, it is good to know that typing `:x` when in Normal mode will save and exit. After that, it's just remembering a few important keys.

Vim's default settings aren't great, and you could spend a lot of time tweaking your configuration (the `.vimrc` file). But if you only use Vim occasionally, you'll be happy to know that [Tim Pope](https://github.com/tpope) has put together some sensible defaults to quickly get started.

Using Vim's built-in package support, install these settings by running:

```
mkdir -p ~/.vim/pack/tpope/start
cd ~/.vim/pack/tpope/start
git clone https://tpope.io/vim/sensible.git
```

With that, Vim will look a lot better next time you open it!

## Python

macOS, like Linux, ships with [Python](http://python.org/) already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.), so we'll install our own version using [pyenv](https://github.com/yyuu/pyenv). This will also allow us to manage multiple versions of Python (ex: 2.7 and 3) should we need to.

Install `pyenv` via Homebrew by running:

```
brew install pyenv
```

When finished, you should see instructions to add something to your profile. Open your `.bash_profile` in the home directory (you can use `code ~/.bash_profile`), and add the following line:

```bash
if command -v pyenv 1>/dev/null 2>&1; then eval "$(pyenv init -)"; fi
```

Save the file and reload it with:

```
source ~/.bash_profile
```

Before installing a new Python version, the [pyenv wiki](https://github.com/pyenv/pyenv/wiki) recommends having a few dependencies available:

```
brew install openssl readline sqlite3 xz zlib
```

We can now list all available Python versions by running:

```
pyenv install --list
```

Look for the latest 3.x version (or 2.7.x), and install it (replace the `.x.x` with actual numbers):

```
pyenv install 3.x.x
```

List the Python versions you have locally with:

```
pyenv versions
```

The star (`*`) should indicate we are still using the `system` version, which is the default. I recommend leaving it as the default as some [Node.js](https://nodejs.org/en/) packages will use it in their installation process.

You can switch your current terminal to another Python version with:

```
pyenv shell 3.x.x
```

You should now see that version when running:

```
python --version
```

In a project directory, you can use:

```
pyenv local 3.x.x
```

This will save that project's Python version to a `.python-version` file. Next time you enter the project's directory from a terminal, `pyenv` will automatically load that version for you.

For more information, see the [pyenv commands](https://github.com/yyuu/pyenv/blob/master/COMMANDS.md) documentation.

### pip

[pip](https://pip.pypa.io) was also installed by `pyenv`. It is the package manager for Python.

Here are a couple Pip commands to get you started. To install a Python package:

```
pip install <package>
```

To upgrade a package:

```
pip install --upgrade <package>
```

To see what's installed:

```
pip freeze
```

To uninstall a package:

```
pip uninstall <package>
```

### virtualenv

[virtualenv](https://virtualenv.pypa.io) is a tool that creates an isolated Python environment for each of your projects.

For a particular project, instead of installing required packages globally, it is best to install them in an isolated folder, that will be managed by `virtualenv`. The advantage is that different projects might require different versions of packages, and it would be hard to manage that if you install packages globally.

Instead of installing and using `virtualenv` directly, we'll use the dedicated `pyenv` plugin [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv) which will make things a bit easier for us. Install it via Homebrew:

```
brew install pyenv-virtualenv
```

After installation, add the following line to your `.bash_profile`:

```bash
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

And reload it with:

```
source ~/.bash_profile
```

Now, let's say you have a project called `myproject`. You can set up a virtualenv for that project and the Python version it uses (replace `3.x.x` with the version you want):

```
pyenv virtualenv 3.x.x myproject
```

See the list of virtualenvs you created with:

```
pyenv virtualenvs
```

To use your project's virtualenv, you need to **activate** it first (in every terminal where you are working on your project):

```
pyenv activate myproject
```

If you run `pyenv virtualenvs` again, you should see a star (`*`) next to the active virtualenv.

Now when you install something:

```
pip install <package>
```

It will get installed in that virtualenv's folder, and not conflict with other projects.

You can also set your project's `.python-version` to point to a virtualenv you created:

```
pyenv local myproject
```

Next time you enter that project's directory, `pyenv` will automatically load the virtualenv for you.

### Anaconda and Miniconda

The Anaconda/Miniconda distributions of Python come with many useful tools for scientific computing.

You can install them using `pyenv`, for example (replace `x.x.x` with an actual version number):

```
pyenv install miniconda3-x.x.x
```

After loading an Anaconda or Miniconda Python distribution into your shell, you can create [conda](https://docs.conda.io/) environments (which are similar to virtualenvs):

```
pyenv shell miniconda3-x.x.x
conda create --name  mycondaproject
conda activate mycondaproject
```

Install packages, for example the [Jupyter Notebook](https://jupyter.org/), using:

```
conda install jupyter
```

You should now be able to run the notebook:

```
jupyter notebook
```

Deactivate the environment, and return to the default Python version with:

```
conda deactivate
pyenv shell --unset
```

### Known issue: `gettext` not found by `git` after installing Anaconda/Miniconda

If you installed an Anaconda/Miniconda distribution, you may start seeing an error message when using certain `git` commands, similar to this one:

```
pyenv: gettext.sh: command not found

The `gettext.sh' command exists in these Python versions:
  miniconda3-latest
```

If that is the case, you can use the following [workaround](https://github.com/pyenv/pyenv/issues/688#issuecomment-428675578):

```
brew install gettext
```

Then add this line to your `.bash_profile`:

```bash
# Workaround for: https://github.com/pyenv/pyenv/issues/688#issuecomment-428675578
export PATH="/usr/local/opt/gettext/bin:$PATH"
```

## Node.js

The recommended way to install [Node.js](http://nodejs.org/) is to use [nvm](https://github.com/creationix/nvm) (Node Version Manager) which allows you to manage multiple versions of Node.js on the same machine.

Install `nvm` by copy-pasting the [install script command](https://github.com/creationix/nvm#install--update-script) into your terminal.

Once that is done, open a new terminal and verify that it was installed correctly by running:

```
command -v nvm
```

View the all available stable versions of Node with:

```
nvm ls-remote --lts
```

Install the latest stable version with:

```
nvm install node
```

It will also set the first version installed as your default version. You can install another specific version, for example Node 10, with:

```
nvm install 10
```

And switch between versions by using:

```
nvm use 10
nvm use default
```

See which versions you have install with:

```
nvm ls
```

Change the default version with:

```
nvm alias default 10
```

In a project's directory you can create a `.nvmrc` file containing the Node.js version the project uses, for example:

```
echo "10" > .nvmrc
```

Next time you enter the project's directory from a terminal, you can load the correct version of Node.js by running:

```
nvm use
```

### npm

Installing Node also installs the [npm](https://npmjs.org/) package manager.

To install a package:

```
npm install <package> # Install locally
npm install -g <package> # Install globally
```

To install a package and save it in your project's `package.json` file:

```
npm install --save <package>
```

To see what's installed:

```
npm list --depth 1 # Local packages
npm list -g --depth 1 # Global packages
```

To find outdated packages (locally or globally):

```
npm outdated [-g]
```

To upgrade all or a particular package:

```
npm update [<package>]
```

To uninstall a package:

```
npm uninstall --save <package>
```

## Ruby

Like Python, [Ruby](http://www.ruby-lang.org/) is already installed on Unix systems. But we don't want to mess around with that installation. More importantly, we want to be able to use the latest version of Ruby.

### Install

The recommended way to install Ruby is to use [rbenv](https://github.com/rbenv/rbenv), which allows you to manage multiple versions of Ruby on the same machine. You can install `rbenv` with Homebrew:

```
brew install rbenv
```

After installation, add the following line to your `.bash_profile`:

```bash
eval "$(rbenv init -)"
```

And reload it with:

```
source ~/.bash_profile
```

### Usage

The following command will show you which versions of Ruby are available to install:

```
rbenv install --list
```

You can find the latest version in that list and install it with (replace `.x.x` with actual version numbers):

```
rbenv install 2.x.x
```

Run the following to see which versions you have installed:

```
rbenv versions
```

The start (`*`) will show you that we are currently using the default `system` version. You can switch your terminal to use the one you just installed:

```
rbenv shell 2.x.x
```

You can also set it as the default version if you want:

```
rbenv global 2.x.x
```

In a specific project's directory, you can ask `rbenv` to create a `.ruby-version` file. Next time you enter that project's directory from the terminal, it will automatically load the correct Ruby version:

```
rbenv local 2.x.x
```

Check anytime which version you are using with:

```
rbenv version
```

See [rbenv's command reference](https://github.com/rbenv/rbenv#command-reference) for more information.

### RubyGems & Bundler

[RubyGems](http://rubygems.org/), the Ruby package manager, was also installed:

```
which gem
```

The first thing you want to do after installing a new Ruby version is to install [Bundler](https://bundler.io/). This tool will allow you to set up separate environments for your different Ruby projects, so their required gem versions won't conflict with each other. Install Bundler with:

```
gem install bundler
```

In a new Ruby project directory, create a new `Gemfile` with:

```
bundle init
```

Add a dependency to the `Gemfile`, for example the [Jekyll]() static site generator:

```ruby
source "https://rubygems.org"

gem "jekyll"
```

Then install the project's dependencies with:

```
bundle install
```

Make sure you check in both the `Gemfile` and `Gemfile.lock` into your Git repository.

Update a specific dependency with:

```
bundle update <gem>
```

For more information, see the [Bundler documentation](https://bundler.io/docs.html).

## Heroku

[Heroku](http://www.heroku.com/) is a [Platform-as-a-Service](http://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) that makes it really easy to deploy your apps. There are other similar solutions out there, but Heroku is among the most popular. Not only does it make a developer's life easier, but I find that having Heroku deployment in mind when building an app forces you to follow modern app development [best practices](http://www.12factor.net/).

Assuming that you have an account (sign up if you don't), let's install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli):

```
brew tap heroku/brew
brew install heroku
```

Login to your Heroku account using:

```
heroku login
```

(This will prompt you to open a page in your web browser and log in to your Heroku account.)

Once logged-in, you're ready to deploy apps! Heroku has great [Getting Started](https://devcenter.heroku.com/start) guides for different languages, so I'll let you refer to that. Heroku uses Git to push code for deployment, so make sure your app is under Git version control. A quick cheat sheet (if you've used Heroku before):

```
cd myapp/
heroku create myapp
git push heroku master
heroku ps
heroku logs -t
```

The [Heroku Dev Center](https://devcenter.heroku.com/) is full of great resources, so be sure to check it out!

## PostgreSQL

[PostgreSQL](https://www.postgresql.org/) is a popular relational database, and Heroku has first-class support for it.

Install PostgreSQL using Homebrew:

```
brew install postgresql
```

It will automatically add itself to Homebrew Services. Start it with:

```
brew services start postgresql
```

If you reboot your machine, PostgreSQL will be restarted at login.

### GUI

You can interact with your SQL database by running `psql` in the terminal.

If you prefer a GUI (Graphical User Interface), [Postico](https://eggerapps.at/postico/) has a simple free version that let's you explore tables and run SQL queries.

## Redis

[Redis](http://redis.io/) is a fast, in-memory, key-value store, that uses the disk for persistence. It complements nicely a database such as PostgreSQL. There are a lot of [interesting things](http://oldblog.antirez.com/post/take-advantage-of-redis-adding-it-to-your-stack.html) that you can do with it. For example, it's often used for session management or caching by web apps, but it has many other uses.

To install Redis, use Homebrew:

```
brew install redis
```

Start it through Homebrew Services with:

```
brew services start redis
```

I'll let you refer to Redis' [documentation](http://redis.io/documentation) or other tutorials for more information.

## Elasticsearch

[Elasticsearch](https://www.elastic.co/products/elasticsearch) is a distributed search and analytics engine. It uses an HTTP REST API, making it easy to work with from any programming language.

You can use elasticsearch for things such as real-time search results, autocomplete, recommendations, machine learning, and more.

### Install

Elasticsearch runs on Java, so check if you have it installed by running:

```bash
java -version
```

If Java isn't installed yet, dismiss the window that just appeared by clicking "Ok", and install Java via Homebrew:

```
brew cask install homebrew/cask-versions/java8
```

Next, install Elasticsearch with:

```bash
brew install elasticsearch
```

### Usage

Start the Elasticsearch server with:

```bash
brew services start elasticsearch
```

Test that the server is working correctly by running:

```bash
curl -XGET 'http://localhost:9200/'
```

(You may need to wait a little bit for it to boot up if you just started the service.)

Elasticsearch's [documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html) is more of a reference. To get started, you can also take a look at [Elasticsearch: The Definitive Guide](https://www.elastic.co/guide/en/elasticsearch/guide/master/index.html).

### GUI

You can interact with the Elasticsearch server using `curl`, or anything that can send an HTTP request.

However, if you prefer a graphical interface, you can take a look at [Dejavu](https://opensource.appbase.io/dejavu/). You can easily install it via the [Dejavu Chrome Extension](https://chrome.google.com/webstore/detail/dejavu-elasticsearch-web/jopjeaiilkcibeohjdmejhoifenbnmlh).

## Projects folder

This really depends on how you want to organize your files, but I like to put all my version-controlled projects in `~/Projects`. Other documents I may have, or things not yet under version control, I like to put in `~/Dropbox` (if you have [Dropbox](https://www.dropbox.com/) installed), or `~/Documents` if you prefer to use [iCloud Drive](https://support.apple.com/en-ca/HT206985).

## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [1Password](https://1password.com/): Securely store your login and passwords, and access them from all your devices. **($3/month)**
- [Dropbox](https://www.dropbox.com/): File syncing to the cloud. It is cross-platform, but if all your devices are Apple you may prefer [iCloud Drive](https://support.apple.com/en-ca/HT206985). **(Free for 2GB)**
- [Postman](https://www.getpostman.com/): Easily make HTTP requests. Useful to test your REST APIs. **(Free for basic features)**
- [GitHub Desktop](https://desktop.github.com/): I do everything through the `git` command-line tool, but I like to use GitHub Desktop just to review the diff of my changes. **(Free)**
- [Spectacle](https://www.spectacleapp.com/): Move and resize windows with keyboard shortcuts. **(Free)**
