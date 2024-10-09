+++
title = "Setup Hyprland in bare metal Void Linux"
date = "2024-10-08 00:47:38"
taxonomies.tags = ["voidlinux", "hyprland", "wayland", "linux", "installation"]
+++

All the commands with sudo in front can be run from the root account or the chroot environment without writing sudo in front.

## Configure the timezone
Information about timezones are stored in the `/usr/share/zoneinfo/` directory. As I live in Dhaka, my zoneinfo file is located at `/usr/share/zoneinfo/Asia/Dhaka`.
```
sudo ln -sf /usr/share/zoneinfo/<timezone> /etc/localtime
```

## Install fonts
Here we are installing a nerd font (I like Iosevka) and a Bangla font as because I am Bangladeshi.
```
sudo xbps-install xz unzip aria2
aria2c https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/Iosevka.tar.xz
aria2c https://ekushey.org/download-font?cp-ekushey-font-id=70

sudo mkdir -p /usr/share/fonts/iosevka
sudo mkdir -p /usr/share/fonts/solaimanlipi

sudo tar xvf Iosevka.tar.xz -C /usr/share/fonts/iosevka
sudo unzip SolaimanLipi.zip -d /usr/share/fonts/solaimanlipi

rm Iosevka.tar.xz SolaimanLipi.zip
```

## Install necessary programs
```
sudo xbps-install mesa-dri elogind polkit Waybar wofi kitty chromium nwg-look pulseaudio pavucontrol network-manager-applet
```

## Install hyprland
Add the hyprland repository
```
sudo echo "repository=https://raw.githubusercontent.com/Makrennel/hyprland-void/repository-x86_64-glibc" > /etc/xbps.d/hyprland-void.conf
```
Sync repositories
```
sudo xbps-install -S
```
Install hyprland and xdg-desktop-portal-hyprland
```
sudo xbps-install hyprland xdg-desktop-portal-hyprland
```

## Enable necessary services
```
ln -s /etc/sv/elogind /etc/runit/runsvdir/default/ 
ln -s /etc/sv/polkitd /etc/runit/runsvdir/default/
```

Now reboot and after login type `Hyprland` in the tty and it will launch hyprland.
