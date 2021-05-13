# ArchLinux installation

## Change KeyMaps

```bash
ls /usr/share/kbd/keymaps/**/*.map.gz | less

loadkeys es
```

## Check Internet connection

```bash
ping www.google.com
```

## Update the system clock

```bash
timedatectl set-ntp true
```

## Partition List

Make a GPT partition

| Label | Type       | Size |
|-------|------------|------|
| /boot | EFI        | 512M |
| /swap | Swap       | 8G   |
| /     | FileSystem | Left |

## Format

### Boot

`mkfs.fat -F32 /dev/sda1`

### Swap

`mkswap /dev/sda2`

`swapon /dev/sda2`

### Root

`mkfs.ext4 /dev/sda3`

## Mount

`mount /dev/sda3 /mnt`

`mkdir /boot`

`mount /dev/sda1 /boot/`

## Intallation base

`pacstrap /mnt base linux linux-firmware`

## Generate fstab

`genfstap -U /mnt >> /mnt/etc/fstab`

## Enter into the new installation

`arch-chroot /mnt`

## Set Timezone

`ln -sf /usr/share/zoneinfo/Europe/Madrid /etc/localtime`

## Hwclock

`hwclock --systohc`

## Set Local

`nano /etc/locale.gen`

Uncomment the line `es_ES.UTF-8 UTF-8`

`locale-gen`

## Keymap

`nano /etc/vconsole.conf`

KEYMAP=es

## Hostname

`nano /etc/hostname`

```text
myhostname
```

## Hosts

`nano /etc/hosts`

```text
127.0.0.1	localhost
::1		    localhost
127.0.1.1	myhostname.localdomain	myhostname
```

## Root pass

`passwd` and set the root password

## Add user

`useradd -m username`

`passwd username`

## Groups

`usermod -aG wheel,audio,video,optical,storage username`

## Install Sudo

`pacman -S sudo`

## Edit sudoers

`EDITOR=nano visudo`

Uncomment the line `%wheel ALL=(ALL) ALL` and all the users on the group `wheel` have sudo privileges using `sudo` command

## GRUB

`pacman -S grub efibootmgr os-prober`

`grub-install /dev/sda --target=x86_64-efi --efi-directory=/boot` 

`grub-mkconfig -o /boot/grub/grub.cfg`

## Networkmanager

`pacman -S networkmanager`

`systemctl enable NetworkManager`

