# Linux Processes & systemd

Services don’t “randomly” stop.
Servers don’t “hang by themselves”.

Something is always running, stuck, consuming resources, or crashing.
my job as a engineer is to **see it clearly and act calmly**.

---

## What Is a Process

A process is:
> a running instance of a program

Examples:
- `nginx` running → process
- `docker` running → process
- `java` app running → process

If a process stops:
- the service stops
- users complain
- alerts fire

---

## Common Mistake #1: Restarting blindly ❌

Very common reaction:
> “Service down? Restart it.”

```bash
systemctl restart nginx
```

Sometimes it works.
Sometimes it hides the real problem. observe, then act.

 ## How to See Running Processes

 Check your shell process
 ```bash
ps
```

See everything
```bash
ps aux
```

This shows:
- who is running the process
- how much CPU / memory it uses
- command used to start it

top – When System Feels Slow:
```bash
top
```

This answers:
- Why CPU is high
- Which process is eating memory
- Whether load is normal or dangerous

 ## Common Mistake: Killing random PIDs ❌

 ```bash
kill -9 1234
```

Without knowing:
- what process it is
- who started it
- what depends on it

Result:
- cascading failures
- corrupted data
- angry teammates

Killing a Process (Correct Way)
  First identify:
  ```bash
ps aux | grep nginx
```

Then stop gracefully:
```bash
kill <pid>
```

Only if needed:
```bash
kill -9 <pid>
```

Rule:
- 9 is the last option, not the first.

systemd – The Service Manager
It manages:
- services
- startup
- restarts
- logs

Checking Service Status
```bash
systemctl status nginx
```

This tells you:
- running or stopped
- last error
- restart attempts
- exit code

 ## Common Mistake: Not reading status output ❌.

 - `failed`

And immediately restart.
But the reason is already written there.
Good engineer read.
Bad ones panic.

Starting, Stopping, Restarting Services
```bash
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
```

Check again:
```bash
systemctl status nginx
```
Never assume it started successfully.

Enable vs Start
```bash
systemctl start nginx
```

👉 starts now
```bash
systemctl enable nginx
```

👉 starts on boot
Common mistake ❌
Starting a service but forgetting to enable it.
After reboot → service is gone.

Checking Service Logs
```bash
journalctl -u nginx
```

Live logs:
```bash
journalctl -u nginx -f
```

 ## Common Mistake: Looking only at app logs ❌

 People check:
 ```bash
/var/log/nginx/error.log
```

But forget:
```bash
journalctl
```

systemd logs often show:
- permission issues
- missing files
- failed dependencies

Zombie & Stuck Processes
Sometimes processes:
- don’t die
- don’t respond
- block resources

Check parent process:
```bash
ps -o ppid= -p <pid>
```

Killing the child may not help. Parent might restart it again.

Real Incident Pattern
Symptom: 
> “Server slow, app unresponsive”

Checklist:
- `uptime`
- `top`
- `ps aux`
- `systemctl status`
- `journalctl`

 ## Hands-On Practice

 ```bash
ps aux | head
top
systemctl list-units --type=service --state=running
systemctl status ssh
journalctl -u ssh
```

 ## Important Commands

 ```bash
ps aux                 # process-list
top                    # live-monitor
kill                   # stop-process
kill -9                # force-stop
systemctl status       # service-state
systemctl start        # start-service
systemctl stop         # stop-service
systemctl restart      # restart-service
systemctl enable       # boot-start
journalctl             # system-logs
journalctl -u service  # service-logs
```

