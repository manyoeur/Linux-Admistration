#Configuration and Management Commands

These commands are used for setting up and modifying network interfaces, addresses, and routing tables. 

* ```ip```: The primary command for showing and manipulating routing, network devices, and addresses.

* ```ip addr show``` or ```ip a```: Displays all network interfaces and their IP addresses, netmasks, and other details.

* ```ip addr add [ip_address/mask] dev [interface]```: Assigns an IP address to a specific interface.

* ```ip link set [interface] up or down```: Enables or disables a network interface.

* ```ip route show```: Displays the kernel's IP routing table.

* ```ifconfig```: An older command (Interface Configuration) still found on some systems for displaying and configuring network interfaces. It can set IP addresses, netmasks, and enable/disable interfaces.

* ```iwconfig```: Specific to wireless network interfaces, used to view or set parameters like SSID and signal strength.

* ```hostname```: Displays or sets the system's hostname.

* ```hostnamectl set-hostname [new_hostname]```: A modern command to control the system hostname with systemd.

* ```route```: An older command used to display or modify the IP routing table.

* ```nmcli```: A command-line client for NetworkManager, a dynamic network management daemon, often used on desktop and server systems to manage connections interactively. 

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
sudo nano /etc/netplan/01-network-manager-all.yaml
```
Then add values as bellow:
```

network:
  version: 2
  renderer: networkd
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
