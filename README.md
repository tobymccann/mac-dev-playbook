# Mac Development Ansible Playbook

[![Build Status](https://travis-ci.org/tobymccann/mac-dev-playbook.svg?branch=master)](https://travis-ci.org/tobymccann/mac-dev-playbook)

This playbook installs and configures most of the software I use on my Mac for web and software development. Some things in macOS are slightly difficult to automate, so I still have some manual installation steps, but at least it's all documented here.

This is a work in progress, and is mostly a means for me to document my current Mac's setup. I'll be evolving this set of playbooks over time.

*See also*:

  - [osxc](https://github.com/osxc)
  - [MWGriffin/ansible-playbooks](https://github.com/MWGriffin/ansible-playbooks) (the original inspiration for this project)

## Installation

  1. [Install Ansible](http://docs.ansible.com/intro_installation.html).
  2. Ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
  3. Clone this repository to your local drive.
  4. Run `$ ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
  5. Run `ansible-playbook main.yml -i inventory -K` inside this directory. Enter your account password when prompted.

> Note: If some Homebrew commands fail, you might need to agree to XCode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.

## Overriding Defaults

Not everyone's development environment and preferred software configuration is the same.

You can override any of the defaults configured in `default.config.yml` by creating a `config.yml` file and setting the overrides in that file. For example, you can customize the installed packages and apps with something like:

    homebrew_installed_packages:
      - cowsay
      - git
      - go
    
    mas_installed_app_ids:
      - 443987910 # 1Password
      - 498486288 # Quick Resizer
      - 557168941 # Tweetbot
      - 497799835 # Xcode

Any variable can be overridden in `config.yml`; see the supporting roles' documentation for a complete list of available variables.

## Included Applications / Configuration (Default)

Applications (installed with Homebrew Cask):

  - [Docker](https://www.docker.com/)
  - [Dropbox](https://www.dropbox.com/)
  - [Fing](https://www.fing.io/)
  - [Google Chrome](https://www.google.com/chrome/)
  - [Handbrake](https://handbrake.fr/)
  - [Homebrew](http://brew.sh/)
  - [Java](https://java.com)
  - [MacVim](http://macvim-dev.github.io/macvim/)
  - [Menu Meters](https://www.ragingmenace.com/software/menumeters/) (Note: Currently using [this fork](http://member.ipmu.jp/yuji.tachikawa/MenuMetersElCapitan/) for compatibility)
  - [Sequel Pro](https://www.sequelpro.com/) (MySQL client)
  - [Slack](https://slack.com/)
  - [Transmit](https://panic.com/transmit/) (S/FTP client)
  - [Vagrant](https://www.vagrantup.com/)
  - [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  - [VLC](http://www.videolan.org/vlc/index.html)

Packages (installed with Homebrew):

  - atom
  - autoconf
  - bash-completion
  - findutils
  - goeip
  - gettext
  - git
  - gnutls
  - go
  - gpg
  - hub
  - httpie
  - iperf
  - libdvdcss
  - libevent
  - packer
  - python
  - sqlite
  - mcrypt
  - mysql
  - npm
  - nvm
  - php70
  - php70-mcrypt
  - php70-xdebug
  - ssh-copy-id
  - cowsay
  - readline
  - subversion
  - openssl
  - pv
  - drush
  - wget
  - wrk

My [dotfiles](https://gitlab.com/jkennemer/dotfiles) are also installed into the current user's home directory, including the `.osx` dotfile for configuring many aspects of macOS for better performance and ease of use.

Finally, there are a few other preferences and settings added on for various apps and services.

## Future additions

### Things that still need to be done manually

It's my hope that I can get the rest of these things wrapped up into Ansible playbooks soon, but for now, these steps need to be completed manually (assuming you already have Xcode and Ansible installed, and have run this playbook).

  1. Set JJG-Term as the default Terminal theme (it's installed, but not set as default automatically).
  2. Install [Sublime Package Manager](http://sublime.wbond.net/installation).
  3. Install all the apps that aren't yet in this setup (see below).
  4. Remap Caps Lock to Escape (requires macOS Sierra 10.12.1+).
  5. Set trackpad tracking rate.
  6. Set mouse tracking rate.
  7. Configure extra Mail and/or Calendar accounts (e.g. Google, Exchange, etc.).

### Applications/packages to be added:

These are mostly direct download links, some are more difficult to install because of custom installers or other nonstandard install quirks:

  - [iShowU HD](http://www.shinywhitebox.com/downloads/iShowU_HD_2.3.20.dmg)
  - [Adobe Creative Cloud](http://www.adobe.com/creativecloud.html)

### Configuration to be added:

  - I have vim configuration in the repo, but I still need to add the actual installation:
    ```
    mkdir -p ~/.vim/autoload
    mkdir -p ~/.vim/bundle
    cd ~/.vim/autoload
    curl https://raw.githubusercontent.com/tpope/vim-pathogen/master/autoload/pathogen.vim > pathogen.vim
    cd ~/.vim/bundle
    git clone git://github.com/scrooloose/nerdtree.git
    ```

## Testing the Playbook

Don't test on your own Macbook! Instead, follow these instructions from Jeff Geerling on how to build a [Mac OS X VirtualBox VM](https://github.com/geerlingguy/mac-osx-virtualbox-vm). Continually run and re-run this playbook to test changes and make sure things work correctly.

Additionally, this project is [continuously tested on Travis CI's macOS infrastructure](https://travis-ci.org/tobymccann/mac-dev-playbook).

## Ansible for DevOps

Check out [Ansible for DevOps](https://www.ansiblefordevops.com/), which teaches you how to automate almost anything with Ansible.

## Author

[Jason Kennemer](http://www.jasonkennemer.com/), 2017 (originally inspired by [Jeff Geerling:geerlingguy/mac-dev-playbook](https://github.com/geerlingguy/mac-dev-playbook)[MWGriffin/ansible-playbooks](https://github.com/MWGriffin/ansible-playbooks)).
