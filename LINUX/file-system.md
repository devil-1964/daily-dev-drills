# Linux File System Structure

## Overview
Linux follows the Filesystem Hierarchy Standard (FHS) which defines the structure and layout of directories in Unix-like operating systems.

## Root Directory Structure

```
/
├── bin/           # Essential user binaries
├── boot/          # Boot loader files
├── dev/           # Device files
├── etc/           # System configuration files
├── home/          # User home directories
├── lib/           # Essential shared libraries
├── lib64/         # 64-bit shared libraries
├── media/         # Removable media mount points
├── mnt/           # Temporary mount points
├── opt/           # Optional software packages
├── proc/          # Process and kernel information
├── root/          # Root user home directory
├── run/           # Runtime data
├── sbin/          # Essential system binaries
├── srv/           # Service data
├── sys/           # System hardware information
├── tmp/           # Temporary files
├── usr/           # User utilities and applications
├── var/           # Variable data files
└── lost+found/    # Recovered files (ext2/3/4)
```

## Detailed Directory Analysis

### /bin - Essential User Binaries
```
/bin/
├── bash           # Bash shell
├── cat            # Display file contents
├── cp             # Copy files
├── ls             # List directory contents
├── mkdir          # Create directories
├── mv             # Move/rename files
├── rm             # Remove files
├── grep           # Search text patterns
├── tar            # Archive utility
├── gzip           # Compression utility
└── pwd            # Print working directory
```

**Purpose**: Contains essential command-line utilities needed by all users
**Accessibility**: Available in single-user mode
**Mount**: Usually part of root filesystem

### /sbin - System Binaries
```
/sbin/
├── init           # System initialization
├── fsck           # File system check
├── mount          # Mount file systems
├── umount         # Unmount file systems
├── fdisk          # Disk partitioning
├── ifconfig       # Network interface configuration
├── iptables       # Firewall configuration
├── systemctl      # systemd control
├── service        # Service control
└── shutdown       # System shutdown
```

**Purpose**: Essential system administration binaries
**Access**: Primarily for root/superuser
**Path**: Usually not in regular user's PATH

### /etc - Configuration Files
```
/etc/
├── passwd         # User account information
├── shadow         # User password hashes
├── group          # Group information
├── hosts          # Host name to IP mappings
├── fstab          # File system mount table
├── crontab        # System-wide cron jobs
├── ssh/           # SSH configuration
│   ├── ssh_config
│   └── sshd_config
├── systemd/       # systemd configuration
│   └── system/
├── network/       # Network configuration
├── apt/           # Package manager config (Debian/Ubuntu)
├── yum.conf       # Package manager config (Red Hat/CentOS)
└── rc.local       # Local startup script
```

**Purpose**: System-wide configuration files
**Format**: Usually plain text files
**Permissions**: Readable by all, writable by root

### /home - User Home Directories
```
/home/
├── user1/
│   ├── .bashrc        # User shell configuration
│   ├── .profile       # User profile
│   ├── .ssh/          # User SSH keys
│   ├── Documents/     # User documents
│   ├── Downloads/     # Downloaded files
│   ├── Desktop/       # Desktop files
│   └── .local/        # User-specific data
├── user2/
└── user3/
```

**Purpose**: Personal directories for regular users
**Permissions**: Each user owns their directory
**Quota**: Can have disk space quotas applied

### /root - Root User Home
```
/root/
├── .bashrc        # Root shell configuration
├── .profile       # Root profile
├── .ssh/          # Root SSH keys
└── scripts/       # Administrative scripts
```

**Purpose**: Home directory for root user
**Location**: Separate from /home for security
**Access**: Only accessible by root

### /usr - User Utilities and Applications
```
/usr/
├── bin/           # User binaries
│   ├── python3
│   ├── gcc
│   ├── vim
│   └── firefox
├── sbin/          # Non-essential system binaries
├── lib/           # Libraries for /usr/bin and /usr/sbin
├── lib64/         # 64-bit libraries
├── include/       # Header files for C/C++
├── share/         # Shared data
│   ├── man/       # Manual pages
│   ├── doc/       # Documentation
│   └── applications/ # Desktop application files
├── local/         # Locally installed software
│   ├── bin/
│   ├── lib/
│   └── share/
└── src/           # Source code
```

**Purpose**: Secondary hierarchy for user utilities
**Shareable**: Can be shared across systems
**Read-only**: Often mounted read-only

### /var - Variable Data
```
/var/
├── log/           # System logs
│   ├── syslog
│   ├── auth.log
│   ├── kern.log
│   └── apache2/
├── cache/         # Application cache data
├── tmp/           # Temporary files (preserved across reboots)
├── spool/         # Spool directories
│   ├── mail/      # Mail queue
│   ├── cron/      # Cron jobs
│   └── cups/      # Print queue
├── lib/           # Variable state information
│   ├── mysql/     # Database data
│   └── systemd/
├── run/           # Runtime data (linked to /run)
└── www/           # Web server document root
```

**Purpose**: Variable data files that change during operation
**Growth**: Can grow significantly over time
**Monitoring**: Requires disk space monitoring

### /tmp - Temporary Files
```
/tmp/
├── temporary_file_1.txt
├── user_session_data/
├── application_temp/
└── .hidden_temp_files
```

**Purpose**: Temporary files for applications and users
**Cleanup**: Usually cleaned on reboot
**Permissions**: Sticky bit set (drwxrwxrwt)
**Security**: World-writable but protected

### /dev - Device Files
```
/dev/
├── sda            # First SATA/SCSI disk
├── sda1           # First partition on sda
├── sda2           # Second partition on sda
├── sdb            # Second SATA/SCSI disk
├── nvme0n1        # NVMe SSD
├── tty            # Current terminal
├── tty1           # First virtual terminal
├── pts/           # Pseudo terminals
│   ├── 0
│   └── 1
├── null           # Null device (discards data)
├── zero           # Zero device (provides zeros)
├── random         # Random number generator
├── urandom        # Pseudo-random generator
├── stdin          # Standard input
├── stdout         # Standard output
└── stderr         # Standard error
```

**Device Types:**
- **Block devices**: Random access (hard drives, SSDs)
- **Character devices**: Sequential access (keyboards, mice)
- **Pseudo devices**: Virtual devices for system functions

### /proc - Process Information
```
/proc/
├── 1/             # Process ID 1 (init)
│   ├── cmdline    # Command line arguments
│   ├── status     # Process status
│   ├── maps       # Memory mappings
│   └── fd/        # File descriptors
├── cpuinfo        # CPU information
├── meminfo        # Memory information
├── version        # Kernel version
├── mounts         # Mounted file systems
├── partitions     # Disk partitions
├── loadavg        # System load average
├── uptime         # System uptime
└── sys/           # Kernel parameters
    ├── kernel/
    └── net/
```

**Purpose**: Virtual filesystem providing process and kernel information
**Dynamic**: Contents generated dynamically by kernel
**Interface**: Provides interface to kernel data structures

### /sys - System Hardware Information
```
/sys/
├── block/         # Block devices
│   ├── sda/
│   └── nvme0n1/
├── bus/           # Bus information
│   ├── pci/       # PCI devices
│   ├── usb/       # USB devices
│   └── i2c/       # I2C devices
├── class/         # Device classes
│   ├── net/       # Network devices
│   ├── input/     # Input devices
│   └── block/     # Block devices
├── devices/       # Device hierarchy
├── firmware/      # Firmware information
└── kernel/        # Kernel information
```

**Purpose**: Virtual filesystem for hardware and kernel information
**sysfs**: Modern replacement for parts of /proc
**Configuration**: Can be used to configure hardware

### /boot - Boot Files
```
/boot/
├── vmlinuz-5.15.0-56-generic    # Kernel image
├── initrd.img-5.15.0-56-generic # Initial ramdisk
├── System.map-5.15.0-56-generic # Kernel symbol table
├── config-5.15.0-56-generic     # Kernel configuration
├── grub/                        # GRUB bootloader
│   ├── grub.cfg                 # GRUB configuration
│   ├── grubenv                  # GRUB environment
│   └── themes/                  # GRUB themes
└── efi/                         # UEFI boot files (if UEFI)
    └── EFI/
        └── ubuntu/
```

**Purpose**: Boot loader and kernel files
**Critical**: Essential for system boot
**Backup**: Should be backed up regularly

## File Types in Linux

### File Type Identification
```
ls -la output interpretation:
-rw-r--r--  # Regular file
drwxr-xr-x  # Directory
lrwxrwxrwx  # Symbolic link
brw-rw----  # Block device
crw-rw-rw-  # Character device
prw-r--r--  # Named pipe (FIFO)
srw-rw-rw-  # Socket
```

### File Type Legend
```
┌─────────────────────────────────────┐
│         File Type Symbols          │
├─────────────────────────────────────┤
│  -  Regular file                   │
│  d  Directory                      │
│  l  Symbolic link                  │
│  b  Block device                   │
│  c  Character device               │
│  p  Named pipe (FIFO)              │
│  s  Socket                         │
└─────────────────────────────────────┘
```

## File System Types

### Common File Systems
```
┌─────────────────────────────────────┐
│           File Systems              │
├─────────────────────────────────────┤
│  ext4      - Default Linux FS      │
│  ext3      - Previous Linux FS     │
│  ext2      - Older Linux FS        │
│  xfs       - High-performance FS   │
│  btrfs     - Modern copy-on-write  │
│  zfs       - Advanced FS features  │
│  ntfs      - Windows FS            │
│  fat32     - Compatible FS         │
│  tmpfs     - Memory-based FS       │
│  nfs       - Network FS            │
│  cifs/smb  - Windows network FS    │
└─────────────────────────────────────┘
```

### Virtual File Systems
```
┌─────────────────────────────────────┐
│        Virtual File Systems        │
├─────────────────────────────────────┤
│  /proc     - Process information   │
│  /sys      - Hardware information  │
│  /dev      - Device files          │
│  /run      - Runtime data          │
│  tmpfs     - Memory filesystem     │
│  debugfs   - Debug information     │
│  configfs  - Kernel configuration  │
│  sysfs     - System information    │
└─────────────────────────────────────┘
```

## Mount Points and File System Hierarchy

### Typical Mount Structure
```
Filesystem      Mounted on    Type
/dev/sda1       /             ext4
/dev/sda2       /home         ext4
/dev/sda3       /var          ext4
tmpfs           /tmp          tmpfs
/dev/sdb1       /mnt/backup   ext4
proc            /proc         proc
sysfs           /sys          sysfs
devtmpfs        /dev          devtmpfs
```

### Mount Points Explained
```
┌─────────────────────────────────────┐
│           Mount Strategy            │
├─────────────────────────────────────┤
│  Separate /home                     │
│  • User data preservation          │
│  • Easier OS reinstallation        │
│                                     │
│  Separate /var                      │
│  • Log file isolation              │
│  • Prevents root FS from filling   │
│                                     │
│  Separate /tmp                      │
│  • Temporary file isolation        │
│  • Security and performance        │
│                                     │
│  Separate /boot                     │
│  • Boot file protection            │
│  • UEFI requirements               │
└─────────────────────────────────────┘
```

## File Permissions and Ownership

### Permission Structure
```
-rwxr-xr--  1 user group 1024 Jan 1 12:00 filename
│││││││││
│││└┴┴┴┴─── Other permissions (r--)
││└┴┴┴───── Group permissions (r-x)
│└┴┴┴────── Owner permissions (rwx)
└─────────── File type (-)
```

### Permission Values
```
┌─────────────────────────────────────┐
│         Permission Values           │
├─────────────────────────────────────┤
│  Read (r)    = 4                   │
│  Write (w)   = 2                   │
│  Execute (x) = 1                   │
│                                     │
│  Examples:                          │
│  rwx = 4+2+1 = 7                  │
│  r-x = 4+0+1 = 5                  │
│  r-- = 4+0+0 = 4                  │
│  --- = 0+0+0 = 0                  │
│                                     │
│  Common combinations:               │
│  755 = rwxr-xr-x                   │
│  644 = rw-r--r--                   │
│  600 = rw-------                   │
│  777 = rwxrwxrwx                   │
└─────────────────────────────────────┘
```

## Hidden Files and Directories

### Dot Files
```
/home/user/
├── .bashrc         # Shell configuration
├── .vimrc          # Vim configuration
├── .gitconfig      # Git configuration
├── .ssh/           # SSH keys and config
├── .cache/         # Application cache
├── .config/        # Application configuration
├── .local/         # User-specific data
└── .mozilla/       # Mozilla Firefox data
```

**Purpose**: Configuration files and user-specific data
**Visibility**: Hidden from normal directory listings
**Access**: Accessible with ls -a or ls -la
