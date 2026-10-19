### About

This project is a fork from [mrclksr/linux-browser-installer](https://github.com/mrclksr/linux-browser-installer), updated chroot environment with debian stable and added more browsers

`freebsd-browser-installer` is a Bourne shell script to install Linux versions of
the Brave, Chrome, Edge, Opera, Vivaldi and other browsers under FreeBSD into a Linux
(Debian stable) chroot.
They allow you to use web services like *Netflix*, *Prime Video*, or *Spotify*
which require [Widevine](https://en.wikipedia.org/wiki/Widevine).
The script is based on the excellent [Howto](https://forums.freebsd.org/threads/linuxulator-how-to-run-google-chrome-linux-binary-on-freebsd.77559/) by @[patovm04](https://github.com/patovm04).

A modified version of FreeBSD's linux rc-script
(`rc.d/debian`) is used to start the *linuxulator*, and to mount the chroot's
filesystems.

### System requirements

FreeBSD 12.2-RELEASE or higher

### Please Note

You can't run different Linux chroots at the same time. If you want to run
rl9-based applications under `/compat/linux`, you have to set
`sysctl compat.linux.emul_path=/compat/linux`, and start the linux rc-script
(`service linux onestart`). Depending on which chroot you intend to use by
default, set either (not both) `linux_enable="YES"` or `debian_enable="YES"`
in `/etc/rc.conf`.

### Supported browsers

```
brave - Brave Browser
braveorigin - Brave Origin
chrome - Google Chrome
edge - Microsoft Edge
firefox - Mozilla Firefox
firefoxesr - Mozilla Firefox ESR
firefoxdevedition - Mozilla Firefox Developer Edition
floorp - Floorp Browser
librewolf - Librewolf
opera - Opera Browser
operagx - Opera GX
vivaldi - Vivaldi Browser
```

### Usage

Clone the repository and change to the `freebsd-browser-installer` directory.

````
$ git clone https://github.com/arfshl/freebsd-browser-installer.git
$ cd freebsd-browser-installer
````

Proceed as user root with the following steps.

#### Install browser

````
# ./freebsd-browser-installer install <browser>
````

If the chroot is not existing yet, it will be created first.

Run `/usr/local/bin/linux-<browser>`
to start your installed browser.

#### Uninstall browser

````
# ./freebsd-browser-installer uninstall <browser>
````

This command uninstalls the browser, and removes its wrapper
scripts from `/usr/local/bin` and `$chroot_path/bin` along with its
desktop file.

#### Create chroot

````
# ./freebsd-browser-installer chroot create
````

#### Upgrade software installed in the chroot

````
# ./freebsd-browser-installer chroot upgrade
````

#### Delete chroot

````
# ./freebsd-browser-installer chroot delete
````

Before deleting the entire chroot under `$chroot_path`, this command
unmounts all the chroot's filesystems, deletes the rc script, and removes its
variable(s) from `/etc/rc.conf`.

### Debugging

FreeBSD desktop files is located on `/usr/local/share/applications/linux-<browser>`

FreeBSD starter script (FreeBSD side launcher defined in `starter.tmpl`) is located on `/usr/local/bin/linux-<browser>`

`chroot`wrapper script (Debian side launcher defined in `chroot-wrapper-*.tmpl`) is located on `/compat/debian/usr/local/bin/bsd-<browser>`

chroot to debian shell directly (Run as root)
```
chroot /compat/debian /bin/bash
```

Run command inside chroot directly from freebsd shell
```
chroot /compat/debian (command)
```

[Firefox cli parameter list](https://firefox-source-docs.mozilla.org/browser/CommandLineParameters.html)

[Chromium cli switch list](https://peter.sh/experiments/chromium-command-line-switches/)

[Chromium cli parameter list](https://thorium.rocks/docs/cmdline_flags.html)