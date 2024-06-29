# My-dots
## Gentoo installation
I used the Gentoo amd64 handbook (https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation) and these videos (https://youtu.be/t0nPxDlFL2I?si=FyU1lBa7gS3blI2J, https://youtu.be/IzUf-wFEirQ?si=AwLTT8W90rOZmUlB) to make my setup.

### Preparation
After booting into the minimal install on the boot device it promts for a keyboard layout. If chosen "de" a few of the keys are still wrong. So i set the keymap manualy.
```
# loadkeys de-latin1
```

### Testing the network
We want to check if we have a working internet connection because that is needed for the installation. First we see if we can ping. It should just work if the laptop/pc is connected via a ethernet cable.
```
# ping archlinux.org
```
Additional information can be gathered with the following command.
```
# ip route
# ip link
# ip address
```

### Connect to wifi
To connect to a wifi network we will use the `wpa_cli` tool. First we have to start it.
```
# wpa_cli
```



Note: If a wifi connection is needed i recommend to use another boot install device that provides a networkmanager

### Partitioning
To check what drives are currently connected we can call this command.
```
# lsblk
```

At the beginning we want to override all data that was on it bevor for safety reasons.
```
# dd if=/dev/urandom of=/dev/<name-of-drive> bs=4096 status=progress
```
