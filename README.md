# My-dots
## Gentoo installation
I used the Gentoo amd64 handbook (https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation) and this video (https://youtu.be/t0nPxDlFL2I?si=FyU1lBa7gS3blI2J) to make my setup.

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
To connect to a wifi network we will use the `wpa_cli` tool. Before we can use it we have to set it up.
To do that we have to create a WPA supplicant configuration file.

_/etc/wpa_supplicant/wpa_supplicant.conf_
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

Now you have to start the wpa_supplicant service.
```
# rc-service wpa_supplicant start
```

After the setup is done we can start the wpa_cli application.
```
# wpa_cli
```

To setup the connection you have to run the following commands inside of this application and it should look similar like this.
```
> scan
OK
> scan_results
bssid / frequency / signal level / flags / ssid
<...> <...> <...> <...>
> add_network
0
> set_network 0 ssid "<network_ssid>"
OK
> set_network 0 psk "<network_password>"
OK
> enable_network 0
OK
> save_config
OK
> quit
```
> [!NOTE]
> Logs like "<3>CTRL_EVENT_SCAN_STARTED" or "<3>CTRL_EVENT_NETWOR_NOT_FOUND" etc. can be ignored.

You can check if it worked in here.
```
# ip link
```
If the link for the wifi entry shows UP it is connected.

### Partitioning
To check what drives are currently connected we can call this command.
```
# lsblk
```

At the beginning we want to override all data that was on it bevor for safety reasons.
```
# dd if=/dev/urandom of=/dev/<name-of-drive> bs=4096 status=progress
```

We will use parted to partition our disks. Open it by typing this.
```
parted /dev/<name-of-drive>
```
