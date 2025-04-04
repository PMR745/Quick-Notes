## Essential Linux Commands

### File & Directory Management

#### List files
```bash
ls -la
```

#### Change directory
```bash
cd /path/to/directory
```

#### Create directory
```bash
mkdir new_folder
```

#### Remove file
```bash
rm filename
```

#### Remove directory
```bash
rm -r folder_name
```

#### Copy file
```bash
cp source destination
```

#### Move file
```bash
mv source destination
```

#### Rename file
```bash
mv oldname newname
```

---

### File Viewing & Editing

#### View file content
```bash
cat filename
```

#### View file page by page
```bash
less filename
```

#### Edit file (nano)
```bash
nano filename
```

#### Edit file (vim)
```bash
vim filename
```

#### Search inside file
```bash
grep "pattern" filename
```

---

### File Permissions & Ownership

#### Change file permissions
```bash
chmod 755 filename
```

#### Change ownership
```bash
chown user:group filename
```

#### View file permissions
```bash
ls -l
```

---

### Process Management

#### View running processes
```bash
ps aux
```

#### Monitor system processes
```bash
top
```

#### Kill process
```bash
kill PID
```

#### Kill process by name
```bash
pkill process_name
```

#### Start background process
```bash
command &
```

#### Bring background process to foreground
```bash
fg
```

---

### Disk Usage & Storage

#### Check disk space
```bash
df -h
```

#### Check directory size
```bash
du -sh folder_name
```

#### Find large files
```bash
find / -type f -size +100M
```

---

### Networking

#### Check IP address
```bash
ip a
```

#### Check open ports
```bash
netstat -tulnp
```

#### Ping a server
```bash
ping example.com
```

#### Download a file
```bash
wget url
```

#### Transfer files (scp)
```bash
scp file user@server:/path/to/destination
```

---

### User Management

#### Add user
```bash
sudo adduser username
```

#### Delete user
```bash
sudo deluser username
```

#### Switch user
```bash
su - username
```

#### View logged-in users
```bash
who
```

---

### System Monitoring & Logs

#### System uptime
```bash
uptime
```

#### Check memory usage
```bash
free -h
```

#### View system logs
```bash
journalctl -xe
```

#### Check CPU info
```bash
lscpu
```

---

### Package Management

#### Debian/Ubuntu (apt)
```bash
sudo apt update && sudo apt upgrade
```
```bash
sudo apt install package-name
```
```bash
sudo apt remove package-name
```

#### RHEL/CentOS (yum/dnf)
```bash
sudo yum install package-name
```
```bash
sudo dnf install package-name
```

---

### Archive & Compression

#### Compress files (tar.gz)
```bash
tar -czvf archive.tar.gz folder
```

#### Extract tar.gz
```bash
tar -xzvf archive.tar.gz
```

#### Zip files
```bash
zip -r archive.zip folder
```

#### Unzip files
```bash
unzip archive.zip
```

---

### Searching & Finding Files

#### Find a file by name
```bash
find / -name filename
```

#### Find files modified in last 7 days
```bash
find /path -mtime -7
```

#### Search for a pattern in files
```bash
grep -r "pattern" /directory
```

---

### Scheduling & Automation

#### List cron jobs
```bash
crontab -l
```

#### Edit cron jobs
```bash
crontab -e
```

#### Run a job every day at midnight
```bash
0 0 * * * /path/to/script.sh
```

---

### Shutdown & Restart

#### Shutdown system
```bash
sudo shutdown -h now
```

#### Restart system
```bash
sudo reboot
```

#### Schedule shutdown
```bash
sudo shutdown -h +30
```
