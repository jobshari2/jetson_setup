# Jetson Nano / Ubuntu Linux Command Reference

This document contains commonly used Linux and Ubuntu commands for running a Jetson Nano in headless console mode.

---

# Linux Command Reference Table

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `pwd` | Show current directory | `pwd` | Prints working directory |
| `ls` | List files/directories | `ls` | Basic directory listing |
| `ls -l` | Detailed directory listing | `ls -l` | Shows permissions, owner, size |
| `ls -a` | Show hidden files | `ls -a` | Includes dot files |
| `cd` | Change directory | `cd /home/jetson` | Navigate folders |
| `cd ..` | Go one level up | `cd ..` | Parent directory |
| `mkdir` | Create directory | `mkdir projects` | Creates folder |
| `rmdir` | Remove empty directory | `rmdir oldfolder` | Empty folders only |
| `rm` | Remove file | `rm file.txt` | Deletes file |
| `rm -r` | Remove directory recursively | `rm -r myfolder` | Deletes folder and contents |
| `cp` | Copy files | `cp a.txt b.txt` | Duplicate file |
| `cp -r` | Copy directories | `cp -r src backup` | Recursive copy |
| `mv` | Move or rename files | `mv old.txt new.txt` | Rename/move |
| `touch` | Create empty file | `touch test.txt` | New file |
| `cat` | Display file content | `cat notes.txt` | Print file |
| `nano` | Simple text editor | `nano config.txt` | Beginner friendly |
| `vim` | Advanced text editor | `vim script.py` | Powerful editor |
| `clear` | Clear terminal screen | `clear` | Clean terminal |
| `history` | Show command history | `history` | Useful for recalling commands |
| `man` | Show command manual | `man ls` | Documentation |
| `echo` | Print text | `echo hello` | Output text |
| `whoami` | Show current user | `whoami` | Current username |
| `hostname` | Show system hostname | `hostname` | Device name |
| `hostname -I` | Show IP address | `hostname -I` | Local IP |
| `uname -a` | System information | `uname -a` | Kernel/system details |
| `df -h` | Disk usage | `df -h` | Human-readable sizes |
| `du -sh` | Folder size | `du -sh myfolder` | Folder disk usage |
| `free -h` | Memory usage | `free -h` | RAM and swap |
| `top` | Real-time processes | `top` | System monitor |
| `htop` | Interactive process monitor | `htop` | Better version of top |
| `ps aux` | Show running processes | `ps aux` | Process list |
| `kill` | Stop process by PID | `kill 1234` | Graceful stop |
| `kill -9` | Force kill process | `kill -9 1234` | Force terminate |
| `reboot` | Restart system | `sudo reboot` | Requires sudo |
| `shutdown now` | Shut down system | `sudo shutdown now` | Immediate shutdown |
| `uptime` | Show system uptime | `uptime` | Load average too |
| `date` | Show current date/time | `date` | System clock |
| `cal` | Display calendar | `cal` | Terminal calendar |

---

# File Permission Commands

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `chmod` | Change file permissions | `chmod +x script.sh` | Make executable |
| `chmod 755` | Numeric permissions | `chmod 755 app.sh` | rwxr-xr-x |
| `chown` | Change ownership | `sudo chown user:file file.txt` | Owner/group |
| `sudo` | Run as administrator | `sudo apt update` | Root privileges |

---

# Networking Commands

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `ping` | Test connectivity | `ping google.com` | Network test |
| `ifconfig` | Show network interfaces | `ifconfig` | Requires net-tools |
| `ip addr` | Show interfaces/IPs | `ip addr` | Modern replacement |
| `netstat -tulnp` | Open ports/services | `sudo netstat -tulnp` | Network diagnostics |
| `ss -tulnp` | Socket statistics | `sudo ss -tulnp` | Faster than netstat |
| `wget` | Download files | `wget https://example.com/file.zip` | CLI downloader |
| `curl` | Transfer data | `curl ifconfig.me` | HTTP requests |
| `scp` | Secure file copy | `scp file.txt user@ip:/home/user/` | SSH copy |
| `ssh` | Remote login | `ssh user@192.168.1.45` | Secure shell |

---

# Package Management (APT)

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `apt update` | Update package lists | `sudo apt update` | Refresh repo metadata |
| `apt upgrade` | Upgrade packages | `sudo apt upgrade -y` | Install updates |
| `apt install` | Install package | `sudo apt install vim` | Install software |
| `apt remove` | Remove package | `sudo apt remove vim` | Keep configs |
| `apt purge` | Remove package/configs | `sudo apt purge vim` | Full removal |
| `apt autoremove` | Remove unused packages | `sudo apt autoremove` | Cleanup |
| `apt search` | Search package | `apt search docker` | Find software |
| `dpkg -l` | List installed packages | `dpkg -l` | Installed apps |

---

# SSH Commands

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `systemctl enable ssh` | Start SSH at boot | `sudo systemctl enable ssh` | Persistent SSH |
| `systemctl start ssh` | Start SSH service | `sudo systemctl start ssh` | Immediate start |
| `systemctl stop ssh` | Stop SSH service | `sudo systemctl stop ssh` | Disable temporarily |
| `systemctl status ssh` | Check SSH status | `sudo systemctl status ssh` | Verify running |
| `ssh-keygen` | Generate SSH keys | `ssh-keygen -t rsa` | Passwordless login |
| `ssh-copy-id` | Copy SSH key | `ssh-copy-id user@host` | Easier login |

---

# Systemctl / Services

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `systemctl status` | Service status | `systemctl status ssh` | Check service |
| `systemctl start` | Start service | `sudo systemctl start docker` | Start now |
| `systemctl stop` | Stop service | `sudo systemctl stop docker` | Stop now |
| `systemctl restart` | Restart service | `sudo systemctl restart ssh` | Reload service |
| `systemctl enable` | Enable at boot | `sudo systemctl enable docker` | Autostart |
| `systemctl disable` | Disable at boot | `sudo systemctl disable bluetooth` | Disable service |
| `systemctl get-default` | Current boot target | `systemctl get-default` | GUI/console |
| `systemctl set-default multi-user.target` | Console boot mode | `sudo systemctl set-default multi-user.target` | Disable GUI |
| `systemctl set-default graphical.target` | GUI boot mode | `sudo systemctl set-default graphical.target` | Enable GUI |

---

# Disk and Storage Commands

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `lsblk` | List storage devices | `lsblk` | Drives/partitions |
| `mount` | Mount filesystem | `sudo mount /dev/sdb1 /mnt` | Attach drive |
| `umount` | Unmount filesystem | `sudo umount /mnt` | Detach drive |
| `fdisk -l` | Disk partition info | `sudo fdisk -l` | Storage details |
| `mkfs.ext4` | Format partition | `sudo mkfs.ext4 /dev/sdb1` | WARNING: erases data |

---

# User Management

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `adduser` | Create user | `sudo adduser devuser` | New account |
| `passwd` | Change password | `passwd` | Current user |
| `passwd username` | Change user password | `sudo passwd jetson` | Admin required |
| `su` | Switch user | `su username` | Change account |
| `groups` | Show groups | `groups` | User permissions |

---

# Process Monitoring

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `jobs` | Show background jobs | `jobs` | Current shell jobs |
| `bg` | Resume in background | `bg` | Background execution |
| `fg` | Bring to foreground | `fg` | Foreground process |
| `nohup` | Run after logout | `nohup python app.py &` | Persistent execution |

---

# Compression Commands

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `tar -czf` | Create tar.gz archive | `tar -czf backup.tar.gz folder` | Compress |
| `tar -xzf` | Extract tar.gz archive | `tar -xzf backup.tar.gz` | Extract |
| `zip` | Create zip file | `zip archive.zip file.txt` | ZIP archive |
| `unzip` | Extract zip | `unzip archive.zip` | Extract ZIP |

---

# Useful Jetson Nano Commands

| Command | Purpose | Example | Notes |
|---|---|---|---|
| `tegrastats` | Show Jetson stats | `tegrastats` | CPU/GPU/RAM monitoring |
| `jetson_clocks` | Max performance mode | `sudo jetson_clocks` | Full speed |
| `nvpmodel -q` | Check power mode | `sudo nvpmodel -q` | Current mode |
| `nvpmodel -m 0` | Max power mode | `sudo nvpmodel -m 0` | Performance mode |
| `nvcc --version` | CUDA version | `nvcc --version` | CUDA toolkit |
| `docker ps` | Running containers | `docker ps` | Docker containers |
| `docker images` | Docker images | `docker images` | Installed images |

---

# Recommended Packages for Headless Jetson Nano

| Package | Install Command | Purpose |
|---|---|---|
| OpenSSH Server | `sudo apt install openssh-server -y` | Remote SSH |
| tmux | `sudo apt install tmux -y` | Persistent terminal |
| htop | `sudo apt install htop -y` | Better process monitor |
| vim | `sudo apt install vim -y` | Text editor |
| net-tools | `sudo apt install net-tools -y` | ifconfig/netstat |
| curl | `sudo apt install curl -y` | HTTP requests |
| git | `sudo apt install git -y` | Version control |
| docker.io | `sudo apt install docker.io -y` | Containers |

---

# Minimal Headless Setup Commands

```bash
sudo systemctl set-default multi-user.target
sudo apt update
sudo apt install openssh-server tmux htop vim net-tools -y
sudo systemctl enable ssh
sudo reboot
```

---

# Useful Tips

## Check RAM usage

```bash
free -h
```

## Check CPU usage

```bash
htop
```

## Find large folders

```bash
du -sh *
```

## Check open ports

```bash
sudo ss -tulnp
```

## Reboot remotely

```bash
sudo reboot
```

---

# Final Notes

This command reference is useful for:

- Headless Jetson Nano setups
- Ubuntu server administration
- Embedded Linux development
- Robotics and AI projects
- Docker deployments
- Remote SSH workflows

Keep this file as a quick-reference guide while working on Jetson Nano or Ubuntu systems.
