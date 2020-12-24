# Windows survival guide for linuxians

> I've used Linux for about 10+ years now. Here's what I setup on windows.

## Windows installation and initial Setup

- Source an *up to date* [Windows ISO](https://www.microsoft.com/en-gb/software-download/windows10ISO)
- To prepare a usb based instalation from Linux, you can use [WoeUSB](https://github.com/slacka/WoeUSB) : It'll setup the ISO to USB with UEFI support
- Install windows. Deactivate any network connections as windows may force you to create an online account instead of a normal local one.

Once Windows is installed:

- Install [Chocolatey](https://chocolatey.org/), avoid [Scoop](https://github.com/lukesampson/scoop) or use it exclusively for packages that don't work well with chocolatey
- Use [DisableWinTracking](https://github.com/10se1ucgo/DisableWinTracking/releases/) to clean stuff a bit
- Update Windows, of force an update if you have a outdated Windows installation.
- Install [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (require a system restart)
- Change windows time to UTC if using dual boot with linux :

    ``` powershell
    Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_QWORD /d 1
    ```

- Reboot
- Go to the initial setup of [WSL](#WSL) (setup name, hostname..). Use [shellconfig](https://github.com/replicajune/shellconfig) to spice up your shell

## Tools

### Package manager

[Chocolatey](https://chocolatey.org) helps to install packages for windows the way apt or yum would do.

> As an alterntive to Chocolatey, you can use [Scoop](https://scoop.sh/). It will uses "portable" versions and install stuff for a given user (the application data/folders will be located into the user directory). Use Chocolatey by default if you're not sure about Scoop, as app integration can be hazardous with the later.

Install chocolatey with powershell as admin:

``` powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

### Utilities

- [DisableWinTracking](https://github.com/10se1ucgo/DisableWinTracking): Disable tracking, remove onedrive
- [Bulk Crap Uninstaller](https://www.bcuninstaller.com): removing adwares and pre-installed (windows) components
- [7zip](https://www.7-zip.org/): to replace to winrar, winzip..
- [SysinternalsSuite](https://docs.microsoft.com/en-us/sysinternals/downloads/): a couple of utilities, including [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer) and [Autoruns](https://docs.microsoft.com/en-us/sysinternals/downloads/autoruns)
- [Veracrypt](https://www.veracrypt.fr/en/Downloads.html): Setup encrypted drives. Known as a safe alternative to bitlocker, and compatible with Linux
- [Keypirinha](https://keypirinha.com/): A launcher, similar to Alfred, spotlight, Ulauncher..
- [Microsoft-windows-terminal](https://github.com/Microsoft/Terminal): Terminal from Microsoft

### Workflows:

- [Github Desktop](https://desktop.github.com/): git client (use https scheme for your local clones, instead of ssh)
- [VScode](https://code.visualstudio.com/): IDE, compatible with *Github Desktop* ([Atom](https://atom.io/) is also a good option)
- [meld](http://meldmerge.org/): graphical tool to manage merge conflicts

### Linux, VM

Some stuff will need a proper Linux installation instead of WSL, you might want to use :

- [Vagrant](https://www.vagrantup.com/) : automatic provision of VMs with Virtualbox (or Hyper-V if you're into that)
- [Virtualbox](https://www.virtualbox.org/) : a backend for Vagrant

### WSL

I made a dedicated post about [WSL2](https://notes.pericat.work/post/linux-cont-on-win/) from WSL2 installation and setup to using podman and spawning containers with WSL2

#### WSL Legacy

> I'll remove this section soon. Update windows and use WSL2, it's way better :)

You might not have access to WSL2 on an old version of windows. If it is your case, either upgrade, or fallback to WSL1.

[WSL1](https://docs.microsoft.com/en-us/windows/wsl/about) ships with flavors of Linux distributions instead of being a dedicated flavor "like" Cygwin is, meaning that you'll use your WSL instance as Ubuntu, Fedora, Suse, etc..

Once you've installed WSL1, you'll need a flavor.

> Be careful when importing files from Windows and WSL1 environment, as file encoding between *DOS* and *UNIX* are not the same.. To convert a file using vim, do `:set ff=unix`. A tool called dos2unix to do the same : `dos2unix $FILE`.

> Generally speaking, its quite a bad idea to mix files used by wsl1 and windows, partially because of that problem. Recents updates made that thing a bit less painful but it still cause issues from time to time.

> I've deleted the upgrade section for WSL1 its content became old an obsolete. Refer to commit history to see what was valid.

### Other tools and apps

I personally like those tools on any windows installation :thumbsup: :

- [Brave](https://laptop-updates.brave.com/latest/winx64) : use chromium, with security by design and have a neat adblocker included.
- [Winamp](https://www.winamp.com/) : it's still alive !
- [Spotify](https://www.spotify.com/fr/download/windows) : needs no introduction.
- [BleachBit](https://www.bleachbit.org/download/windows) : because the other candidate bacome unreliable.
