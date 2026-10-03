# VLAN Design

## VLAN plan

| VLAN | Name | Subnet | Gateway | Purpose |
|---:|---|---|---|---|
| 10 | Management | 192.168.10.0/24 | 192.168.10.1 | Infrastructure administration |
| 20 | Servers | 192.168.20.0/24 | 192.168.20.1 | Server workloads |
| 30 | Trusted | 192.168.30.0/24 | 192.168.30.1 | Authorized user devices |
| 40 | Security | 192.168.40.0/24 | 192.168.40.1 | Security tooling/monitoring |
| 50 | Attack Lab | 192.168.50.0/24 | 192.168.50.1 | Kali/vulnerable systems |
| 60 | IoT | 192.168.60.0/24 | 192.168.60.1 | IoT/low-trust devices |
| 70 | Guest | 192.168.70.0/24 | 192.168.70.1 | Guest clients |
| 80 | NAS | 192.168.80.0/24 | 192.168.80.1 | Backup Storage |

## Address convention

```text
.1        gateway
.2-.19    network infrastructure
.20-.49   core services
.50-.99   static servers
.100-.199 DHCP
.200-.239 lab/static
.240-.254 future
```

## Proposed infrastructure addresses

| Host | VLAN | Proposed IP |
|---|---:|---|
| FortiGate | 10 | 192.168.10.1 |
| MokerLink | 10 | 192.168.10.2 |
| PVE-01 | 10 | 192.168.10.11 |
| PVE-02 | 10 | 192.168.10.12 |
| PVE-03 | 10 | 192.168.10.13 |
| DC-01 | 20 | 192.168.20.10 |
| AdGuard | 20 | 192.168.20.20 |
| Wazuh | 40 | 192.168.40.10 |
| Security Onion | 40 | 192.168.40.20 |

These are design proposals until verified during implementation.

## Trunk

The FortiGate-to-switch link is intended to carry tagged VLANs 10, 20, 30, 40, 50, 60, 70, and 80 using 802.1Q.

Exact native/untagged behavior should be documented after implementation.

## Security intent

- Management: highly restricted
- Servers: restricted to required services
- Trusted: normal user access
- Security: monitoring/admin functions
- Attack: isolated and controlled
- IoT: Internet-first, internal access denied by default
- Guest: Internet only

## Validation

Test both positive and negative cases:

- Correct DHCP
- Correct gateway
- Correct DNS
- Internet access where intended
- Authorized management works
- Guest cannot reach internal VLANs
- IoT cannot reach management
- Attack VLAN cannot reach management
- Unapproved inter-VLAN ports are blocked
