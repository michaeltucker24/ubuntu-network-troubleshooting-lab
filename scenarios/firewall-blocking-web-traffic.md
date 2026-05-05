# Scenario 003: Firewall Blocking Web Traffic

## Reported Issue

A user reports that a web application is reachable locally on the Ubuntu server but not accessible from another machine.

## Impact

Users cannot access the web application externally.

## Environment

- OS: Ubuntu Server
- Service: Nginx or Apache
- Tools: `curl`, `ss`, `ufw`, `tcpdump`, `systemctl`

## Investigation Steps

### 1. Test local web access

```bash
curl -I http://localhost
```

### 2. Confirm service is listening on port 80

```bash
sudo ss -tuln | grep :80
```

### 3. Check web service status

```bash
sudo systemctl status nginx
```

or:

```bash
sudo systemctl status apache2
```

### 4. Review firewall rules

```bash
sudo ufw status verbose
```

### 5. Allow HTTP traffic

```bash
sudo ufw allow 80/tcp
sudo ufw reload
```

### 6. Capture traffic if needed

```bash
sudo tcpdump -i any port 80
```

### 7. Test external access

```bash
curl -I http://server-ip
```

## Commands Used

```bash
curl -I http://localhost
sudo ss -tuln | grep :80
sudo systemctl status nginx
sudo systemctl status apache2
sudo ufw status verbose
sudo ufw allow 80/tcp
sudo ufw reload
sudo tcpdump -i any port 80
curl -I http://server-ip
```

## Root Cause

The web service was running locally and listening on port 80, but the firewall did not allow inbound HTTP traffic.

## Resolution

The firewall was updated to allow HTTP traffic on port 80.

```bash
sudo ufw allow 80/tcp
sudo ufw reload
```

## Verification

External access was tested successfully using `curl`.

```bash
curl -I http://server-ip
```

## Customer-Facing Update

The web access issue was resolved. The application was running locally, but inbound HTTP traffic was blocked by the firewall. The firewall rule was updated and external access was verified.

## Lessons Learned

When a service works locally but not remotely, check listening ports, firewall rules, and external network access separately.
