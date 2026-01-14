# Linux Permissions & Security for DevOps (Real-World)

This file exists because **permissions break production more often than code**.
If an application suddenly stops working after deployment, permissions are usually the reason.

---

## Why Permissions Matter in DevOps

In real incidents:
- Docker containers fail to write volumes
- CI/CD pipelines break after `git pull`
- SSH login suddenly stops
- Nginx shows 403 errors

All of these come back to **wrong permissions or ownership**.

---

## Understanding Permission Structure (Core Concept)

Every file and directory has:
- **Owner**
- **Group**
- **Others**

And three permissions:
- `r` → read
- `w` → write
- `x` → execute

When you run the command:

```bash
ls -l

```

- **output**  → -rw-r--r-- 1 devops devops app.conf

- **Breakdown**
```bash 
  -rw-r--r-- 1 devops devops app.conf
│ │  │  │  │      │      └── file-name
│ │  │  │  │      └───────── group
│ │  │  │  └──────────────── owner
│ │  │  └─────────────────── hard-links
│ │  └────────────────────── permissions
└─────────────────────────── file-type

```

File Permissions
- `r` → read file content
- `w` → modify file
- `x` → execute file

Directory Permissions

- `r` → list files
- `w` → create/delete files
- `x` → enter directory

Numeric Permission Model
| Number | Meaning |
| ------ | ------- |
| 4      | read    |
| 2      | write   |
| 1      | execute |

Add them:
- `7` → rwx
- `6` → rw-
- `5` → r-x
- `4` → r--
  
Examples you must remember:
- `755` → executable apps
- `644` → config files
- `600` → private keys

chmod – Changing Permissions

```bash
chmod 644 app.conf
chmod 755 script.sh

```

Rules:
- `Config files` → never executable
- `Scripts` → executable only when required
- `777` → almost always wrong

chown – Ownership

Check owner:

```bash
ls -l app.log

```
Change owner:

```bash
sudo chown devops:devops app.log

```

 ## SSH Security
 Private keys
 Correct:
 ```bash
chmod 600 ~/.ssh/id_rsa

```

Hands-On Practice
```bash
cd ~
mkdir perm-test
cd perm-test
touch app.conf script.sh
chmod 644 app.conf
chmod 755 script.sh
ls -l

```

Important Permission Commands
```bash
ls -l            # permissions
chmod 644 file   # config-safe
chmod 755 file   # executable
chmod 600 key    # private
chown user:user file  # ownership
id               # user-info
whoami           # current-user

```


