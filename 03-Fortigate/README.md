# 03 — FortiGate 61E

This directory documents the FortiGate 61E used as the initial security gateway for the Security Engineering Lab.

## Current baseline

| Item | Value |
|---|---|
| Platform | Fortinet FortiGate 61E |
| FortiOS | 7.2.10 |
| Operating mode | NAT/Route |
| Primary role | Firewall, router, VLAN gateway, NAT |
| Upstream | Apartment Ethernet / provider-managed network |
| Downstream | MokerLink managed switch |
| Management VLAN | VLAN 10 |
| Management subnet | 192.168.10.0/24 |
| Firewall management IP | 192.168.10.1 |
| Switch management IP | 192.168.10.2 |
| DNS upstream preference | 1.1.1.1 |
| Future firewall | Protectli VP3210 / OPNsense |

## Architecture

```text
                 Apartment / Provider Network
                           │
                           │ Ethernet
                           ▼
                    ┌───────────────┐
                    │ FortiGate 61E │
                    │               │
                    │ WAN1          │
                    │ VLAN Gateway  │
                    │ Firewall/NAT  │
                    └───────┬───────┘
                            │
                       802.1Q trunk
                            │
                            ▼
                    ┌───────────────┐
                    │ MokerLink     │
                    │ Managed L2    │
                    │ Switch        │
                    └───────┬───────┘
                            │
          ┌─────────────────┼──────────────────|──────────────────┐
          │                 │                  │                  │ 
       Proxmox            Proxmox           Proxmox              AP
        hosts              hosts             hosts
```

## Implementation order

1. Factory/reset baseline
2. Administrator security
3. System identity and time
4. WAN
5. Temporary LAN
6. Internet connectivity
7. Configuration backup
8. Management VLAN
9. VLAN interfaces
10. DHCP
11. Firewall address objects
12. Internet policies with NAT
13. Inter-VLAN default-deny
14. Explicit inter-VLAN exceptions
15. Logging
16. Verification
17. Backup and change record

## Documentation rules

Never commit:

- Unencrypted configuration backups
- Administrator passwords
- VPN private keys
- API tokens
- Public IPs
- ISP credentials
- Serial numbers unless intentionally required
- Sensitive logs
- Secrets embedded in screenshots


## Related documentation

- `01-architecture/` — network architecture and VLAN design
- `02-hardware/` — physical rack and equipment
- `04-switching/` — MokerLink switching
- `08-wazuh/` — SIEM/XDR
- `09-security-onion/` — network detection
- `15-security-testing/` — controlled security tests
- `19-opnsense-migration/` — future firewall migration

