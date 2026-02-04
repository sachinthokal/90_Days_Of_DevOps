## Mini Self-Check 

Which 3 commands save you the most time right now, and why?
```bash

# journalctl -xe → Instantly shows service errors and failures (fast RCA).

# ss -tulpn → Quickly tells which service is using which port (no guesswork).

# du -sh * | sort -h → Immediately finds what’s eating disk space.

```

How do you check if a service is healthy? List the exact 2–3 commands you’d run first.
```bash
- sudo systemctl status <service>
- sudo journalctl -u <service> -f
```
How do you safely change ownership and permissions without breaking access? Give one example command.
```bash
# First check current owner and permissions (ls -ld path) and understand which user/service needs access.

# Then apply minimum required permissions (avoid 777) and test as the target user (sudo -u user ls path) to ensure nothing breaks.

```
What will you focus on improving in the next 3 days?
```bash

# Linux troubleshooting speed (logs, CPU, memory, disk checks)

# Clear communication—explaining issues and RCA confidently to the team

# Goal: faster RCA, fewer mistakes, better confidence.
```