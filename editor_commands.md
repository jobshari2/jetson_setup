# Linux Console Editors Reference Guide

This document explains how to use popular text editors directly from the Linux terminal/console mode on Ubuntu and Jetson Nano.

Included editors:

- nano
- vim
- vi
- emacs
- micro
- sed
- less
- cat
- tee

---

# 1. Nano Editor

Nano is beginner-friendly and easiest for console editing.

## Install Nano

```bash
sudo apt install nano -y
```

---

## Open/Create File

```bash
nano filename.txt
```

Example:

```bash
nano notes.txt
```

---

## Nano Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `CTRL + O` | Save file |
| `CTRL + X` | Exit nano |
| `CTRL + K` | Cut line |
| `CTRL + U` | Paste line |
| `CTRL + W` | Search text |
| `CTRL + G` | Help |
| `CTRL + C` | Show cursor position |
| `CTRL + _` | Go to line number |
| `ALT + U` | Undo |
| `ALT + E` | Redo |

---

## Example Workflow

```bash
nano script.py
```

Write code.

Save:

```text
CTRL + O
ENTER
```

Exit:

```text
CTRL + X
```

---

# 2. Vim Editor

Vim is powerful and commonly used by developers.

## Install Vim

```bash
sudo apt install vim -y
```

---

## Open File

```bash
vim filename.txt
```

Example:

```bash
vim app.py
```

---

# Vim Modes

| Mode | Purpose |
|---|---|
| Normal Mode | Navigation/commands |
| Insert Mode | Writing text |
| Command Mode | Save/quit/search |

---

# Enter Insert Mode

Press:

```text
i
```

Now you can type text.

---

# Exit Insert Mode

Press:

```text
ESC
```

---

# Save and Exit

| Command | Action |
|---|---|
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |

Type commands after pressing:

```text
ESC
```

then:

```text
:wq
```

---

# Vim Navigation

| Key | Action |
|---|---|
| `h` | Left |
| `j` | Down |
| `k` | Up |
| `l` | Right |
| `gg` | Go to top |
| `G` | Go to bottom |
| `/text` | Search text |
| `dd` | Delete line |
| `yy` | Copy line |
| `p` | Paste |
| `u` | Undo |

---

# Example Vim Workflow

```bash
vim config.yaml
```

Press:

```text
i
```

Write content.

Press:

```text
ESC
```

Save and quit:

```text
:wq
```

---

# 3. vi Editor

`vi` is the original Unix editor.

Usually installed by default.

---

## Open File

```bash
vi file.txt
```

Usage is mostly same as Vim.

---

# Common vi Commands

| Command | Action |
|---|---|
| `i` | Insert mode |
| `ESC` | Exit insert mode |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Force quit |

---

# 4. Emacs Editor

Emacs is highly advanced and extensible.

## Install Emacs

```bash
sudo apt install emacs -y
```

---

## Open File

```bash
emacs file.txt
```

---

# Emacs Shortcuts

| Shortcut | Action |
|---|---|
| `CTRL + X CTRL + S` | Save |
| `CTRL + X CTRL + C` | Exit |
| `CTRL + G` | Cancel command |
| `CTRL + K` | Cut line |
| `CTRL + Y` | Paste |
| `CTRL + S` | Search |
| `CTRL + A` | Start of line |
| `CTRL + E` | End of line |

---

# 5. Micro Editor

Micro is a modern beginner-friendly terminal editor.

## Install Micro

```bash
sudo apt install micro -y
```

---

## Open File

```bash
micro file.txt
```

---

# Micro Shortcuts

| Shortcut | Action |
|---|---|
| `CTRL + S` | Save |
| `CTRL + Q` | Quit |
| `CTRL + F` | Search |
| `CTRL + Z` | Undo |
| `CTRL + Y` | Redo |
| `CTRL + C` | Copy |
| `CTRL + V` | Paste |

---

# 6. less Command

`less` is for viewing files.

---

## Open File

```bash
less filename.txt
```

Example:

```bash
less log.txt
```

---

# less Navigation

| Key | Action |
|---|---|
| `Space` | Next page |
| `b` | Previous page |
| `/text` | Search |
| `n` | Next search result |
| `q` | Quit |

---

# 7. cat Command

`cat` displays file contents.

---

## Show File

```bash
cat file.txt
```

---

## Create File Quickly

```bash
cat > file.txt
```

Type content.

Press:

```text
CTRL + D
```

to save.

---

# 8. tee Command

Write output to file.

---

## Example

```bash
echo "hello" | tee file.txt
```

Append:

```bash
echo "new line" | tee -a file.txt
```

---

# 9. sed Stream Editor

Used for automated editing.

---

## Replace Text

```bash
sed -i 's/old/new/g' file.txt
```

Example:

```bash
sed -i 's/localhost/127.0.0.1/g' config.txt
```

---

## Print Specific Line

```bash
sed -n '5p' file.txt
```

---

# 10. grep Command

Search text in files.

---

## Search Text

```bash
grep "hello" file.txt
```

---

## Recursive Search

```bash
grep -r "TODO" project/
```

---

# 11. awk Command

Powerful text processing.

---

## Print Column

```bash
awk '{print $1}' file.txt
```

---

## Example

```bash
df -h | awk '{print $1}'
```

---

# 12. tail Command

View file ending.

---

## View Last 10 Lines

```bash
tail file.txt
```

---

## Live Log Monitoring

```bash
tail -f logfile.log
```

---

# 13. head Command

View file beginning.

---

## First 10 Lines

```bash
head file.txt
```

---

# 14. diff Command

Compare files.

---

## Compare Two Files

```bash
diff file1.txt file2.txt
```

---

# 15. Console Development Workflow

## Create Project

```bash
mkdir myproject
cd myproject
```

---

## Create File

```bash
nano app.py
```

or

```bash
vim app.py
```

---

## Run Python

```bash
python3 app.py
```

---

## Edit Again

```bash
vim app.py
```

---

# 16. Recommended Editors for Jetson Nano

| Editor | Best For |
|---|---|
| nano | Beginners |
| vim | Advanced users |
| micro | Easy modern editor |
| emacs | Heavy customization |
| less | Viewing logs |
| sed | Automated edits |

---

# 17. Recommended Installation

```bash
sudo apt update
sudo apt install nano vim micro emacs htop tmux -y
```

---

# 18. Best Lightweight Setup for Headless Jetson Nano

Recommended combination:

- nano or micro for editing
- vim for advanced editing
- tmux for persistent sessions
- htop for monitoring

Install:

```bash
sudo apt install nano micro vim tmux htop -y
```

---

# 19. tmux Console Session Manager

tmux keeps terminal sessions alive after SSH disconnects.

---

## Install

```bash
sudo apt install tmux -y
```

---

## Start tmux

```bash
tmux
```

---

## Detach Session

Press:

```text
CTRL + B
D
```

---

## Reattach Session

```bash
tmux attach
```

---

# 20. Final Notes

These console editors and tools are essential for:

- Headless Linux servers
- Jetson Nano development
- SSH remote administration
- Embedded Linux systems
- Robotics
- AI deployments
- Cloud/VPS systems

Learning `nano` first and `vim` later is recommended.
