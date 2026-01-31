#Configuration and Management Commands

These commands are used for setting up and modifying network interfaces, addresses, and routing tables. 

*```ip```: The primary command for showing and manipulating routing, network devices, and addresses.

```ip addr show``` or ```ip a```: Displays all network interfaces and their IP addresses, netmasks, and other details.

```ip addr add [ip_address/mask] dev [interface]```: Assigns an IP address to a specific interface.

```ip link set [interface] up or down```: Enables or disables a network interface.

```ip route show```: Displays the kernel's IP routing table.

```ifconfig```: An older command (Interface Configuration) still found on some systems for displaying and configuring network interfaces. It can set IP addresses, netmasks, and enable/disable interfaces.

```iwconfig```: Specific to wireless network interfaces, used to view or set parameters like SSID and signal strength.

```hostname```: Displays or sets the system's hostname.

```hostnamectl set-hostname [new_hostname]```: A modern command to control the system hostname with systemd.

```route```: An older command used to display or modify the IP routing table.

```nmcli```: A command-line client for NetworkManager, a dynamic network management daemon, often used on desktop and server systems to manage connections interactively. 

