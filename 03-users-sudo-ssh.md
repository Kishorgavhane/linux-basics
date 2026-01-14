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

