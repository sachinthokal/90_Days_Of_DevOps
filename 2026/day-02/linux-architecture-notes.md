# Day 02 – Linux Architecture, Processes, and systemd

### The core components of Linux (kernel, user space, init/systemd)
```
kernel :
    kernel is doing communication between hardware and software. 
    it give us shell to control the system.
    User Command →  Shell → System Call → Kernel → Hardware

User space :
    User space is where all user-level software/scripts run.

    Includes
        - Shells: bash, sh, zsh
        - Core utilities: ls, cp, ps, grep
        - System libraries: libs
        - Applications: nginx, docker, kubectl, java, python

init/systemd :
    The init system is the first process started by the kernel.
    Process ID = PID 1
    Responsible for starting and managing services

    systemd Responsibilities : 

        - Start/Stop services on system
        - Restart failed services
        - Manage dependencies
```
### How processes are created and managed ?
```
A new process is created using fork()
Then exec() replaces child with a new program

    Every process has:
        - PID (Process ID)
        - PPID (Parent Process ID)

Process Management

    - Kernel schedules processes using CPU time slicing
    - Processes can be: Paused, resumed, killed using signals
    - Common management commands: ps, top, kill, nice, htop
```
### What systemd does and why it matters ?
```
Systemd Does:

    - Starts services at boot
    - Restarts failed services automatically
    - Manages service dependencies
    - Handles logs via journald
    - Controls mounts, timers, sockets

Systemd Matters:

    - Ensures high availability of services
    - Enables auto-restart after crashes
    - Provides centralized logging
    - Critical for production stability

```
---

### Explain **process states** (running, sleeping, zombie, etc.)
```
Running (R) -
    Process is currently executing on CPU or ready to run
    Uses CPU time

    Example: a script, active request handling

Sleeping (S) -
    Waiting for an event (I/O, network, user input)
    Most processes stay here
    Can be interrupted

    Example: nginx waiting for a request

Uninterruptible Sleep (D) -
    Waiting for disk or network I/O
    Cannot be killed immediately
    Long time in D state = disk/NFS/storage issue

    Example: process stuck on disk read

Stopped (T) -
    Process is paused by a signal
    Usually via Ctrl + Z or debugger
    Can be resumed

    Example: fg

```
- List **5 commands** you would use daily
```
    1. ps - Check running processes
    2. top / htop - Monitor CPU & memory usage in real time
    3. systemctl - Manage services
    4. df - Check disk usage
    5. cp - copy files from src to dest
    6. ls - list the files/folders
    7. cat - to review file content on terminal
    8. grep - to saerch by pattern
```