# Development Environment macOS

This guide covers my peronal preferences and tools for a development environment on a new Mac. I have used [this](http://sourabhbajaj.com/mac-setup/) guide as a reference.

## Xcode
Xcode is an integrated development environment for macOS containing a suite of software development tools developed by Apple for developing software for macOS, iOS, watchOS and tvOS.

For installing Xcode command line tools run:

```bash
xcode-select --install
```

It'll prompt you to install the command line tools. Follow the instructions and you'll have Xcode and Xcode command line tools both installed.

## Homebrew

[Homebrew](https://brew.sh/) calls itself The missing package manager for macOS and is an essential tool for any developer.

To install Homebrew run the following: terminal, hit Enter, and follow the steps on the screen:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Upgrade and cleanup packages:

```bash
brew update
brew upgrade
brew cleanup -s
```

This will:

* update the local base of available packages and versions, to know what is updatable
* installs new version of outdated packages
* removes outdated downloads and remove old versions of installed formulae
* allow you to keep only linked versions (by default, the last) and save some disk space

### Cask

[Homebrew-Cask](https://caskroom.github.io/) extends Homebrew and allows you to install large binary files via a command-line tool. 

You need Homebrew on your system to use Cask:

```bash
brew tap caskroom/cask
```

## Quick Look Plugins

These plugins add support for the corresponding file type to Mac Quick Look (In Finder, mark a file and press Space to start Quick Look).

```bash
brew cask install \
    qlcolorcode \
    qlstephen \
    qlmarkdown \
    quicklook-json \
    qlprettypatch \
    quicklook-csv \
    betterzip \
    webpquicklook \
    suspicious-package
```

## iTerm2, Fonts

* [iTerm2](http://www.iterm2.com/) is an open source replacement for Apple's Terminal. It's highly customizable and comes with a lot of useful features.
* The Z shell (also known as zsh) is a Unix shell that is built on top of bash (the default shell for macOS) with additional features. It's recommended to use zsh over bash. It's also highly recommended to install a framework with zsh as it makes dealing with configuration, plugins and themes a lot nicer.

Install fonts, iterm2 and zsh:

```bash
brew tap caskroom/fonts && brew cask install font-source-code-pro iterm2 zsh
```

### Colors and Font Settings
Here are some suggested settings you can change or set, they are all optional.

* Set hot-key to open and close the terminal to command + option + i
* Go to profiles -> Default -> Terminal -> Check silence bell to disable the terminal session from making any sound
* Download one of iTerm2 color schemes and then set these to your default profile colors. We will use the Solarized scheme. http://ethanschoonover.com/solarized/files/solarized.zip
* Change the cursor text and cursor color to yellow make it more visible
* Change the font to 14pt Source Code Pro Lite.

## Oh My ZSH

[Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh/) is an open source, community-driven framework for managing your zsh configuration. It comes with a bunch of features out of the box and improves your terminal experience.

Install Oh My Zsh:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### Plugins
Add plugins to your shell by adding the name of the plugin to the plugin array in your .zshrc.

```
plugins=(git colored-man colorize pip python brew osx zsh-syntax-highlighting httpie docker vscode)
```

You'll find a list of all plugins on the [Oh My Zsh Wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins).

### Themes
Changing theme is as simple as changing a string in your configuration file. The default theme is `robbyrussell`. Just change that value to change theme, and don't forget to apply your changes.

```
ZSH_THEME=pygmalion
```

You'll find a list of themes with screenshots on the [Oh My Zsh Wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes).

## Git

Let's install the latest version of Git:

```bash
brew install git
```

Next, we'll define your Git user:

```bash
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```

## SSH Config  

There 's no $HOME/.ssh config when you did not use SSH before. Start with "ssh-ing" to a server (e.g. github.com):

```bash
ssh github.com
```

Generate a new SSH key:

```bash
ssh-keygen -t rsa -C "your_email@example.com"
```

Run the following commands to add your SSH key to the ssh-agent.

```bash
eval "$(ssh-agent -s)"
```

If you're running macOS Sierra 10.12.2 or later, you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain:

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

No matter what operating system version you run you need to run this command to complete this step:

```bash
ssh-add -K ~/.ssh/id_rsa
```

## Visual Studio Code

Just started using Visual Studio Code instead of SublimeText. Not sure yet which is my favorite.

```bash
brew cask install visual-studio-code
```

## IntelliJ IDEA

This is my favorite IDE for development using Golang, Java or Javascript. If you're a student or an instructor (teaching staff members) all IDEs from JetBrains are free to use. You can read more on [their website](https://www.jetbrains.com/student/). If you're not a student they still offer a few free Community Edition (CE) IDEs.

Community Edition:

```bash
brew cask install intellij-idea-ce
```

Ultimate Edition:

```bash
brew cask install intellij-idea
```

## Python

macOS, like Linux, ships with Python already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.). 

[pyenv](https://github.com/yyuu/pyenv) is a Python version manager that can manage and install different versions of Python. 

```bash
brew install pyenv
```

You can install a specific Python version with:

```bash
pyenv install 3.7.1
```

Install pip for managing Python packages:

```bash
curl https://bootstrap.pypa.io/get-pip.py > get-pip.py
sudo python get-pip.py
```

## Java

Install OpenJDK 11:

```bash
brew cask install java
```

## Golang

Go (also known as Golang) is an open source programming language maintained by Google.

```bash
brew install golang
```

## Vagrant

Create and configure lightweight, reproducible, and portable development environments. [Vagrant](http://www.vagrantup.com/) is a tool for managing virtual machines via a simple to use command line interface.

Vagrant uses Virtualbox to manage the virtual dependencies. 

```bash
brew cask install virtualbox vagrant vagrant-manager
```

## Docker

[Docker](https://docs.docker.com/) is a platform for developers and sysadmins to develop, ship, and run applications.

Docker for Mac is the current release of Docker for macOS and can be downloaded here:
https://docs.docker.com/docker-for-mac/install/

## Terraform

Hashicorp [Terraform](https://www.terraform.io/) enables you to safely and predictably create, change, and improve infrastructure.

```bash
brew install terraform
```

## Ansible

[Ansible](https://www.ansible.com/) is an open source tool for automating configuration management, service orchestration, cloud provisioning and application deployment. Ansible is "agentless", using SSH to push changes from a single source to multiple remote resources. Commands can be invoked either ad hoc on the command line or via "playbooks" written in YAML.

```bash
brew install ansible
```

## AWS CLI

The AWS Command Line Interface (CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

Install:

```bash
brew install awscli
```

See:
* https://docs.aws.amazon.com/cli/latest/userguide/installing.html
* https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html

## Google Cloud SDK

The Google Cloud SDK is a set of tools for the Google Cloud Platform and includes the `gcloud` command line tool.

```bash
brew cask install google-cloud-sdk
```

See:
* https://cloud.google.com/sdk/docs/quickstart-macos

## Kubernetes CLI

Kubectl is a command line interface for running commands against Kubernetes clusters.

```bash
brew install kubernetes-cli
```

https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl

In Docker for Mac 17.12 Edge (mac45) and higher, and 18.06 Stable (mac70) and higher, a standalone Kubernetes server is included that runs on your Mac, so that you can test deploying your Docker workloads on Kubernetes.

It is also possible to use Minikube for your local Kubernetes environment. With Minikube you can configure another container, network-plugin, drivers, different kubernetes version, persistent volumes an other addons like ingress, efk, kube-dns, dashboard, etc.

```bash
brew cask install minikube
```

See:
* https://kubernetes.io/docs/tasks/tools/install-kubectl/
* https://kubernetes.io/docs/setup/minikube/
* https://github.com/kubernetes/minikube/blob/master/docs/README.md


## Other Apps

This will install the following productivity and office apps:

```bash
brew cask install \
    aware \
    boostnote \
    caffeine \
    dropbox \
    google-chrome \
    insomnia \
    safeincloud-password-manager \
    slack \
    the-unarchiver \
    vlc    
```