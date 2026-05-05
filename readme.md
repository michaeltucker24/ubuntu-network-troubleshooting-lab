# Ubuntu Network Troubleshooting Lab

## Overview

This repository documents a hands-on Ubuntu network troubleshooting lab focused on diagnosing connectivity issues from the Linux command line.

The lab covers IP configuration, routing, DNS resolution, SSH access, firewall rules, listening ports, service availability, and packet capture basics.

## Scenario

A user reports that they cannot connect to an Ubuntu server. The issue could involve SSH, DNS, firewall rules, incorrect IP configuration, a stopped service, or a blocked port.

## Objectives

- Verify IP configuration
- Check routing
- Test basic network connectivity
- Troubleshoot DNS resolution
- Confirm listening ports
- Check service status
- Review firewall rules
- Use packet capture for deeper troubleshooting
- Document the root cause and resolution

## Environment

- OS: Ubuntu Server
- Platform: Local VM / Cloud VM
- Tools: `ip`, `ping`, `traceroute`, `dig`, `resolvectl`, `ss`, `curl`, `nc`, `ufw`, `tcpdump`, `systemctl`, `journalctl`

## Skills Demonstrated

- Linux network troubleshooting
- SSH diagnostics
- DNS troubleshooting
- Firewall validation
- Port and service checks
- Packet capture basics
- Root cause analysis
- Technical documentation
- Customer-facing technical updates

## Scenario Index

| Scenario | Issue | Key Tools | Link |
|---|---|---|---|
| Scenario 001 | SSH connection timeout | `ssh`, `ss`, `ufw`, `systemctl`, `journalctl` | [View Scenario](scenarios/ssh-connection-timeout.md) |
| Scenario 002 | DNS resolution failure | `ping`, `dig`, `resolvectl`, `/etc/resolv.conf` | [View Scenario](scenarios/dns-resolution-failure.md) |
| Scenario 003 | Firewall blocking web traffic | `ufw`, `ss`, `curl`, `tcpdump` | [View Scenario](scenarios/firewall-blocking-web-traffic.md) |

## Investigation Workflow

### 1. Check IP configuration

```bash
ip addr
ip route
```

### 2. Test network connectivity

```bash
ping 8.8.8.8
ping example.com
```

### 3. Test DNS resolution

```bash
dig example.com
resolvectl status
```

### 4. Check listening ports

```bash
ss -tuln
```

### 5. Test service access

```bash
curl -v http://localhost
nc -zv server-ip 22
```

### 6. Review firewall rules

```bash
sudo ufw status verbose
```

### 7. Check service status

```bash
sudo systemctl status ssh
sudo journalctl -u ssh
```

### 8. Capture traffic

```bash
sudo tcpdump -i any port 22
```

## Common Root Causes

- SSH service not running
- Firewall blocking required port
- DNS server misconfiguration
- Service not listening on expected interface
- Incorrect IP address
- Incorrect cloud network security rule
- Routing issue
- Application service running locally but blocked externally

## Verification Checklist

Before closing a network troubleshooting ticket, verify:

- Correct IP address is assigned
- Route is present
- DNS resolution works
- Required service is running
- Service is listening on the expected port
- Firewall allows required traffic
- Local and external connection tests succeed
- Findings and resolution are documented clearly

## Customer-Facing Update Example

The connectivity issue was resolved. The server was online, but network access was blocked by a firewall rule. The required access rule was corrected and connectivity was verified.

## Lessons Learned

This lab reinforced a layered approach to network troubleshooting: IP configuration, routing, DNS, firewall, service status, port validation, and application-level testing.

## Portfolio Note

This project is part of my Linux Support Engineer portfolio. It demonstrates practical troubleshooting, documentation, and systems administration skills relevant to Ubuntu/Linux support roles.
