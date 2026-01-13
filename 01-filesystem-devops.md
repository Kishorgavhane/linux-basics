
## Why Filesystem Knowledge Is Critical in DevOps

In real production incidents:
- Services fail because configs are wrong
- Systems go down because disks get full
- Applications break because of permission issues

All of this comes back to **filesystem understanding**.

DevOps is not about memorizing commands.
It is about knowing **where things live and why**.

---

## Root Filesystem (`/`) – The Starting Point

Linux does not have drives like C:, D:  
Everything starts from a single root:


Every file, directory, device, and process is attached somewhere under `/`.

When a system boots, the kernel mounts `/` first.
If root filesystem is corrupted, the system does not boot.

That is why `/` is sacred.

---

## `/etc` – Configuration Brain of the System

This is the **most important directory for DevOps**.

`/etc` contains:
- System configuration
- Service configuration
- Security-related settings

Examples you will touch daily:
- `/etc/nginx/nginx.conf`
- `/etc/ssh/sshd_config`
- `/etc/systemd/system/`
- `/etc/fstab`

Golden rule:
- `/etc` contains **only text files**
- No binaries
- No logs

In production, when something breaks, the first question is:
> “Did someone change something in `/etc`?”

---

## `/var` – Where Problems Are Recorded

`/var` stands for **variable data**.
Its size changes constantly while the system is running.

This directory is responsible for:
- Logs
- Cache
- Runtime data
- Application state

Important DevOps paths:
- `/var/log/` → logs (your best friend during incidents)
- `/var/lib/` → application data (Docker, databases)
- `/var/cache/` → cached data
- `/var/tmp/` → temporary files (survive reboot)

Most production outages related to disk space happen because:

