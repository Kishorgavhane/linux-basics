# Users, sudo & SSH

This document is written from real server usage.
Most production issues are not caused by Linux itself,
they are caused by **humans using Linux incorrectly**.

Users, sudo, and SSH define **who is allowed to do what**.
If this part is weak, security is weak.

---

## Why Engineers Care About Users

In real environments:
- Nobody works as root all the time
- Every action should be traceable to a user
- Access should be minimal, not unlimited

If everyone has root access:
- Mistakes happen
- No accountability
- Security audits fail

---

## Linux Users – The Basics You Must Respect

Every process in Linux runs as **some user**.

Check your current user:
```bash
whoami
```

Check user details:
```bash
id
```

This tells you:
- username
- user ID
- group memberships

 ## Common Human Mistake

 ```bash
sudo su
```

Result:
- Files owned by root
- Apps break for normal users
- CI/CD permission issues
- SSH access problems later

Rule:
- Use root only when required, not by habit.

## Creating a User (Correct Way)

Create a DevOps user:
```bash
sudo useradd -m devops
```

Set password
```bash
sudo passwd devops
```

Check home directory:
```bash
ls /home
```

 ## Groups – Silent Permission Controller

 Check groups of a user:
 ```bash
groups devops
```

Add user to a group:
```bash
sudo usermod -aG docker devops
```
 ## sudo – Controlled Power

Check sudo access:
 ```bash
sudo -l

```
Add user to sudo group:
```bash
sudo usermod -aG sudo devops

```
After this:
```bash
su - devops
sudo whoami
```
Output:
- `root`

 ## Common Mistake #2: Giving full sudo blindly ❌

Bad practice:
- Giving sudo to everyone
- No command restriction
- No review`

Better mindset:
- Give sudo only to required users
- Remove access when role changes
- Security is about control, not convenience

 ## SSH – Remote Access Backbone

 Basic connection:
 ```bash
ssh user@server-ip
```

SSH Keys – MUST KNOW
Generate key on local machine:
```bash
ssh-keygen
```

Public key:
```bash
~/.ssh/id_rsa.pub
```

Private key:
```bash
~/.ssh/id_rsa
```
 ## Copy SSH Key to Server (Right Way)

 ```bash
ssh-copy-id devops@server-ip
```
SSH Config File (Productivity Booster)
- ~/.ssh/config

Example:
- Host prod-server
- HostName 10.0.0.5
- User devops

Now connect using:
```bash
ssh prod-server
```

 ## Common Mistake: Editing SSH config as root ❌

SSH config is user-specific.
Do not edit root SSH config unless required.

 ## Hands-On Practice
 ```bash
whoami
id
groups
sudo -l
ls -ld /home/$USER
```

 ## Important Commands
 ```bash
whoami          # current-user
id              # user-details
groups          # group-list
useradd         # create-user
usermod         # modify-user
passwd          # set-password
sudo -l         # sudo-check
ssh             # remote-login
ssh-keygen      # key-create
ssh-copy-id     # key-upload
```

