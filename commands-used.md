# Commands Used

This file lists the primary commands used throughout the Ubuntu Network Troubleshooting Lab.

## Check IP configuration

```bash
ip addr
ip route
```

## Test connectivity

```bash
ping 8.8.8.8
ping example.com
```

## Trace route path

```bash
traceroute example.com
```

## Test DNS resolution

```bash
dig example.com
resolvectl status
cat /etc/resolv.conf
```

## Check listening ports

```bash
ss -tuln
sudo ss -tulnp
```

## Test service access

```bash
curl -v http://localhost
curl -I http://server-ip
nc -zv server-ip 22
nc -zv server-ip 80
```

## Check firewall rules

```bash
sudo ufw status verbose
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw reload
```

## Check service status

```bash
sudo systemctl status ssh
sudo journalctl -u ssh
sudo systemctl status nginx
sudo journalctl -u nginx
```

## Capture traffic

```bash
sudo tcpdump -i any port 22
sudo tcpdump -i any port 80
sudo tcpdump -i any host server-ip
```
