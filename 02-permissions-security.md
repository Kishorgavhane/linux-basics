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
`ls -l`

---

Output
-rw-r--r-- 1 devops devops app.conf

Breakdown
-rw-r--r-- 1 devops devops app.conf
│ │  │  │  │      │      └── file-name
│ │  │  │  │      └───────── group
│ │  │  │  └──────────────── owner
│ │  │  └─────────────────── hard-links
│ │  └────────────────────── permissions
└─────────────────────────── file-type






