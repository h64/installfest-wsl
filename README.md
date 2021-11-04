<img src="https://i.imgur.com/pF2sUV5.jpg">

# SEI Installfest

We'll be installing the following tools.

- WSL (Windows Subsystem for Linux 2)
- Slack
- VS Code
- Git
- Node.js
- PostgreSQL
- MongoDB
- Python
- Django

## Slack

We will be using slack to communicate throughout the course. You will receive an invite to the relevant channels via e-mail. You can login via the web browser, but downloading / installing the app is highly recommended.

[Download Slack](https://slack.com/downloads/windows)

---


## WSL Introduction
Windows Subsystem for Linux (WSL) is a tool by Microsoft that allows you to run a Linux command line environment directly inside of Windows without having to dual-boot or run a separate VM program.

Similar to how you may have used the Git Bash terminal for your pre-work, WSL will give a you Bash terminal – but with the full power of a complete Linux distribution for development.

However, it is a tool that's actively in development, and the development experience on WSL will not be exactly the same as on a native Linux installation.

The biggest differences for our classroom use are that the installation for various tools may require additional steps, and unlike Git Bash, all of our files will live inside the WSL environment. This means that while using WSL we need to be mindful that our files exist in the Linux environment, so we will be installing and using exclusively the Linux version of tools rather than Windows tools. (With the exception of VS Code, which is able to interoperate with WSL seamlessly)

## Installing WSL
The following instructions are pulled from the [Microsoft Install WSL](https://docs.microsoft.com/en-us/windows/wsl/install) page and will work for Windows 10 
version 2004 and higher (Build 19041 and higher).

> To check your Windows version and build number, select **Windows logo key + R**, type **winver**, select OK.

If you have an older version of Windows, consult the [manual installation steps](https://docs.microsoft.com/en-us/windows/wsl/install-manual) on the Microsoft site.

Open `powershell` as an **admin**. Once powershell opens, run the following commands within that shell:
```
wsl --install
```

Next set the default version to 2 (WSL2):
```
wsl --set-default-version 2
```

Next install the Linux distribution Ubuntu:

```
wsl --install -d Ubuntu 
```

Once the download completes, you should be prompted with a terminal window:

![Bash](https://docs.microsoft.com/en-us/windows/wsl/media/ubuntuinstall.png)

Enter a username and password. We recommend setting these something easy to type and remember!

Type in your desired username and press the `enter` key to submit.

Then type in your desired password, and also press the `enter` key to submit. 
> Note that your password will be invisible as you type it!

## Updating The Linux Environment
Before proceeding, run the following command in your Ubuntu terminal:

```
sudo apt update
```
---

## Windows Terminal 
Head over to the the [Microsoft Store](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701) to install the Windows Terminal Application.

Windows terminal gives you more flexibility and customization options with your terminal window with features like tabs and color themes.

Once you have Windows Terminal installed, open the Settings menu to change the default profile to Ubuntu

![profile](https://i.imgur.com/bwivlBQ.png)

Then configure Windows Terminal to open at the home `~` directory:
1. Go to Settings -> Profiles -> Ubuntu -> Click on 'Open JSON file' in the bottom left
2. Open the JSON file with VS Code or Notepad
3. Under "profiles" -> "list" find the one with `"name": "Ubuntu"`, and add:

```
    "startingDirectory" : "//wsl$/Ubuntu/home/<Your Ubuntu Username>"
```

Example of what it'll look like:

![bash](https://i.imgur.com/VfIqPAd.png)


You can do lots of customization in Windows Terminal, highly recommend checking out some of the settings!

---

## Visual Studio Code

Text editors are a personal choice. One of the most popular open source text editors these days, for good reason, is Visual Studio Code.

> Note: VS Code's _keyboard shortcuts_ are different than the shortcuts used by the Sublime or Atom editors. If you already know Sublime's shortcuts and don't want to learn those of VS Code, it's possible to configure VS Code to use Sublime's.

Download and install VS Code from [https://code.visualstudio.com/](https://code.visualstudio.com/).

Once VS Code is installed, open it using the command

```
code .
```

You will see that it automatically does an additional installation for WSL that looks like so:

![install](https://i.imgur.com/SnoTF0J.png)


Once VS Code is open, go to the 'Extensions' tab on the left side and install the `Remote - WSL` extension.

![extension](https://i.imgur.com/DNfBIfs.png)

---

## Installing Zsh and Oh-My-Zsh

### Installing Zsh

Zsh is an extension of the regular bash shell that many computers use as default. It provides us with features that the regular bash shell does not have.

Install Zsh by running the following command in your terminal:

```sh
sudo apt install zsh
```

### Installing Oh-My-Zsh

Oh-My-Zsh is an extension of the Zsh prompt. It provides us with useful information in a clear and legible format.

Install Oh-My-Zsh by running the following command in your terminal:

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

A prompt will appear to ask if you want to switch your shell to Zsh, type in `Y` to select Yes.

Close your terminal and re-open it. Oh-My-Zsh should now load by default.

---

## Git


[Github](https://github.com/) provides a way to host Git repos in the cloud.  It enables collaboration and is wildly popular.

You should have already opened a personal Github account, however, you need to have a General Assembly Github Enterprise account as well.  You can get one by signing up here:  [https://git.generalassemb.ly/join](https://git.generalassemb.ly/join)

#### Installation
We can use the `apt` program to install Git:

```
sudo apt install git
```


### Configuration
Enter the following commands into your terminal:

Replace "Your Name" with your GitHub username.
```
git config --global user.name "Your Name"
```

Replace youremail@domain.com with the email you have registered with GitHub.
```
git config --global user.email "youremail@domain.com"
```

#### Configuring git to default to a branch named `main`

GitHub (in the cloud) now defaults newly created remote repos to use a default branch named `main` instead of `master`.  To ensure that when you create a local repo (using `git init`) it does the same, run the following command:

```
git config --global init.defaultBranch main
```

#### Configuring git's "pull" Mode:

Run the following command to inform how git should merge fetched commits:

```
git config --global pull.rebase true
```

#### Configuring git to use VS Code as its Editor

There will be a time when git needs info and automatically opens an editor.  The default editor used by git is usually vim or nano - and neither is very user friendly.  The following command will set git's editor to VS Code:

```
git config --global core.editor "code --wait" 
```

#### Configuring a Global git ignore

> Note: **THIS STEP IS CRITICAL**

Everyone should have a global **git ignore** file so that you don’t have to worry about making the appropriate entries in a project’s git ignore.

First, create the file:  `touch ~/.gitignore_global`

Next, configure git to use this file:  `git config --global core.excludesfile ~/.gitignore_global`

Finally, lets put some good stuff in there by editing the newly created `.gitignore_global` file using VS Code:

1. `code ~/.gitignore_global` to open the file in VS Code

2. Copy/paste the following into `~/.gitignore_global`:

```sh
# This is a list of rules for ignoring files in every Git repositories on your computer.
# See https://help.github.com/articles/ignoring-files

# Compiled source #
###################
*.class
*.com
*.dll
*.exe
*.o
*.so

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Logs and databases #
######################
*.log

# OS generated files #
######################
._*
.DS_Store
.DS_Store?
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# Testing #
###########
.rspec
capybara-*.html
coverage
pickle-email-*.html
rerun.txt
spec/reports
spec/tmp
test/tmp
test/version_tmp

# node #
########
node_modules

# Rails #
#########
**.orig
*.rbc
*.sassc
.project
.rvmrc
.sass-cache
/.bundle
/db/*.sqlite3
/log/*
/public/system/*
/tmp/*
/vendor/bundle


# Ruby #
########
*.gem
*.rbc
.bundle
.config
.yardoc
_yardoc
doc/
InstalledFiles
lib/bundler/man
pkg
rdoc
tmp

# for a library or gem, you might want to ignore these files since the code is
# intended to run in multiple environments; otherwise, check them in:
# Gemfile.lock
# .ruby-version
# .ruby-gemset

# CTags #
#########
tags

# Env #
#######
.env

# Python #
#######
*.pyc
__pycache__/

# Misc #
.eslintcache

```

3. Save the file.

#### Avoiding Having to Create A Git Message Every Time a Git Merge Takes Place

By default, git asks for a commit message any time a merge takes place, for example, you'll be running this command quite a bit:  `git pull upstream main`.

To avoid this from happening, we can add a single line to our terminal configuration - this is the line we're going to need to add anywhere inside of the file identified below:

```
export GIT_MERGE_AUTOEDIT=no
```

**For ZSH users:**

Use VS Code to edit the `~/.zshrc` file:

```
code ~/.zshrc
```

**If NOT using ZSH:**

Use VS Code to edit the `~/.bash_profile` file:

```
code ~/.bash_profile
```

Copy the `export GIT_MERGE_AUTOEDIT=no` to the bottom of the chosen file and save it.

**Regardless of which file you edited, be sure to save it.  You will also need to quit terminal and relaunch it for this setting to take effect.**

---

## Node.js

Node is a JavaScript engine for the backend. We use it to power our web servers and connect to our databases.

We'll use a tool called Node Version Manager (nvm) to install the latest version.

You can check out their documentation for the latest install scripts [here](https://github.com/nvm-sh/nvm#install--update-script).


#### Installation 

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | zsh
```

Close and re-open your terminal.

Install the latest version of node:
```
nvm install node
```


#### Verifying the Install

Verify the installation afterwards by running:

```
node -v
npm -v
```

The above commands should display versions without any errors. To verify that all the required permissions are set correctly, try to install a package such as the useful _nodemon_ globally:

```
npm install -g nodemon
```

## Installing PostgreSQL

PostgreSQL is going to be our relational database of choice for this course. Install it by running the following command in your terminal:

```sh
sudo apt install postgresql
```

Once the installation completes, run the next command in your terminal to confirm the installation:

```sh
psql --version
```

To start the postgres service, enter the following command in your terminal:

```sh
sudo service postgresql start
```
> Note: After restarting your computer, you may need to run the `sudo service postgresql start` command again to start and access the database.

Enter the postgres shell as an admin:
```sh
sudo -u postgres psql
```

Next we'll create a SUPER USER. Change "your_linux_username" to your linux username:

```sh
CREATE USER your_linux_username WITH SUPERUSER LOGIN;
```

To exit the shell:

```sh
\q
```

Once postgres starts, enter the following command in your terminal.

```sh
createdb `whoami`
```

## Installing MongoDB

Install **MongoDB** using `apt` using the following commands:

```
sudo apt install mongodb
```

### Starting the MongoDB Server

You start the Mongo database server with the following command:

```
sudo service mongodb start
```

> Note: After restarting your computer, you may need to run the `sudo service mongodb start` command again to start and access the database.


## Installing Python 3

> Note: Due to time constraints and for simplicity, we will not be using Python "virtual environments" during SEI.  If you are familiar with using virtual environments, you may continue to use them.  If you decide to continue to develop using Python beyond SEI, your next step would be to learn about using virtual environments.

`apt` is also used to install Python 3. 

Install **Python** with this command: 

```
sudo apt install python3
``` 

You can test the installation by running `python3 --version`.

Next install Python 3's package manager, `pip3` 

```
sudo apt install python3-pip
```

Test that it was installed by running `pip3 --version`.


Next we need to add the packages that we can install using pip to the `PATH`

Open up either `.zshrc` or `.bash_profile` if you're using ZSH or BASH respectively:

``` 
code ~/.zshrc

# OR if you're using bash
code ~/.bash_profile
```

Then paste this line to the bottom of the file, replacing your_user_name with your linux username:
```
# To allow pip packages to be in PATH
path+=(/home/your_user_name/.local/bin)
```

## Installing Django

We will use `pip3` to install Django, a robust web framework for Python. We will be installing the latest version (3.x.x):

```
pip3 install Django
```

If you receive a "permissions" error, try this command:

```
pip3 install --user Django
```
