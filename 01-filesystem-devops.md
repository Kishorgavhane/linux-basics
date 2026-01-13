
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


A engineer always checks `/var` first.

---

## `/usr` – Installed Software (Do Not Touch Blindly)

This is where system-installed software lives.

Common locations:
- `/usr/bin` → user commands (git, docker, python)
- `/usr/sbin` → system services (nginx, sshd)
- `/usr/lib` → libraries

Important mindset:
- `/usr` is managed by package manager (apt, yum)
- Manual changes here are dangerous
- Never edit files here unless you know exactly why

If `/usr` breaks, the system becomes unusable.

---

## `/opt` – Third-Party & Custom Applications

This directory exists for **manual installations**.

Typical use cases:
- Enterprise tools
- Custom internal applications
- Software not installed via apt

Examples:
- `/opt/sonarqube`
- `/opt/custom-monitoring`

DevOps best practice:
If you install something manually, put it in `/opt`.

It keeps the system clean and predictable.

---

## `/home` – Human Space

This is where **users live**, not services.

Contains:
- User files
- SSH keys
- Scripts
- Environment configs

Examples:
- `/home/devops/.ssh`
- `/home/devops/scripts`

Production rule:
- Services should NOT depend on `/home`
- Human users do

If a service breaks when a user logs out, it’s a bad design.

---

## `/tmp` – Short-Term Memory

This directory is for temporary files.

Key points:
- Anyone can write here
- Files may disappear on reboot
- Used by installers, scripts, CI tools

DevOps usage:
- Temporary builds
- Script outputs
- Debug experiments

Never store important data in `/tmp`.

---

## `/var/lib` – Application Reality

This directory deserves special attention.

Modern applications store their state here:
- Docker → `/var/lib/docker`
- Kubernetes → `/var/lib/kubelet`
- Databases → `/var/lib/mysql`

If `/var/lib` is deleted or corrupted:
- Containers are gone
- Databases lose data

This directory is **always backed up** in production systems.

---

## How a DevOps Engineer Debugs a Service (Real Flow)

Example: Nginx is not working.

1. Check binary exists:
```bash
which nginx
