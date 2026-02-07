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
