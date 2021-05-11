# Guide

## Install pacakges

`sudo pacman -S xf86-video-xxx xorg xorg-init nitrogen picom qtile`

## Copy xorg config

`cp /etc/X11/xinit/xinitrc /home/username/.xinitrc`

## Edit .xinitrc

Remove the last lines and add

```bash
nitrogen --restore &
picom &
exec qtile
```
