- ## Configure Wi-Fi

### Network Manager (nmcli)

* Install Network Manager
  
  ```
  sudo apt install network-manager
  ```

* Discover network information for all network interfaces
  
  ```
  nmcli device show
  ```

* If device is unmanaged run following command
  
  ```
    sudo nmcli dev set "wifi-card-name" managed yes
  ```

* Can use nice Python 3 script
  
  ```
  https://github.com/NoahCristino/easywifi
  ```

--------------------------

### Improve WiFi connection by disabling power management for the wireless card

For some wireless chipsets a simple tweak is sufficient for increasing the connection quality a lot. Namely disabling the power management for the wireless chipset. The speed of your wireless internet may then increase also.

No worries: this tweak won't disable power management for your entire machine. It'll only disable it for the WiFi chipset.

There are two ways to do it: an easy method and a harder one. Below, I'll describe both ways, because even the harder method has its use: it shows more clearly what you're doing than the "magical terminal incantation" of the easy method.

The easiest way: improving your WiFi connection by executing a single command
2.1.1. The easiest way to improve your WiFi connection by disabling power management for the WiFi chipset (for that chipset alone, not systemwide), is this:

a. First you need to find out whether Mint applies power management to your WiFi chipset. For this, launch a terminal window.
(You can launch a terminal window like this: *Click*)

b. Type in the terminal:

```
iwconfig
```

You can then not only see the name for your wireless chipset (for example: wlp2s0), but also whether Power Management is on for it. When it's off, or when no mention is made of Power Management at all, you don't need to do anything.

When Power Management is on, proceed as follows:

c. Use copy/paste for transferring the following blue line into the terminal (don't try to type it!):

```
sudo sed -i 's/3/2/' /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
```

d. Reboot your computer.

e. Then check in the terminal, by the command iwconfig, whether Power Management for the wireless chipset is off now.

If so, you're done!

The harder way: improving your WiFi connection by editing a file manually
2.1.2. You can also edit a configuration file by hand, in order to disable power management for the Wifi chipset. It's a bit more difficult than the method described in item 2.1.1, but you can do it as follows:

a. First you need to find out whether Mint applies power management to your wireless chipset. For this, launch a terminal window.
(You can launch a terminal window like this: *Click*)

b. Type in the terminal:

```
iwconfig
```

You can then not only see the name for your wireless chipset (for example: wlp2s0), but also whether Power Management is on for it. When it's off, or when no mention is made of Power Management at all, you don't need to do anything.

c. When Power Management is on, proceed as follows.

In order to prevent typos, copy/paste the following blue line into the terminal (it's one line!):

```
xed admin:///etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
```

d. Now a text file opens. In that text file, you see the following content:

```
[connection]
wifi.powersave = 3
```

**Change 3 into 2.**

Save the modified file and close it.

e. Reboot your computer.

f. Then check in the terminal, by the command iwconfig, whether Power Management for the wireless chipset is off now.

If so, you're done!\

### DNS Problem

resolv.conf -   DNS config

```
sudo nano /etc/resolv.conf
```

```
nameserver 8.8.8.8
nameserver 1.1.1.1
```

---