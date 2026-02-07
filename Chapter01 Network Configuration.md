# Set static IP address in Ubuntu
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
# Enable DHCPv4 client on Ubuntu
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
# How to set static IP address in CentOS
## Method 1: Using nmtui (Text UI – easiest)
```
sudo nmtui
```
Then:

1.Select Edit a connection

2.Choose your interface (e.g., eth0 or ens33)

3.Set IPv4 CONFIGURATION to Manual

4.Enter:

* Address: 192.168.1.100
* Netmask: 255.255.255.0
* Gateway: 192.168.1.1

5.Add DNS server(s): 8.8.8.8, 1.1.1.1
6.Save and quit
7.Restart network:
