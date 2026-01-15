# Logs & Troubleshooting

Most people say:
> “Application is not working”

But logs always say:
> “This is exactly what went wrong”

**how quickly they reach the logs and how calmly they read them**.

---

## Why Logs Matter More Than Commands

In production:
- Commands change state
- Logs explain state

If you don’t read logs:
- You restart blindly
- You repeat mistakes
- You miss root causes

Logs are not noise.
They are **conversation between the system and you**.

---

## Where Logs Live

Most important locations:
- `/var/log/` → system & service logs
- `journalctl` → systemd logs
- Application-specific log directories

---

## Common Mistake: Restarting Before Reading Logs ❌

Typical reaction:
```bash
systemctl restart app
```

What happens:
- Error disappears temporarily
- Root cause remains
- Problem comes back later

Correct approach:
> “Read logs first. Restart later.”

System Logs
View recent system logs
```bash
journalctl
```

View logs for a specific service
```bash
journalctl -u nginx
```

Live log view.
```bash
journalctl -u nginx -f
```

This tells you:
- permission issues
- missing files
- failed dependencie
- startup errors

 ## Common Mistake: Only checking app logs ❌

People check:
```bash
/var/log/nginx/error.log
```

But forget:
```bash
journalctl
```

systemd logs often show why the app failed to start,
even before app logs are created.

Traditional Log Files (/var/log)

List log directory:
```bash
ls /var/log
```

Common files:
- `syslog`
- `auth.log`
- `kern.log`
- service-specific folders

Read safely:
```bash
less /var/log/syslog
```

Live view:
```bash
tail -f /var/log/syslog
```

 ## Common Mistake: Ignoring Timestamps ❌

Logs are time-based.

If you don’t check:
- when error happened
- what happened before it

You debug randomly.
Always observe:
- timestamp
- sequence
- repetition

Disk Full & Log Flooding

Symptom:
> “Server suddenly stopped responding”

Check:
```bash
df -h
```

Usually:
- /var is full
- logs grew uncontrollably

Find culprit:
```bash
du -sh /var/log/*
```

Logs can break a healthy system.

Filtering Logs (Think, Don’t Scroll)
Use `grep`:
```bash
grep error /var/log/syslog
grep denied /var/log/auth.log
```

This saves time and mental energy.

 ## Hands-On Practice

 ```bash
journalctl -xe
ls /var/log
tail -f /var/log/syslog
grep error /var/log/syslog
df -h
```

 ## Important Commands

 ```bash
journalctl            # system-logs
journalctl -u svc     # service-logs
journalctl -f         # live-logs
less logfile          # safe-read
tail -f logfile       # live-read
grep keyword file     # filter
df -h                 # disk-space
du -sh /var/log/*     # log-usage
```

