# Day 04 – Linux Practice: Processes and Services

## practice Linux fundamentals with real commands.

Running basic commands and capturing output :

- Check running processes

###  ps
```
output

![alt text](image-1.png)

```

### ps aux
```
output

![alt text](image.png)
    
```

### uptime
```
output

![alt text](image-2.png)
    
```

### top
```
output

![alt text](image-5.png)
    
```

### ls -la
```
output

![alt text](image-6.png)
    
```

### ip a
```
output

![alt text](image-7.png)
    
```

---

## Inspect one systemd service

###  systemctl status nginx
```
output

![alt text](image-3.png)
    
```

### journalctl -u nginx
```
output

![alt text](image-4.png)
    
```
---

### Log checks
---

### cat

```
output

![alt text](image-8.png)

```

### tail -f <log_filename>
```
output 

![alt text](image-9.png)
    
```

### grep "string to find"
```
output 

![alt text](image-9.png)
    
```

## Capture a small troubleshooting flow for cron

```bash

# 1. Check cron service
systemctl status cron 

# 2. Verify cron jobs
crontab -l

# 3. Use full paths
which df
/bin/df -h

# 4. Redirect output & errors
* * * * * /path/script.sh >> /tmp/cron.log 2>&1

# 5. Check cron logs
grep CRON /var/log/syslog    # Ubuntu

# 6. Check script permissions
ls -l script.sh
chmod +x script.sh

# 7. Test script manually
bash script.sh

```

---