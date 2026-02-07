# Basic Linux Command Line
## 1. Check for updates and upgrade the system
```
sudo apt update && sudo apt upgrade -y
```
## 2. Shutdown System
```
sudo shutdown now
```
Or
```
sudo init 0
```
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

## 3. Schedule shutdown system
To shut down after 10 minutes, use:
```
sudo shutdown +10
```
Shutdown with warning message next 10 minutes
```
sudo shutdown +10 "System going down for maintenance in 10 minutes."
```
To shut down at 11:30 PM (23:30), use the 24-hour format:
```
sudo shutdown 23:30
```
Canceling a Scheduled Shutdown
```
sudo shutdown -c
```
### 4. Reboot system
```
sudo init 6
```
Or
```
sudo reboot
```
Or
```
sudo shutdown -r now
```
### 5. File & Directory Navigation
```pwd```	Prints the current working directory path.

<img width="802" height="137" alt="image" src="https://github.com/user-attachments/assets/4154d060-7b46-4d36-b5b4-a4f2dec25799" />

```ls```	Lists files and directories in the current folder.

<img width="905" height="94" alt="image" src="https://github.com/user-attachments/assets/be886710-208c-4644-b2d3-45c382aa7a92" />

```cd```	Changes the current directory.

<img width="840" height="59" alt="image" src="https://github.com/user-attachments/assets/dacced5e-b6da-4674-aad6-58a114944dec" />

```mkdir```	Creates a new directory.

<img width="843" height="107" alt="image" src="https://github.com/user-attachments/assets/3b32f7f9-4cc1-47db-9da9-6138a5c2c485" />

```rmdir```	Removes an empty directory.

<img width="816" height="79" alt="image" src="https://github.com/user-attachments/assets/de0e6675-56a2-47e5-8edf-d4d64a4fde55" />



