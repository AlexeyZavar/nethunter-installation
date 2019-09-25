# Intro
We'll install it with [Linux Deploy](https://play.google.com/store/apps/details?id=ru.meefik.linuxdeploy)

This instruction is for opp6t, but can be reproduced on the other devices (btw you need special nethunter kernel)

# Stage 0: Installing dependences
Install [DJY's](https://github.com/johanlike/DJY-Oneplus6-or-Oneplus6T-Nethunter-Andrax-Kernel) kernel

Install [Magisk module](https://drive.google.com/file/d/16PS3NMm4Rf8-InuktamXA8U69VskBYqA/view?usp=sharing)

Install [BusyBox from Magisk repo or from GitHub](https://github.com/Magisk-Modules-Repo/busybox-ndk)

You're ready!

# Stage 1: Downloading rootfs & Linux Deploy
Download & install [Linux Deploy](https://play.google.com/store/apps/details?id=ru.meefik.linuxdeploy)

Download [kalifs](https://build.nethunter.com/kalifs/kalifs-latest/kalifs-armhf-full.tar.xz) and place in at */sdcard/kalifs-armhf-full.tar.xz* (*/storage/emulated/0/kalifs-armhf-full.tar.xz*)

Using any root file explorer, create folders at "*/data/local/nhsystem/kali-armhf*"

# Stage 2: Installing Nethunter

Open Linux Deploy and set settings as shown on the [pictures (click)](https://imgur.com/a/6DxbfAQ)

Click on 3 dots in top right corner -> Install

Wait 5-7 minutes

Then click STOP, wait, START

# Stage 3: Configuring Nethunter

Open Terminal -> Android su

Click on 3 dots in top right corner -> Config Chroot Path and replace "*arm64*" with "*armhf*"

Restart Terminal -> Kali

Finally, write "**apt update && apt upgrade -y && apt dist-upgrade -y**" to update Nethunter

# Troubleshooting

#### apt update
If you'll try to "**apt update**" - you may get an error

To fix that write "**apt-key adv --keyserver hkp://keys.gnupg.net --recv-keys 7D8D0BF6**", but if it doesn't works - replace "*7D8D0BF6*" with key that can't be verified (specified in "apt update" error)

#### ssh
If you need to start ssh - "**service ssh start**"

But you may can't connect to your phone

To fix that write "**nano /etc/ssh/sshd_config**" and find "*PermitRootLogin yes*" - uncomment it. Now find "*UsePAM yes*" and replace it with "*UsePAM no*"

Now "**passwd**" to change root password if needed & "**service ssh restart**"

#### iptables
Nethunter contains 2 versions of "**iptables**", so default doesn't works for me

Simply write "**mkdir -p /root/scripts  && mv /usr/sbin/iptables /root/scripts/ && ln -s /usr/sbin/iptables-legacy /usr/sbin/iptables**"

#### HID
Open Nethunter app -> USB Army -> USB Interface -> hid -> Set USB interface

HID interface may not be displayed in Nethunter, but it does exists :)

# Decorations

## Zsh
### Installation
Do "**apt install zsh -y**"

Then we need to install [Oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) - "**git clone https://github.com/robbyrussell/oh-my-zsh.git && cd oh-my-zsh && ./oh-my-zsh.sh**"

Install it as default shell

### dikiaap's dot files
I've installed [this](https://github.com/dikiaap/dotfiles) dot files, so they're working almost perfect.

"**git clone https://github.com/dikiaap/dotfiles**", then "**cd dotfiles && ./install.sh && zsh**"

You can add your functions in "~/.functions", for example:
```sh
# Update
apt-update() {
    sudo apt update
    sudo apt upgrade -y
    sudo apt dist-upgrade -y
    apt-clean
}
```

If there'll be any problems:

#### z
Run "**wget https://raw.githubusercontent.com/rupa/z/master/z.sh && mkdir ~/.zsh/plugins/z && mv z.sh ~/.zsh/plugins/z/z.sh**"

#### .functions_private && .exports_private
Just create these files ("**touch ~/.functions_private && touch ~/.aliases_private**") or remove their references in ~/.zshrc

#### Numpad buttons (PuTTY)
Run "**touch ~/.numpad**", add in end of "*~/.zshrc*" "**source ~/.numpad**" add in this file these lines:
```sh
# Keypad
# 0 . Enter
bindkey -s "^[Op" "0"
bindkey -s "^[Ol" "."
bindkey -s "^[OM" "^M"
# 1 2 3
bindkey -s "^[Oq" "1"
bindkey -s "^[Or" "2"
bindkey -s "^[Os" "3"
# 4 5 6
bindkey -s "^[Ot" "4"
bindkey -s "^[Ou" "5"
bindkey -s "^[Ov" "6"
# 7 8 9
bindkey -s "^[Ow" "7"
bindkey -s "^[Ox" "8"
bindkey -s "^[Oy" "9"
# + -  * /
bindkey -s "^[Ok" "+"
bindkey -s "^[Om" "-"
bindkey -s "^[Oj" "*"
bindkey -s "^[Oo" "/"
```
[Source](https://superuser.com/questions/742171/zsh-z-shell-numpad-numlock-doesnt-work)
