To grant sudo access to a user in CentOS, the recommended method is to add the user to the wheel group using the usermod command. 
## 1.Log in as the root user
<img width="1505" height="1144" alt="image" src="https://github.com/user-attachments/assets/d62112f4-f9eb-4edb-9781-8b359977caa8" />
## 2.Add the user to the wheel group:
se the usermod command with the -aG options to append the user to the supplementary wheel group. Replace <username> with the actual username:
```
usermod -aG wheel <username>
```
logout from user root then login with your own user.
then, you should be able to use sudo command
# ✅ Done!
