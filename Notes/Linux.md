## 📘 Linux Essentials for DevOps

---

### 📁 Linux Root Directory Structure (Ubuntu)

#### `/` — **Root**

* The top-level directory of the file system. Everything starts here.

#### `/bin` — **Essential User Binaries**

* Contains basic system commands and utilities (e.g., `ls`, `cp`, `mv`).
* Needed for basic functionality and available to all users.

#### `/boot` — **Boot Files**

* Contains files required for the system to boot (e.g., kernel, GRUB).

#### `/dev` — **Device Files**

* Virtual files that represent system hardware (e.g., hard drives, USBs).

#### `/etc` — **Configuration Files**

* System-wide configuration files and startup scripts.

#### `/home` — **User Home Directories**

* Each non-root user has a personal directory here (e.g., `/home/alex`).

#### `/lib` — **Shared Libraries**

* Libraries required by binaries in `/bin` and `/sbin`.

#### `/media` — **Removable Media**

* Auto-mounted devices like USB drives and CDs appear here.

#### `/mnt` — **Temporary Mount Point**

* Used for manually mounting filesystems (e.g., extra drives or partitions).

#### `/opt` — **Optional Software**

* Used for installing third-party and additional software packages.
* Can contain different versions of apps (e.g., `/opt/myapp-v1.0`).

#### `/proc` — **Process Info (Virtual)**

* A virtual filesystem with info about running processes and kernel.

#### `/root` — **Root User's Home Directory**

* Home folder for the `root` user (not to be confused with `/`).

#### `/run` — **Runtime Data**

* Temporary data used by processes and services at runtime.
* Cleared on reboot.

#### `/sbin` — **System Binaries**

* Contains system administration commands (e.g., `reboot`, `fdisk`).
* Mostly used by the root user.

#### `/srv` — **Service Data**

* Contains data for services like web or FTP servers (e.g., `/srv/www`).

#### `/sys` — **System Info (Virtual)**

* Exposes kernel and hardware info to user space.
* Used to configure and query hardware.

#### `/tmp` — **Temporary Files**

* Used by programs to store temporary files.
* Often cleared on reboot.

#### `/usr` — **User Applications and Data**

* Contains most user commands and software.
* Subfolders:

  * `/usr/bin` – user commands
  * `/usr/lib` – libraries
  * `/usr/local` – software installed manually by the user

#### `/var` — **Variable Data**

* Stores frequently changing files like:

  * Logs (`/var/log`)
  * Cache, spool files
  * Mail and web server data

#### `/data` — *(Optional/Custom)*

* Not a default Linux folder.
* Often created manually to store application or project data.
* Used to separate data from system files.

---

### 👤 User Management

* `adduser <username>` – Adds a new user with home directory and prompts for info.
* `useradd <username>` – Adds a user, no home directory or extra prompts (script-friendly).
* `passwd <username>` – Set or change user password.
* `cat /etc/passwd` – View user account info.
* `cat /etc/shadow` – View encrypted user passwords.
* `su - <username>` – Switch to another user.
* `whoami` – Show current user.
* `groupadd <groupname>` – Create a new group.
* `cat /etc/group` – View group info.
* `usermod -aG <groupname> <username>` – Add user to a group.
* `sudo su -` – Switch to root user.

🛑 **Note**: Linux does **not** allow password recovery – only reset via `root` or `sudo`.

---

### 📂 File Management

* `ls` – List files and directories.
* `cd <dirname>` – Change directory.
* `mkdir <dirname>` – Create new directory.
* `rmdir <dirname>` – Remove empty directory.
* `touch <filename>` – Create empty file.
* `rm <filename>` – Delete file.
* `ls -ltr` – List files by modification time.
* `cat <filename>` – View file content.
* `mv <src> <dest>` – Move or rename file/folder.

---

### 🔐 File Permissions

* `chmod` – Change permissions.
* `chown` – Change ownership.
* Permissions format: `r` (read), `w` (write), `x` (execute)
* File permissions are shown as: `-rwxr-xr--`

---

### ⚙️ Process Management

* `ps` – Show running processes.
* `ps aux` – Detailed process info with CPU & memory usage.
* `ps -ef` – Full-format listing.
* `kill <PID>` – Terminate process.
* `kill -STOP <PID>` – Pause process.
* `kill -CONT <PID>` – Resume process.
* `renice` – Change process priority.
* `systemctl start <service>` – Start a system service.
* `systemctl stop <service>` – Stop a service.

---

### 📊 Monitoring

* `top`, `htop` – Real-time system usage.
* `vmstat` – Memory, CPU, and IO stats.
* `free -m` – Memory usage.
* `nproc` – Number of CPU cores.
* `df -h` – Disk space usage.
* `du -sh <path>` – Directory/file size.
* **Prometheus + Grafana** – Monitoring and visualization tools.

---

### 💽 Disk Management

* `lsblk` – List block devices.
* `fdisk -l` – Partition table details.
* `mkfs -t ext4 /dev/xvdf` – Format disk with ext4.
* `mkdir /mnt/demo-vol` – Create mount point.
* `mount /dev/xvdf /mnt/demo-vol/` – Mount formatted volume.

---

### 📚 Helpful Linux Documentation for DevOps

* [Ubuntu Linux Official Docs](https://help.ubuntu.com/)
* [Linux Command Manual (tldr pages)](https://tldr.sh/)
* [The Linux Documentation Project](https://www.tldp.org/)

---

### Made with love by **Kishgi** ❤️

