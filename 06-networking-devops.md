# Networking for DevOps


It is about understanding **how data moves from one place to another**.


---

## How to Think About Networking

Whenever an application needs to work over network,
four things must be correct:

1. The system must have an IP
2. The service must be running
3. The service must be listening on a port
4. The port must be reachable

Networking problems happen when **one of these is missing**.

---

## IP Address – Identity of the System

Every server needs an IP address to communicate.

Check IP addresses:
```bash
ip a
ip addr
```

This shows:

- network interfaces
- IP addresses
- whether the interface is UP or DOWN

# Understanding Local vs Remote

- localhost → this machine
- private IP → same network
- public IP → internet-facing

Example:
```bash
curl localhost
```

# Ports – Where Services Listen

Applications do not listen on IP alone.
They listen on IP + PORT.
Check listening ports:
```bash
ss -tulnp
```

This tells:
- which port is open
- which service owns it
- which IP it is bound to

This command answers the question:
> “Is my service actually ready to receive traffic?”

# Service Status vs Network Readiness

A service can be:
- running
- but not listening

Always verify both:
```bash
systemctl status app
ss -tulnp
```

# Connectivity Testing (Basic Level)

Check reachability:
```bash
ping 8.8.8.8
```

Check HTTP service:
```bash
curl localhost:8080
```

# DNS – Name to IP Translation
Humans remember names.
Machines use IPs.

DNS connects the two.

Check DNS resolution:
```bash
nslookup google.com
```

If DNS fails:
- service may be running
- network may be fine
- but name will not resolve

# /etc/hosts – Local Override

View file:
```bash
cat /etc/hosts
```

This file maps names to IPs locally.
It is useful for:
- learning
- testing

But it should not be used as a permanent solution in production.

# Firewall – Traffic Gatekeeper

Even if:
- service is running
- port is listening

Traffic can still be blocked.
Check firewall:
```bash
sudo ufw status
```

# Hands-On Learning

```bash
ip a
ss -tulnp
curl localhost
ping 8.8.8.8
nslookup google.com
sudo ufw status
```

# Important Commands

```bash
ip a              # ip-info
ss -tulnp         # open-ports
curl              # service-test
ping              # reachability
nslookup          # dns-check
dig               # dns-detail
ufw status        # firewall-check
```

