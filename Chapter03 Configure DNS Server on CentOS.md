# How to Setup DNS Server on CentOS
## 1. Install BIND (DNS Server Software)
Update packages:
```
sudo yum update -y
```
Install BIND and related tools:
```
sudo yum install bind bind-utils -y
```
Enable and start the service:
```
sudo systemctl enable named
sudo systemctl start named
```
Check status:
```
sudo systemctl status named
```
## 2. Configure BIND Primary Zone
Edit the main configuration file:
```
sudo nano /etc/named.conf
```
Change listen-on and allow-query so your server can answer DNS queries:
```

options {
    listen-on port 53 { any; };
    listen-on-v6 port 53 { any; };
    allow-query     { any; };

    recursion yes;
};
```
Save and exit.
##  3. Define Your DNS Zone
```
sudo nano /etc/named.rfc1912.zones
```
Add your domain zone (example: example.com):
```

zone "example.com" IN {
    type master;
    file "example.com.zone";
    allow-update { none; };
};
```
## 4. Create Zone File
Create the zone file in /var/named/:
```
sudo nano /var/named/example.com.zone
```
Paste the template below (modify domain & IP):
```
$TTL 86400
@   IN  SOA ns1.example.com. admin.example.com. (
        2024020101  ; Serial
        3600        ; Refresh
        1800        ; Retry
        604800      ; Expire
        86400 )     ; Minimum TTL

; Name servers
@       IN  NS      ns1.example.com.

; A records
ns1     IN  A       192.168.1.10
@       IN  A       192.168.1.10
www     IN  A       192.168.1.10
```
Set correct permissions:
```

sudo chown root:named /var/named/example.com.zone
sudo chmod 640 /var/named/example.com.zone
```
## 5. (Optional) Create Reverse DNS Zone
Edit configuration:
```
sudo nano /etc/named.rfc1912.zones
```
Add reverse zone (example for 192.168.1.x):
```

zone "1.168.192.in-addr.arpa" IN {
    type master;
    file "192.168.1.rev";
    allow-update { none; };
};
```
Create reverse zone file:
```
sudo nano /var/named/192.168.1.rev
```
Example:
```
$TTL 86400
@   IN  SOA ns1.example.com. admin.example.com. (
        2024020101
        3600
        1800
        604800
        86400 )

@     IN  NS    ns1.example.com.
10    IN  PTR   example.com.
```
## 6. Check Configuration for Errors
Check named.conf:
```
sudo named-checkconf
```
Check your zone files:
```

sudo named-checkzone example.com /var/named/example.com.zone
sudo named-checkzone 1.168.192.in-addr.arpa /var/named/192.168.1.rev
```
If both say OK, continue.
## 7. Restart BIND
```
sudo systemctl restart named
```
Allow DNS through firewall:
```

sudo firewall-cmd --add-service=dns --permanent
sudo firewall-cmd --reload
```
## 8. Test DNS
Test A record:
```
dig @192.168.1.10 example.com
```
Test www:
```
dig @192.168.1.10 www.example.com
```
Test reverse lookup:
```
dig @192.168.1.10 -x 192.168.1.10
```
If you see ANSWER SECTION → DNS is working.
