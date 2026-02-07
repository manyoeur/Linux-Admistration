# How to configure DHCPv4 on Ubuntu/Debian Server
## 1. Install the ISC DHCP Server package
```
sudo apt update
sudo apt install isc-dhcp-server
```
## 2. Set the network interface the DHCP server should listen on
Edit the default configuration file:
```
sudo nano /etc/default/isc-dhcp-server
```
Find the line:
```
INTERFACESv4=""
```
Set your interface (example: ens33, eth0, etc.):
```
INTERFACESv4="eth0"
```
To check your interface name:
## 3. Configure DHCP settings

You have to backup your default configuration file

``
sudo cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.back
``

Then start to configure file below

```
sudo nano /etc/dhcp/dhcpd.conf
```
Example basic DHCP configuration
```

# Default lease times
default-lease-time 600;
max-lease-time 7200;

# Authoritative DHCP server
authoritative;

# Subnet configuration
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.10 192.168.10.200;
    option routers 192.168.1.1;
    option subnet-mask 255.255.255.0;
    option domain-name-servers 8.8.8.8, 1.1.1.1;
    option domain-name "local.lan";
}
```
## 4. Enable and restart the DHCP server
```

sudo systemctl enable isc-dhcp-server
sudo systemctl restart isc-dhcp-server
```
## 5. Check DHCP server status
```
systemctl status isc-dhcp-server
```
## 6. Check for configuration errors
```

sudo journalctl -xe
sudo tail -f /var/log/syslog
```
## 7. Verify DHCP leases
```
cat /var/lib/dhcp/dhcpd.leases
```
## 8. Assign static IP reservations (optional)
```

host printer01 {
    hardware ethernet AA:BB:CC:DD:EE:FF;
    fixed-address 192.168.10.50;
}
```
## Run a syntax/config test (if service not start)
```
sudo dhcpd -t -4 -cf /etc/dhcp/dhcpd.conf
```
* No output means syntax is OK.
* If there’s an error, fix the reported line in /etc/dhcp/dhcpd.conf and retest.

# How to Configure DHCPv4 on Redhat/CentOS
## 1. Install the DHCP Server package
```
sudo yum install -y dhcp
```
## 2. Locate the DHCP configuration files
* Main config:
```
/etc/dhcp/dhcpd.conf
```
* backup configuration file
```
cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.back
```
* Service file
```
/usr/lib/systemd/system/dhcpd.service
```
## 3. Configure the DHCP server
```
sudo nano /etc/dhcp/dhcpd.conf
```
* Example DHCPv4 configuration
```

default-lease-time 600;
max-lease-time 7200;
authoritative;

subnet 192.168.2.0 netmask 255.255.255.0 {
    range 192.168.2.100 192.168.2.200;
    option routers 192.168.2.1;
    option subnet-mask 255.255.255.0;
    option domain-name-servers 8.8.8.8, 1.1.1.1;
    option domain-name "local.lan";
}
```
## 4. Assign the listening interfaces
```
sudo nano /etc/sysconfig/dhcpd
```
Find:
```
DHCPDARGS=
```
Example:
```
DHCPDARGS=eth0
```
If serving multiple interfaces:
```
DHCPDARGS="eth0 eth1"
```
## 5. Enable and start the DHCP service
```
sudo systemctl enable dhcpd
sudo systemctl start dhcpd
sudo systemctl status dhcpd
```
If it fails, check logs:
```
sudo journalctl -u dhcpd -xe
sudo tail -n 100 /var/log/messages
```
## 6. Open the DHCP port in firewalld
```

sudo firewall-cmd --add-service=dhcp --permanent
sudo firewall-cmd --reload
```
## 7. Verify DHCP leases
```
cat /var/lib/dhcpd/dhcpd.leases
```
## 8. Add static IP reservations (optional)
nside dhcpd.conf:
```

host server01 {
    hardware ethernet AA:BB:CC:DD:EE:FF;
    fixed-address 192.168.50.10;
}
```
