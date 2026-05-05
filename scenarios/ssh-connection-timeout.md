# Scenario 001: SSH Connection Timeout

## Reported Issue

A user reports that they cannot SSH into an Ubuntu server. The SSH client eventually times out instead of showing an authentication prompt.

## Impact

The user cannot remotely administer the server, review logs, deploy updates, or perform support tasks.

## Environment

- OS: Ubuntu Server
- Service: OpenSSH
- Tools: `ssh`, `systemctl`, `journalctl`, `ss`, `ufw`, `nc`

## Investigation Steps

### 1. Confirm server IP address

```bash
ip addr
```

### 2. Confirm SSH service status

```bash
sudo systemctl status ssh
```

### 3. Confirm SSH is listening on port 22

```bash
sudo ss -tuln | grep :22
```

### 4. Test port reachability from the client

```bash
nc -zv server-ip 22
```

### 5. Review firewall rules

```bash
sudo ufw status verbose
```

### 6. Allow OpenSSH if needed

```bash
sudo ufw allow OpenSSH
sudo ufw reload
```

### 7. Review SSH logs

```bash
sudo journalctl -u ssh
```

## Commands Used

```bash
ip addr
sudo systemctl status ssh
sudo ss -tuln | grep :22
nc -zv server-ip 22
sudo ufw status verbose
sudo ufw allow OpenSSH
sudo ufw reload
sudo journalctl -u ssh
```

## Root Cause

The SSH service was running and listening on port 22, but firewall rules were blocking inbound SSH traffic.

## Resolution

The firewall was updated to allow OpenSSH traffic.

```bash
sudo ufw allow OpenSSH
sudo ufw reload
```

## Verification

Port 22 was tested again from the client, and SSH access succeeded.

```bash
nc -zv server-ip 22
ssh username@server-ip
```

## Customer-Facing Update

The SSH timeout issue was resolved. The server was online and SSH was running, but inbound SSH traffic was blocked by the firewall. The firewall rule was updated and remote access was verified.

## Lessons Learned

SSH timeouts often indicate network or firewall issues, while immediate permission errors usually point to authentication or key problems.
