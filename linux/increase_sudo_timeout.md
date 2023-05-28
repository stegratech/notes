https://www.techrepublic.com/article/how-to-change-the-default-sudo-timeout

# edit the sudoers file
```
sudo visudo
```

# Add this to the end
```
Defaults:username timestamp_timeout=30
```
