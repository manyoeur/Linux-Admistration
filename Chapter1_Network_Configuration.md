# Configuration and Management Commands

These commands are used for setting up and modifying network interfaces, addresses, and routing tables. 
## How to check IP address in Ubuntu
* ```ip```: The primary command for showing and manipulating routing, network devices, and addresses.

* ```ip addr show``` or ```ip a```: Displays all network interfaces and their IP addresses, netmasks, and other details.

* ```ip addr add [ip_address/mask] dev [interface]```: Assigns an IP address to a specific interface.

* ```ip link set [interface] up or down```: Enables or disables a network interface.

* ```ifconfig```: An older command (Interface Configuration) still found on some systems for displaying and configuring network interfaces. It can set IP addresses, netmasks, and enable/disable interfaces.
## Display routing table
* ```ip route show```: Displays the kernel's IP routing table.
* ```route```: An older command used to display or modify the IP routing table.
* ```iwconfig```: Specific to wireless network interfaces, used to view or set parameters like SSID and signal strength.
## To display hostname of the system
* ```hostname```: Displays or sets the system's hostname.

* ```hostnamectl set-hostname [new_hostname]```: A modern command to control the system hostname with systemd.

* ```nmcli```: A command-line client for NetworkManager, a dynamic network management daemon, often used on desktop and server systems to manage connections interactively. 
# Shutdown Linux command line
Shutdown Linux from the Command Line
```
sudo shutdown now
```
Shutdown at a specific time (e.g., 1 minute from now)
```
sudo shutdown +1
```
Shutdown at a specific clock time (shutdown at 10:30 PM)
```
sudo shutdown 22:30
```
Power off the system immediately
```
sudo poweroff
```
 Use systemctl (modern method)
 ```
sudo systemctl poweroff
```
Halt the system (stop CPU, no power off)
```
sudo halt
```
Shutdown in old system
```
sudo init 0
```
# How to reboot Linux system
```
sudo reboot
```
Using the systemd method
```
sudo systemctl reboot
```
Reboot now using shutdown command
```
sudo shutdown -r now
```
Schedule a reboot (example: reboot in 5 minutes)
```
sudo shutdown -r +5
```
 Cancel a scheduled reboot
 ```
sudo shutdown -c
```

## Set static IP address in Ubuntu
Open the Netplan Configuration File
Common locations:
* /etc/netplan/01-network-manager-all.yaml (desktop)
* /etc/netplan/50-cloud-init.yaml (server)
* /etc/netplan/*.yaml
```
ls /etc/netplan
```
Open the file in a text editor:
```
sudo nano /etc/netplan/50-cloud-init.yaml.yaml
```
Then add values as bellow:
```

network:
  version: 2
  ethernets:
    enp3s0:
      dhcp4: false
      addresses:
        - 192.168.1.50/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1
```
Replace:

* enp3s0 → your interface
* IP values with your network
Then restart Netplan by using command below:
```
sudo netplan apply
```
Verify the IP Address
```
ip a
ip route
systemd-resolve --status
```
## Enable DHCPv4 on Ubuntu 24.04 Server
Check your network interface name
```
ip a
```
On Ubuntu Server, the common file is:
```
sudo nano /etc/netplan/50-cloud-init.yaml
```
Set DHCPv4 to true
```

network:
  version: 2
  ethernets:
    ens160:
      dhcp4: true
```
If you previously had a static IP, remove or comment out:
* addresses:
* gateway4:
* nameservers:
Apply the configuration
```
sudo netplan apply
```
