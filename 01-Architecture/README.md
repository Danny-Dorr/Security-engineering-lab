# 01 — Architecture

This directory documents the logical architecture of the home security engineering lab.

## Architecture goals

- Enterprise-style network segmentation
- Centralized firewall enforcement
- Controlled inter-VLAN communication
- Dedicated management, server, trusted, security, attack, IoT, and guest zones
- Security telemetry and evidence collection
- Reproducible infrastructure
- Controlled offensive-security testing
- Portfolio-quality documentation

## Current physical foundation

- FortiGate 61E firewall
- MokerLink managed 2.5GbE switch
- Three Intel NUC8i7BEH Proxmox hosts
- Synology NAS
- Patch panel
- Wireless AP infrastructure
- 10-inch rack

## High-level topology

```text
Apartment / ISP
      |
      v
FortiGate 61E
      |
      | 802.1Q VLAN trunk
      v
MokerLink managed switch
  |       |       |       |
  v       v       v       v
PVE-01  PVE-02  PVE-03   AP
  |       |       |
  +-------+-------+
          |
       Synology

Security zones:
VLAN 10 Management
VLAN 20 Servers
VLAN 30 Trusted
VLAN 40 Security
VLAN 50 Attack Lab
VLAN 60 IoT
VLAN 70 Guest
VLAN 80 NAS
```

## Roles

| Component | Primary role |
|---|---|
| FortiGate 61E | WAN, NAT, routing, firewall, VPN, policy logging |
| MokerLink switch | Layer-2 switching, VLANs, trunks |
| Proxmox NUCs | Virtualization |
| AP | Wireless access into selected VLANs |
| Synology | Storage/backup role |

## Security model

The FortiGate is the primary routed security boundary. Inter-VLAN traffic is denied by default and explicitly permitted only when required.

The switch provides Layer-2 segmentation. The hypervisors provide virtual infrastructure. Security tools provide endpoint and network visibility.

## Implementation status

Architecture is designed; VLANs and services are implemented progressively. Items marked planned elsewhere in this repository are not claims of current deployment.

## Build order

1. FortiGate WAN/LAN
2. Switch management
3. FortiGate-to-switch trunk
4. VLANs
5. Proxmox networking
6. AD/DNS/DHCP
7. AdGuard
8. Wazuh/Security Onion/Nessus
9. Wireless VLANs
10. Remote access
11. Security testing
12. Detection/IR documentation
