---
title: "How I fixed arch linux on my Surface 3"
subtitle: ""
date: 2024-03-25T03:57:01-05:00
lastMod: 2024-03-25T21:48:16-05:00
author: ""
image: "anhack-surface3-arch-gnome.jpeg"
imageAlt: "Arch on Surface3"
category: ""
tags: ["linux","arch","surface3"]
toc: true
draft: false
---

Just got this Surface 3 as a hand-me-down. And I wanted to breathe some new life into it.

Plus it'd be cool to have a small x86 computer to run around with. Who knows I may use it as a dedicated radio demodulator or something else fun.

There's actually a lot of support for these computers. Honestly I had no idea.
The [Linux Surface Project](https://github.com/linux-surface/linux-surface) on github addresses most of the problems you'd run into with installing linux on a Surface.

I had a problem though. Support for the Surface 3 hasn't really kept up with the rest of the line.
And some of the recommended fixes for problems I ran into didn't work or, at most, partially worked.

I've worked with this computer for the last couple of days and have finally got it to a point where I'm happy. Bluetooth and the cameras still don't work (but to be honest I wasn't going to use them). Most importantly to me however, the touchscreen controller isn't crashing any more and the backlight controls *finally* work and are playing well with gnome.

If you've run into the same issues that I have and haven't been able to find a fix yet. I hope this helps! :)

---

# List of Fixes

List of all fixes that worked on my surface 3

DEVICE INFO: Kernel 6.8.1 Arch; GNOME 45.5;
Surface 3; 2GB Ram

## General Surface Drivers and Support

[Arch install](https://github.com/linux-surface/linux-surface/wiki/Installation-and-Setup#arch)

[Linux Surface Project](https://github.com/linux-surface/linux-surface)

[`libwacom-surface` driver](https://aur.archlinux.org/packages/libwacom-surface) can be installed through the AUR.

Even though it's not needed, I did install the marvel firmware for the wifi.

## Broken Drivers

### Touchscreen

Problem: Touchscreen controller randomly dies.

Fix: Added `intel_idle.max_cstate=1 i915.enable_dc=0 intel_iommu=off iommu=off` to kernel settings.

### Backlight

Problem: Backlight controls do not work.

Fix: Rebuild kernel with two drivers (pwm and i2c) switching places.

This causes the drivers to load in a different order. It's more of a hack than anything.

---

# Step by step

This is exactly what I did to install arch with gnome and get the touchscreen and backlight to work.

## Install Arch
<https://wiki.archlinux.org/title/Installation_guide>
Follow this guide for the initial setup before you get to the chroot part.

### Preface

I do recommend changing the font in the live environment
```sh
># setfont ter-132b
```

And mount boot efi disk to `/boot` and not `/boot/efi`

---

### After Chroot
Once you're in root partition

#### Set timezone
```sh
># ln -sf /usr/share/zoneinfo/<Region>/<City> /etc/localtime
```

#### Update hardware clock
```sh
># hwclock --systohc
```

#### Generate locales

edit `/etc/locale.gen` and uncomment `en_US.UTF-8 UTF-8` and other needed UTF-8 locales

```sh
># locale-gen
```

```sh
/etc/locale.conf
---------------------------------------
LANG=en_us.UTF-8
```

#### Set terminal font
```sh
># pacman -S terminus-font
```

```sh
/etc/vconsole.conf
---------------------------------------
FONT=ter-132b
```

#### Set hostname

```sh
/etc/hostname
---------------------------------------
<yourhostname>
```

#### Install text editors for later
```sh
># pacman -S vi vim
```

#### Set root password

```sh
># passwd
```

---

### Install linux-surface project
These commands are subject to change. I will write out everything that I did so that maybe you can find where something went wrong

```sh
># curl -s https://raw.githubusercontent.com/linux-surface/linux-surface/master/pkg/keys/surface.asc | sudo pacman-key --add -
```

```sh
># pacman-key --finger 56C464BAAC421453
```

```sh
># pacman-key --lsign-key 56C464BAAC421453
```

#### Add repository to the end of `pacman.conf`

```sh
/etc/pacman.conf
---------------------------------------
[linux-surface]
Server = https://pkg.surfacelinux.com/arch/
```

#### Install main packages for linux-surface

```sh
># pacman -Syu linux-surface linux-surface-headers iptsd
```

#### Install additional packages we will need later

```sh
># pacman -S linux-firmware-marvell intel-ucode sudo networkmanager
```

This is everything for `linux-surface` for now, but we'll get back to it later.

---

### Install grub

```sh
># pacman -S grub efibootmgr
```

```sh
># grub-mkconfig -o /boot/grub/grub.cfg
```

#### Create update-grub script

```sh
/usr/sbin/update-grub
---------------------------------------
#!/bin/sh
set -e
exec grub-mkconfig -o /boot/grub/grub.cfg "$@"
```

```sh
># chown root:root /usr/sbin/update-grub
```

```sh
># chmod 755 /usr/sbin/update-grub
```

#### Install into `/boot`

```sh
># grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```

#### Update grub config

Change line `GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet"`

```sh
/etc/default/grub
---------------------------------------
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet intel_idle.max_cstate=1 i915.enable_dc=0 intel_iommu=off iommu=off"
```

The setting: `intel_idle.max_cstate=1 i915.enable_dc=0 intel_iommu=off iommu=off`, along with the wacom driver (that we will install later) will fix the issue of the touchscreen controller randomly dying some time after boot.

```sh
># update-grub
```

---

### Create user

```sh
># useradd -m -g users -G wheel,video <username>
```

#### Set new user password

```sh
># password <username>
```

#### Enable sudo for new user

```sh
># visudo
```

This will open the sudoers file

Uncomment either:

`%wheel ALL=(ALL:ALL) ALL` For sudo access for the wheel group

`%wheel ALL=(ALL:ALL) NOPASSWD: ALL` Same thing without a password

### Done with Arch install

```sh
># exit
```

```sh
># reboot
```

## Login as user

### Setup NetworkManager

```sh
>$ systemctl enable NetworkManager
```

```sh
>$ systemctl start NetworkManager
```

```sh
>$ nmcli device wifi connect <SSID> password <password>
```

### Install gnome

```sh
>$ sudo pacman -S gnome
```

```sh
>$ systemctl enable gdm.service
```

```sh
>$ reboot
```

### Install yay

```sh
>$ sudo pacman -S git base-devel
```

```sh
>$ git clone https://aur.archlinux.org/yay-bin.git
```

```sh
>$ cd yay-bin/
```

```sh
>$ makepkg -si
```

### Install libwacom-surface

```sh
>$ yay -S libwacom-surface
```

### Install onscreen keyboard panel button

```sh
>$ sudo pacman -S firefox gnome-browser-connector
```

Open firefox and go to <https://extensions.gnome.org/>

Install the browser extension

Search for `Enhanced OSK` and install

In the preferences for `Enhanced OSK` enable "Show Panel Indicator"

### Disable login screen

#### On boot

Go to Settings > Users > Automatic Login : Enable

#### Out of suspend

```sh
>$ gsettings set org.gnome.desktop.screensaver lock-enabled false
```

### Rebuild the Kernel

This is the only way that I have found to make the backlight controller work.
There is a [forum post](https://gitlab.freedesktop.org/drm/intel/-/issues/26) discussing this issue. But the gist is you have two competing drivers and the wrong one is loaded first. To fix this we have to recompile the kernel.

Config settings that have worked for people in kernel version 5.6.13

```
CONFIG_PWM=y
CONFIG_PWM_CRC=y
CONFIG_I2C_DESIGNWARE_PLATFORM=y
CONFIG_I2C_DESIGNWARE_PCI=m
CONFIG_INTEL_SOC_PMIC=y
CONFIG_DRM_I915=m
```

For arch-6.8.1 the only ones we need to change are `CONFIG_PWM_CRC` and `CONFIG_I2C_DESIGNWARE_PCI`

{{< panel "caution" >}}
Caution: kernel build files use approximately 10-12 GB of disk space, and the build took me around 5 hours to complete.
{{< /panel >}}

---

#### Alright so lets get into it

```sh
>$ git clone https://github.com/linux-surface/linux-surface.git
```

```sh
>$ cd linux-surface/pkg/arch/kernel/
```

Get checksum of default config

```sh
>$ sha256sum config 
```

Keep this output for a bit later

##### Edit kernel configuration

```sh
config
---------------------------------------
CONFIG_PWM_CRC=y
...
CONFIG_I2C_DESIGNWARE_PCI=m
```

Now you have to resign the config file

```sh
>$ sha256sum config
```

Take the output of that command and place it into `PKGBUILD`

```sh
PKGBUILD
---------------------------------------
sha256sums=('SKIP'
            '<checksum>'
            ...)
```

Replace old config checksum with the new one.

It should be the second one in the list right after `'SKIP'`

But use the old checksum we got from earlier to confirm.

Replace checksum and save `PKGBUILD`

##### Build kernel

```sh
>$ PKGEXT=".pkg.tar" MAKEFLAGS="-j8" makepkg -s --skippgpcheck
```

##### Install new kernel package

```sh
>$ sudo pacman -U linux-surface-*.pkg.tar
```

```sh
>$ sudo update-grub
```

```sh
>$ reboot
```

And that's it. That is everything I've done to make gnome arch working on my surface 3.

# References & Resources

<https://wiki.archlinux.org/title/Installation_guide>

<https://github.com/linux-surface/linux-surface/wiki/Installation-and-Setup#arch>

<https://github.com/linux-surface/linux-surface/wiki/Surface-3>

<https://github.com/linux-surface/linux-surface/tree/master/pkg/arch>

<https://gitlab.freedesktop.org/drm/intel/-/issues/26>