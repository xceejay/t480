# t480 Random Notes

This and that...

## Bluetooth

I'm using AirPod Pros with my T480, they work great.

* pacman -S bluez bluez-utils pulseaudio-bluetooth
* pulseaudio -k
* sudo systemctl start bluetooth
* sudo systemctl enable bluetooth
* bluetooth-ctl
    * power on
    * scan on
    * pair <mac>
    * connect <mac>
* Follow instructions [here](https://wiki.archlinux.org/index.php/Bluetooth_headset#Setting_up_auto_connection) to setup auto connect

## Firefox

Fix monospace font:
* Preferences -> Fonts and Colors -> Advanced -> Change Monospace to Source Code Pro -> Uncheck "Allow pages to choose their own fonts, instead of your selections above" -> Ok

Add-ons:
* uBlock Origin
* Imagus
* Dark Reader
* Stylus
    * [GitHub Dark](https://github.com/StylishThemes/GitHub-Dark)
    * [Dark Wikipedia](https://userstyles.org/styles/42313/dark-wikipedia)
    * [StackOverflow Dark](https://github.com/StylishThemes/StackOverflow-Dark)
    * [A Dark Hacker News](https://userstyles.org/styles/22794/a-dark-hacker-news)
    * [Stylus Dark - ShadowFox](https://userstyles.org/styles/153739/stylus-dark-shadowfox)
* [TTV ad-block](https://github.com/odensc/ttv-ublock)
    * Currently blocks ads on Twitch.

## Ghidra

* Edit -> Tool Options -> Tool
    * Swing Look and Feel -> "CDE/Motif"
    * Use Inverted Colors (Enabled)

## KVM/QEMU/libvirt

```
$ sudo pacman -S qemu virt-manager libguestfs dnsmasq vde2 bridge-utils ebtables iptables
$ # ^ hit yes on any iptable package replacement warnings
$ sudo systemctl enable libvirtd.service
$ sudo systemctl start libvirtd.service
$ sudo vim /etc/libvirt/libvirtd.conf
$ # unix_sock_group = "libvirt"
$ # unix_sock_rw_perms = "0770"
$ sudo usermod -a -G libvirt user
$ newgrp libvirt # or logout & back in
$ cat br1.xml 
<network>
  <name>br1</name>
  <forward mode='nat'/>
  <bridge name='virbr1' stp='on' delay='0'/>
  <ip address='192.168.69.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.69.128' end='192.168.69.254'/>
    </dhcp>
  </ip>
</network>
$ sudo virsh net-define br1.xml
$ sudo virsh net-start br1
$ sudo virsh net-autostart br1
$ sudo virsh net-list --all
$ brctl show
$ sudo systemctl restart libvirtd.service
$ virt-manager
```

## Ranger Icons

~/.Xresouces needs to use "Sauce Code Pro":
```
URxvt*font:     xft:SauceCodePro Nerd Font Mono:size=12
URxvt*boldFont: xft:SauceCodePro Nerd Font Mono:size=12
```

Need at minimum this package (AUR): `nerd-fonts-source-code-pro`

Then install ranger_devicons:
```
$ git clone https://github.com/alexanderjeurissen/ranger_devicons
$ cd ranger_devicons/
$ make install
```

## Steam Audio / pavucontrol issue

Some apps in Steam use OpenALsoft and you can't change the audio output in pavucontrol...

Create `~/.alsoftrc`:
```
[pulse]
allow-moves=yes
```

It will fix the problem.

## Urxvt tabbed

Add this to `~/.Xresources`

```
! tabs
URxvt.perl-ext-common: tabbed
URxvt.tabbed.tabbar-fg: 3
URxvt.tabbed.tabbar-bg: 0
URxvt.tabbed.tab-fg: 7
URxvt.tabbed.tab-bg: 0
```

## VSCodium

Change font:
* File -> Preferences -> Settings -> Text Editor -> Font -> Font Family -> "Source Code Pro"

Extensions:
* Python
* Go
* Code Spell Checker
