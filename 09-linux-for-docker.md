# Linux for Docker

This file focuses on **how Docker depends on Linux**,
so you understand *why things work*, not just *how to run commands*.

---

## What Docker Really Uses from Linux

Docker is not magic.
It is built on top of Linux features.

Docker depends on:
- Linux processes
- Linux filesystem
- Linux networking
- Linux permissions
- Linux resource control

If Linux works logically,
Docker works logically too.

---

## Containers Are Just Processes

A container is **not a virtual machine**.

Inside Linux:
- Containers are normal processes
- They run in isolation
- They share the same kernel

This means:
- If you understand processes, you understand containers
- If you can debug a process, you can debug a container

---

## Filesystem View: Host vs Container

Docker uses Linux filesystem heavily.

Key idea:
- Container sees its own filesystem
- Host has the real filesystem

Volumes connect the two.

Example concept:
```text
Host directory  --->  Container directory
```

Docker does not create data magically. It stores data on the host.

---

## Where Docker Stores Data on Linux

By default, Docker stores data in:
```text
/var/lib/docker
```

This includes:
- images
- containers
- volumes
- logs

That is why disk understanding from earlier chapters matters here.

---

# Volumes: Sharing Data Safely
Volumes are Linux directories mounted into containers.
Concept:
-Host directory exists
-Container uses it

This allows:
- data persistence
- backups
- inspection from host

Volumes are just Linux mounts in disguise.

---

 # Permissions & Docker

Containers run as users.
Host directories have owners.
For data to work:
- container user must have access
- host permissions must allow it

This is why Linux permission knowledge is essential for Docker.

---

# Networking: Containers Use Linux Networking

Docker creates:
- virtual networks
- bridges
- interfaces

All of these are Linux networking concepts.

If you know:
- IPs
- ports
- listening services

You already know half of Docker networking.

---

# Ports: Host and Container Relationship

Docker maps:
- container port → host port

Concept:
```text
Host:8080  --->  Container:80
```

Linux checks:
- is port free?
- is firewall allowing it?
- is service listening?

Docker does not bypass Linux rules.

---

# Processes Inside Containers

You can think of container processes like this:
- they start
- they consume CPU & memory
- they stop or crash

Linux still controls:
- scheduling
- limits
- signals

Understanding ps, top, and kill helps here.

---

# Logs: Container Logs Are Linux Logs

Docker logs come from:
- standard output
- standard error

Linux still handles:
- file writing
- disk usage
- rotation

That’s why log discipline matters even with containers. 

---

# Simple Mental Model (Remember This)

- Docker = Linux + isolation
- Container = process
- Volume = directory
- Network = Linux bridge
- Logs = Linux output

This model reduces confusion a lot.

---

# Hands-On Learning

```bash
docker info
docker ps
docker images
ls /var/lib/docker
```

# Important Linux Concepts for Docker

```bash
processes     -> containers
filesystem    -> images & volumes
permissions   -> data access
networking    -> ports & bridges
disk usage    -> images & logs
```
