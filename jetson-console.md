# Jetson Nano Headless Console-Only Setup Guide

This guide explains how to run an NVIDIA Jetson Nano in **console/headless mode only** (without desktop GUI) and access it remotely from other computers using SSH.

Running without the graphical desktop saves RAM and improves performance.

---

# 1. Disable the Graphical Desktop (GUI)

Jetson Nano uses Ubuntu-based JetPack Linux.

The desktop environment starts through `graphical.target`.

## Check current boot target

```bash
systemctl get-default
```

If it shows:

```bash
graphical.target
```

switch to console mode:

```bash
sudo systemctl set-default multi-user.target
```

Reboot:

```bash
sudo reboot
```

After reboot, the Jetson Nano will boot into text console mode only.

---

# 2. Verify GUI Is Disabled

After reboot, you should see a login prompt instead of the desktop GUI.

Check memory usage:

```bash
free -h
```

You should notice lower RAM usage.

---

# 3. Install and Enable SSH

SSH allows remote console access from another computer.

## Install SSH server

```bash
sudo apt update
sudo apt install openssh-server -y
```

## Enable SSH at boot

```bash
sudo systemctl enable ssh
```

## Start SSH immediately

```bash
sudo systemctl start ssh
```

## Verify SSH status

```bash
sudo systemctl status ssh
```

You should see:

```text
Active: active (running)
```

---

# 4. Find the Jetson Nano IP Address

Run:

```bash
hostname -I
```

Example output:

```text
192.168.1.45
```

---

# 5. Connect From Another Computer

## From Linux or macOS

```bash
ssh username@192.168.1.45
```

Example:

```bash
ssh jetson@192.168.1.45
```

---

## From Windows

### Using PowerShell

```powershell
ssh username@192.168.1.45
```

### Using PuTTY

1. Install PuTTY
2. Enter Jetson Nano IP address
3. Select SSH
4. Click Open

---

# 6. Optional: Remove GUI Packages Completely

This can free additional storage and RAM.

## Check installed desktop packages

```bash
dpkg -l | grep ubuntu-desktop
```

## Remove Ubuntu desktop packages

```bash
sudo apt purge ubuntu-desktop gdm3 -y
sudo apt autoremove -y
```

On some Jetson Nano images the display manager is `lightdm`.

Disable it:

```bash
sudo systemctl disable lightdm
```

Recommendation:

- First disable GUI only
- Verify headless setup works
- Then optionally remove GUI packages

---

# 7. Optional: Serial Console Access

Useful if networking stops working.

## Requirements

- USB-to-TTL serial adapter
- Terminal software:
  - minicom
  - PuTTY

Jetson Nano UART pins can provide low-level console access.

---

# 8. Optional Memory Optimization

List enabled services:

```bash
systemctl list-unit-files --state=enabled
```

Disable unnecessary services:

```bash
sudo systemctl disable bluetooth
sudo systemctl disable cups
sudo systemctl disable avahi-daemon
```

Only disable services you do not need.

---

# 9. Switch Back to GUI Later

## Re-enable desktop mode permanently

```bash
sudo systemctl set-default graphical.target
sudo reboot
```

## Start GUI temporarily without reboot

```bash
sudo systemctl start graphical.target
```

---

# 10. Recommended Headless Utilities

Install useful terminal tools:

```bash
sudo apt install tmux htop vim net-tools -y
```

## Recommended workflow

- Console-only boot
- SSH access
- tmux for persistent sessions
- VS Code Remote SSH
- Docker for applications

---

# 11. Optional: Connect Without Remembering IP Address

Install Avahi/mDNS:

```bash
sudo apt install avahi-daemon -y
```

Then connect using:

```bash
ssh username@jetsonnano.local
```

instead of:

```bash
ssh username@192.168.1.45
```

---

# 12. Minimal Recommended Setup

If you only want the essential commands:

```bash
sudo systemctl set-default multi-user.target
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo reboot
```

---

# 13. Verify Everything Works

After reboot:

## On Jetson Nano

You should see:

- Text login prompt
- No desktop GUI

## From another computer

SSH should work:

```bash
ssh username@jetsonnano.local
```

or

```bash
ssh username@<JETSON_IP>
```

---

# 14. Troubleshooting

## SSH connection refused

Restart SSH:

```bash
sudo systemctl restart ssh
```

Check firewall:

```bash
sudo ufw status
```

Allow SSH:

```bash
sudo ufw allow ssh
```

---

## Forgot IP address

Check router DHCP list or run:

```bash
hostname -I
```

---

## GUI still starts

Check current default target:

```bash
systemctl get-default
```

It should show:

```text
multi-user.target
```

If not:

```bash
sudo systemctl set-default multi-user.target
```

---

# 15. Final Notes

Running Jetson Nano in headless console mode is recommended for:

- AI inference servers
- Robotics
- IoT applications
- Docker deployments
- Remote development
- Memory-constrained applications

This setup reduces RAM usage and improves system responsiveness.
