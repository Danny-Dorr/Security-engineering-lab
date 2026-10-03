# IP Address Plan

Primary private addressing uses RFC1918 `192.168.0.0/16`, divided into `/24` security zones.

| VLAN | Network | Gateway |
|---:|---|---|
| 10 | 192.168.10.0/24 | 192.168.10.1 |
| 20 | 192.168.20.0/24 | 192.168.20.1 |
| 30 | 192.168.30.0/24 | 192.168.30.1 |
| 40 | 192.168.40.0/24 | 192.168.40.1 |
| 50 | 192.168.50.0/24 | 192.168.50.1 |
| 60 | 192.168.60.0/24 | 192.168.60.1 |
| 70 | 192.168.70.0/24 | 192.168.70.1 |
| 80 | 192.168.80.0/24 | 192.168.80.1 |

## Naming standard

```text
FW-01       FortiGate
SW-CORE-01  MokerLink
PVE-01      Proxmox node 1
PVE-02      Proxmox node 2
PVE-03      Proxmox node 3
DC-01       Domain Controller
ADG-01      AdGuard
WAZUH-01    Wazuh
SO-01       Security Onion
NESSUS-01   Nessus
KALI-01     Kali
NAS-01      NAS
```
