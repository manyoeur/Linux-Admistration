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
### Reboot system
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
