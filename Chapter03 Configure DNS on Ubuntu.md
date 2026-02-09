# How to setup DNS Server on Ubuntu
## 1. Update Your System
```
sudo apt update && sudo apt upgrade -y
```
## 2. Install BIND9 (DNS Server Software)
```
sudo apt install bind9 bind9utils bind9-doc -y
```
Check if the service is running:
```
systemctl status bind9
```
## 3. Configure the DNS Zone
Create a zone file for your domain (example.com)
Edit the main config:
```
sudo nano /etc/bind/named.conf.local
```
Add the following:
```

zone "example.com" {
    type master;
    file "/etc/bind/zones/db.example.com";
};
```
Create the zones directory:
```
sudo mkdir /etc/bind/zones
```
## 4. Create the Zone File
```
sudo nano /etc/bind/zones/db.example.com
```
Paste this template (edit your domain & IPs):
```
$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                        2         ; Serial
                        604800    ; Refresh
                        86400     ; Retry
                        2419200   ; Expire
                        604800 )  ; Negative Cache TTL
;
@               IN      NS      ns1.example.com.
ns1             IN      A       192.168.1.10

@               IN      A       192.168.1.10
www             IN      A       192.168.1.10
```
Replace:
* example.com → your domain
* 192.168.1.10 → server IP
* admin.example.com. → your email (replace @ with .)
## 5. Configure Reverse Zone (Optional)
If your IP is 192.168.1.10, then reverse zone = 1.168.192.in-addr.arpa
Edit:
```
sudo nano /etc/bind/named.conf.local
```
Add:
```

zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.192";
};
```
Create reverse file:
```
sudo nano /etc/bind/zones/db.192
```
Paste:
```
$TTL 604800
@   IN  SOA ns1.example.com. admin.example.com. (
        1
        604800
        86400
        2419200
        604800 )
;
@             IN  NS   ns1.example.com.
10            IN  PTR  example.com.
```
## 6. Check Config for Errors
```
sudo named-checkconf
```
Check zone files:
```

sudo named-checkzone example.com /etc/bind/zones/db.example.com
sudo named-checkzone 1.168.192.in-addr.arpa /etc/bind/zones/db.192
```
If all OK → continue.
## 7. Restart and Enable BIND9
```
sudo systemctl restart bind9
sudo systemctl enable bind9
```
## 8. Configure Ubuntu to Use Your Own DNS Server
```
sudo nano /etc/resolv.conf
```
Add:
```
nameserver 192.168.1.10
```
For Netplan (permanent):
```
sudo nano /etc/netplan/01-netcfg.yaml
```
Example:
```

nameservers:
    addresses: [192.168.1.10, 8.8.8.8]
```
Apply:
```
sudo netplan apply
```
## 9. Test DNS Resolution
Test A record:
```
dig @192.168.1.10 example.com
```
Test CNAME or www:
```
dig @192.168.1.10 www.example.com
```
Reverse lookup:
```
dig @192.168.1.10 -x 192.168.1.10
```
If you see “ANSWER SECTION”, your DNS is working.
