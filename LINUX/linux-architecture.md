# Linux Architecture

## Overview
Linux follows a layered architecture model where each layer provides specific services to the layer above it and uses services from the layer below.

## Linux System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    USER APPLICATIONS                        │
│  (Web Browsers, Text Editors, Games, Office Applications)  │
├─────────────────────────────────────────────────────────────┤
│                   SYSTEM LIBRARIES                         │
│              (glibc, pthread, OpenSSL)                     │
├─────────────────────────────────────────────────────────────┤
│                      SYSTEM CALLS                          │
│            (Interface between User & Kernel Space)         │
├─────────────────────────────────────────────────────────────┤
│                    LINUX KERNEL                            │
│  ┌─────────────┬─────────────┬─────────────┬─────────────┐  │
│  │   Process   │   Memory    │    File     │   Device    │  │
│  │ Management  │ Management  │  System     │  Drivers    │  │
│  └─────────────┴─────────────┴─────────────┴─────────────┘  │
├─────────────────────────────────────────────────────────────┤
│                      HARDWARE                              │
│     (CPU, RAM, Storage, Network, Input/Output Devices)     │
└─────────────────────────────────────────────────────────────┘
```

## Detailed Layer Analysis

### 1. Hardware Layer
**Components:**
- **CPU (Central Processing Unit)**: Executes instructions
- **RAM (Random Access Memory)**: Temporary storage for running programs
- **Storage Devices**: Hard drives, SSDs for persistent data
- **I/O Devices**: Keyboard, mouse, monitor, network cards
- **Motherboard**: Connects all components

**Key Points:**
- Linux abstracts hardware complexity through device drivers
- Hardware resources are managed by the kernel
- Direct hardware access is restricted to kernel space

### 2. Linux Kernel Layer
The kernel is the core of the operating system that manages system resources.

#### Kernel Components:

**Process Management:**
- **Process Scheduler**: Decides which process runs when
- **Process Creation/Termination**: fork(), exec(), exit() system calls
- **Inter-Process Communication (IPC)**: Pipes, signals, shared memory
- **Process States**: Running, Ready, Blocked, Zombie

**Memory Management:**
- **Virtual Memory**: Each process has its own virtual address space
- **Paging**: Memory divided into fixed-size pages
- **Swapping**: Moving inactive pages to disk
- **Memory Protection**: Prevents processes from accessing each other's memory

**File System Management:**
- **Virtual File System (VFS)**: Common interface for different file systems
- **File Operations**: Open, read, write, close, seek
- **Directory Management**: Creating, deleting, navigating directories
- **File Permissions**: Read, write, execute permissions for users/groups

**Device Drivers:**
- **Character Devices**: Sequential access (keyboards, mice)
- **Block Devices**: Random access (hard drives, SSDs)
- **Network Devices**: Network interface cards
- **Device Files**: Everything is treated as a file in /dev/

### 3. System Call Interface
Bridge between user space and kernel space.

**Common System Calls:**
- **Process Control**: fork(), exec(), wait(), exit()
- **File Operations**: open(), read(), write(), close()
- **Memory Management**: brk(), mmap(), munmap()
- **Communication**: pipe(), socket(), signal()

**System Call Mechanism:**
```
User Application
      ↓
System Call Interface
      ↓
Kernel Mode Switch
      ↓
Kernel Function Execution
      ↓
Return to User Mode
```

### 4. System Libraries Layer
Provides high-level programming interfaces.

**Key Libraries:**
- **glibc (GNU C Library)**: Standard C library functions
- **pthread**: POSIX thread library for multithreading
- **OpenSSL**: Cryptographic functions
- **X11**: Graphics and windowing system
- **Qt/GTK**: GUI toolkit libraries

### 5. User Applications Layer
Applications that end users interact with.

**Categories:**
- **System Utilities**: ls, ps, top, grep
- **Desktop Applications**: Web browsers, text editors
- **Server Applications**: Apache, Nginx, MySQL
- **Development Tools**: GCC, GDB, Make

## Kernel Architecture Types

### Monolithic Kernel (Linux)
```
┌─────────────────────────────────────┐
│           USER SPACE                │
├─────────────────────────────────────┤
│                                     │
│  ┌─────┬─────┬─────┬─────┬─────┐    │
│  │ FS  │ Net │ Mem │Proc │Dev  │    │ KERNEL
│  │     │     │ Mgmt│Mgmt │Drv  │    │ SPACE
│  └─────┴─────┴─────┴─────┴─────┘    │
│                                     │
├─────────────────────────────────────┤
│             HARDWARE                │
└─────────────────────────────────────┘
```

**Advantages:**
- Fast performance (no message passing overhead)
- Direct function calls between kernel modules
- Better resource utilization

**Disadvantages:**
- Large kernel size
- If one module crashes, entire kernel crashes
- Difficult to maintain and debug

## User Space vs Kernel Space

### User Space
- **Privilege Level**: Ring 3 (lowest privilege)
- **Memory Access**: Limited to allocated virtual memory
- **System Access**: Through system calls only
- **Protection**: Cannot directly access hardware or other processes
- **Examples**: Applications, user programs

### Kernel Space
- **Privilege Level**: Ring 0 (highest privilege)
- **Memory Access**: Can access all physical memory
- **System Access**: Direct hardware access
- **Protection**: Full system control
- **Examples**: Kernel code, device drivers

## Memory Layout
```
┌─────────────────────────────────────┐ ← 0xFFFFFFFF (4GB)
│           KERNEL SPACE              │
│  ┌─────────────────────────────┐    │
│  │    Kernel Code & Data       │    │
│  ├─────────────────────────────┤    │
│  │      Device Drivers         │    │
│  ├─────────────────────────────┤    │
│  │    Kernel Stack/Heap        │    │
│  └─────────────────────────────┘    │
├─────────────────────────────────────┤ ← 0xC0000000 (3GB)
│           USER SPACE                │
│  ┌─────────────────────────────┐    │
│  │         Stack               │    │ ← High Addresses
│  │         ↓                   │    │
│  │                             │    │
│  │         ↑                   │    │
│  │         Heap                │    │
│  ├─────────────────────────────┤    │
│  │    Uninitialized Data       │    │
│  │         (BSS)               │    │
│  ├─────────────────────────────┤    │
│  │    Initialized Data         │    │
│  ├─────────────────────────────┤    │
│  │      Program Code           │    │ ← Low Addresses
│  │        (Text)               │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘ ← 0x00000000

```

## Key Concepts

### 1. Kernel Modules
- **Loadable Kernel Modules (LKM)**: Code that can be loaded/unloaded at runtime
- **Benefits**: Reduces kernel size, adds functionality without reboot
- **Examples**: Device drivers, file systems, network protocols

### 2. Interrupts
- **Hardware Interrupts**: Signals from hardware devices
- **Software Interrupts**: System calls, exceptions
- **Interrupt Handling**: Kernel responds to interrupts immediately

### 3. Context Switching
Process of saving current process state and loading another process:
```
Process A Running → Save State → Load Process B State → Process B Running
```

### 4. Virtual Memory
- Each process sees a continuous memory space
- Physical memory may be fragmented
- Memory protection between processes
- Enables more processes than physical RAM allows

## Linux Distribution Architecture
```
┌─────────────────────────────────────┐
│        Desktop Environment          │
│     (GNOME, KDE, XFCE, etc.)       │
├─────────────────────────────────────┤
│         Display Server              │
│        (X11, Wayland)               │
├─────────────────────────────────────┤
│         Init System                 │
│    (systemd, SysV, OpenRC)         │
├─────────────────────────────────────┤
│        System Libraries             │
│         (glibc, etc.)               │
├─────────────────────────────────────┤
│         Linux Kernel                │
├─────────────────────────────────────┤
│           Hardware                  │
└─────────────────────────────────────┘
```
