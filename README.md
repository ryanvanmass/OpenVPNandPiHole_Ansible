# Description
Easily Deploy a Openvpn Network with DNS level ad blocking via PiHole

# UFW Configuration
| Port | State           | Purpose |
|------|-----------------|---------|
| 22   | Limited         | SSH     |
| 2049 | Allowed on Eth1 | NFS     |
| 1194 | Allowed         | OpenVPN |


# Setup
## Ansible Playbook
```
    apt install ansible
    ansible-pull -U https://github.com/ryananmass/OpenVPNandPiHole_Ansible Deploy.yml
```

## OpenVPN
Guide: https://docs.pi-hole.net/guides/vpn/installation/
1. Execute Setup Script
```
sh /root/openvpn-install/openvpn-install.sh
```
2. Select UDP
3. Use Port 1194
4. select Google for DNS
5. name the first client the hostname of the server

### Pihole
1. Run the Install Script
```
sh /root/PiHole/automated\ install/basic-install.sh
```
2. select tun0
3. Select Google
4. accept defualt
5. accept Defualt
6. set the IP address as 10.8.0.1 and the gateway to be the public ip of the server
7. Accept Defaults
8. Accept Defaults
9. Accept Defaults
10. Accept Defaults
11. edit `/etc/openvpn/server/server.conf`to reflect the following
```
push "dhcp-option DNS 10.8.0.1"
#push "dhcp-option DNS 8.8.8.8"
```
12. Login to web portal and change password

### FileSync
Is a pre-configured Service that can be used as a template for syncing content between a NAS on your Local Network and your cloud deployment