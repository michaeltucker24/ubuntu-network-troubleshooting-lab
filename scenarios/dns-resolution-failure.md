# Scenario 002: DNS Resolution Failure

## Reported Issue

A user reports that the Ubuntu server can reach IP addresses but cannot resolve domain names.

## Impact

The server may be unable to install packages, reach external APIs, download updates, or communicate with services by hostname.

## Environment

- OS: Ubuntu Server
- Tools: `ping`, `dig`, `resolvectl`, `cat`, `systemctl`

## Investigation Steps

### 1. Test connectivity by IP address

```bash
ping 8.8.8.8
```

If this works, basic internet connectivity is available.

### 2. Test connectivity by domain name

```bash
ping example.com
```

If this fails, DNS resolution may be the issue.

### 3. Run a DNS lookup

```bash
dig example.com
```

### 4. Review resolver status

```bash
resolvectl status
```

### 5. Check resolver configuration

```bash
cat /etc/resolv.conf
```

### 6. Restart resolver service if needed

```bash
sudo systemctl restart systemd-resolved
```

### 7. Flush DNS cache

```bash
sudo resolvectl flush-caches
```

## Commands Used

```bash
ping 8.8.8.8
ping example.com
dig example.com
resolvectl status
cat /etc/resolv.conf
sudo systemctl restart systemd-resolved
sudo resolvectl flush-caches
```

## Root Cause

The server had working IP connectivity, but DNS lookups were failing due to incorrect or unavailable resolver configuration.

## Resolution

The DNS resolver configuration was reviewed and corrected. The resolver service was restarted, and DNS cache was flushed.

## Verification

Domain name resolution was tested again successfully.

```bash
dig example.com
ping example.com
```

## Customer-Facing Update

The DNS issue was resolved. The server had network connectivity by IP address, but name resolution was failing. Resolver settings were corrected and domain lookups were verified.

## Lessons Learned

When IP connectivity works but domain names fail, focus on DNS resolver configuration, resolver service status, and DNS lookup behavior.
