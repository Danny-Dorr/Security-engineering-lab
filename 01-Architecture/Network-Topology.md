# Network Topology

## Logical topology

```text
Apartment Network
       |
       v
FortiGate 61E
       |
       | 802.1Q trunk
       v
MokerLink 2.5GbE managed switch
   |       |       |       |
   v       v       v       v
 PVE-01  PVE-02  PVE-03   AP
   |       |       |
   +-------+-------+
           |
        Synology
```

## Firewall

The FortiGate provides:

- WAN connectivity
- NAT
- Inter-VLAN routing
- Firewall policy
- DHCP where appropriate
- VPN functionality
- Traffic/security logging

## Switch

The MokerLink provides:

- VLAN switching
- Access ports
- Trunking
- Layer-2 connectivity

It should not be treated as the primary inter-VLAN security boundary.

## Proxmox

Three NUC8i7BEH systems form the virtualization layer.

Planned workload distribution:

- PVE-01: AD/DC, DNS/DHCP, AdGuard
- PVE-02: Wazuh, Security Onion, Nessus
- PVE-03: additional servers, vulnerable systems, test environments

Workloads can move between nodes as the lab evolves.

## Wireless

Planned SSIDs:

| SSID | VLAN | Purpose |
|---|---:|---|
| Home-Trusted | 30 | Authorized devices |
| Home-IoT | 60 | IoT |
| Home-Guest | 70 | Guest access |

Guest client isolation should be enabled where supported.

## Troubleshooting layers

```text
Physical
  -> cables / patch panel / switch ports

Layer 2
  -> VLANs / trunks / MAC learning

Layer 3
  -> gateway / routing / firewall

Application
  -> VM / service / host

Security
  -> policy / logs / detection / response
```
