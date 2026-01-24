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


