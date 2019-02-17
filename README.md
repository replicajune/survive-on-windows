> I've used Linux for about 10+ years now. Here's what I setup on windows.

# Setup

## Initial actions

-   Source an *up to date* [Windows ISO](https://www.microsoft.com/en-gb/software-download/windows10ISO)
-   To prepare a usb based instalation from Linux, you can use [WoeUSB](https://github.com/slacka/WoeUSB) : It'll setup the ISO to USB with UEFI support
-   Install windows
-   Use [DisableWinTracking](https://github.com/10se1ucgo/DisableWinTracking/releases/) to clean stuff a bit
-   Update Windows, of force an update if you have a outdated Windows installation
-   Change windows time to UTC if using dual boot with linux :

``` powershell
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_QWORD /d 1
```

-   Reboot
-   Install [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
-   Go to the initial setup of WSL (setup name, hostname..)

# Tools

Here is a selection of tools to have around :

## Chocolatey

[Chocolatey](https://chocolatey.org) helps to install packages for windows the way apt or yum would do. As a powershell admin, do :

```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

Almost all tools given bellow are available wih Chocolatey and are most of the time installed doing  `choco install package_name`

## Utilities

-   [7zip](https://www.7-zip.org/) : to replace to winrar, winzip..
-   [KeepassXC](https://keepassxc.org/download/#windows) : if you don't have any passwords manager already, this one is a great choice
-   [SysinternalsSuite](https://docs.microsoft.com/en-us/sysinternals/downloads/) : a couple of utilities, including [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer) and [Autoruns](https://docs.microsoft.com/en-us/sysinternals/downloads/autoruns)
-   [Veracrypt](https://www.veracrypt.fr/en/Downloads.html) : Setup encrypted drives. Known as a safe alternative to bitlocker, and compatible with Linux
-   [Scoop](https://github.com/lukesampson/scoop) : a command-line installer for Windows, alternative to Chocolatey

## Workflows : Git, ssh ...

-   [cmder](http://cmder.net/) : Terminal, WSL compatible
-   [Github Desktop](https://desktop.github.com/) : git client (use https scheme for your local clones, instead of ssh)
-   [Atom](https://atom.io/) : IDE, compatible with *Github Desktop* ([VScode](https://code.visualstudio.com/) is also a good option)

## Linux, VM

Some stuff will need a proper Linux installation instead of WSL, you might want to use :

-   [Vagrant](https://www.vagrantup.com/) : automatic provision of VMs with Virtualbox (or Hyper-V if you're into that)
-   [Virtualbox](https://www.virtualbox.org/) : a backend for Vagrant

# WSL

[WSL](https://docs.microsoft.com/en-us/windows/wsl/about) is a tool to interact with an Unix shell under Windows. Until some years ago, [Cygwin](https://www.cygwin.com/) was the way to go 100% of the time, but today WSL offer a way more interesting integration to windows than Cygwin. WSL also ship with flavors of Linux distributions instead of being a dedicated flavor like Cygwin, meaning that you'll use your WSL instance as Ubuntu, Fedora, Suse, etc..

Exemples given bellow assume you chosed **ubuntu** as your WSL provider.

## Setup

Basic utilities are always welcomed :

```
sudo apt update -y && apt install \
  openssh-client \
  git \
  htop \
  vim \
  tmux
```

### Dotfiles

I've a couple of custom stuff set in `.bash_wsl`. To source that in `.bashrc`, I have this :

``` bash
if [ -f /home/${SUDO_USER-$USER}/.bash_wsl ]; then
    source /home/${SUDO_USER-$USER}/.bash_wsl
fi
```

- Then in `/root/.bashrc` (or the main `bashrc` config file), I have that set up :

``` bash
if [ -f /home/${SUDO_USER}/.bashrc ]; then
    source /home/${SUDO_USER}/.bashrc
fi
```

The files sourced in `.bash_wsl` are included in this repository and must be set in your home folder. They are :

-   `.bash_agent` : init an ssh agent with environment variables when you spawn a term
-   `.bash_aliases` : some bash aliases..

Be careful when importing files from Windows and WSL environment, as file-formats between *DOS* and *UNIX* are not the same.. To convert a file using vim, do :

``` vim
:set ff=unix
```

Generally speaking, its quite a bad idea to mix files used by wsl and windows, partially because of that problem.

> Note that this "guide" is using bash exclusively, but WSL is compatible with any shells. When launching wsl, just add your prefered shell, like : `wsl sh` !

## Upgrade WSL

You might need to update *WSL* at some point. Two options exists : One using `lxrun`, the other one through *WSL*.

### Using WSL

This is a bit like a `dist-upgrade` :

``` bash
do-release-upgrade
```

> :information_source: one or more reboot might be needed.

### Via `lxrun`

> :warning: This will **wipe** your *WSL* installation. **BACKUP EVERYTHING** :warning:

-   Uninstall *WSL* :

``` powershell
lxrun /uninstall /full /y
```

-   Go back to the [Windows store](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-your-linux-distribution-of-choice), install *WSL*, and setup everything again/back.


# Other nice stuff

I personally like those tools on any windows installation :thumbsup: :

-   [Rambox](https://rambox.pro/#home) : multi-client accounts manager (mails & IMs mainly).
-   [Brave](https://laptop-updates.brave.com/latest/winx64) : use chromium, with security by design and have a neat adblocker included.
-   [Winamp](https://www.winamp.com/) : it's still alive !
-   [Spotify](https://www.spotify.com/fr/download/windows) : needs no introduction.
-   [BleachBit](https://www.bleachbit.org/download/windows) : because the other candidate is becoming a bit weird lately..
