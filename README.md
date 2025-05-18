# Debian IPTables Setup
1. Create and edit /etc/iptables.conf (for a docker host, copy contents of docker-iptables.conf, for a non-docker host, copy contents of noo-docker-iptables.conf; adjust accordingly)
```
touch /etc/iptables.conf
nano /etc/iptables.conf
```
2. Install IPTables and configure service
```
apt update
apt install iptables -y
iptables-restore -n /etc/iptables.conf
nano /etc/systemd/system/iptables.service
```
```
[Unit]
Description=Restore iptables firewall rules
Before=network-pre.target

[Service]
Type=oneshot
ExecStart=/sbin/iptables-restore -n /etc/iptables.conf

[Install]
WantedBy=multi-user.target
```
2. Enable service on boot
```
systemctl enable --now iptables
```
3. Restart service
```
systemctl restart iptables
```
