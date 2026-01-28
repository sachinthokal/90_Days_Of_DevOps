# Day 03 – Linux cheat sheet of commands :

- Process management

```bash
ps            # Show running processes
top           # Real-time process monitoring
htop          # Interactive process viewer
atop          # Advanced system & process monitor
uptime        # System running time & load average
kill          # Send signal to a process
kill -9 <PID> # Force kill process by PID
pkill         # Kill process using name/pattern
bg            # Resume stopped job in background
fg            # Bring job to foreground
jobs          # List background jobs
nice          # Start process with priority
renice        # Change priority of running process
watch         # Run command repeatedly
strace        # Trace system calls of a process
lsof          # List open files by process

```
- File system

```bash
ls          # List files and directories
pwd         # Show current directory
cd          # Change directory
df -h       # Disk usage of file systems
du -sh *    # Directory/file size
mount       # Show mounted file systems
umount      # Unmount file system
lsblk       # List block devices
blkid       # Show block device UUIDs
find        # Search files/directories
stat        # File detailed metadata
chmod       # Change file permissions
chown       # Change file ownership
ln          # Create hard/soft links
fsck        # File system check

```

- Networking troubleshooting
```bash
ip a        # Show IP addresses
ping        # Network connectivity test
traceroute # Network path tracing
ss -tulnp   # Check listening ports
netstat    # Network connections (legacy)
curl        # Test HTTP/HTTPS endpoints
wget        # Download / connectivity test
nslookup   # DNS lookup
hostname   # Show system hostname

```
---