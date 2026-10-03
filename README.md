# Security Engineering Lab
Enterprise-style cybersecurity, networking, virtualization, detection engineering, and cloud security home lab.

## Overview
This project documents the design, deployment, operation, and security testing of a multi-VLAN home cybersecurity laboratory.

The lab is designed to simulate enterprise infrastructure and provide hands-on experience with:

- Network security
- Firewall administration
- VLAN segmentation
- Network monitoring
- Security information and event management
- Vulnerability management
- Active Directory
- Linux administration
- Virtualization
- Incident response
- Detection engineering
- Cloud security
- VPN and remote access
- Disaster recovery

## Architecture

Current core infrastructure:

- Fortinet FortiGate 61E
- Managed 8 Port 2.5GbE network switch
- Three Intel NUC8i7BEH Proxmox hosts
- Custom Windows workstation
- Wireless access point
- Synology 2 Bay NAS

## Virtualization

The lab uses three Proxmox VE hosts.

Each host:

- Intel Core i7
- 32 GB RAM
- 256 GB NVMe

The Proxmox hosts form the virtualization foundation for the laboratory.

## Network Segmentation

| VLAN | Name | Purpose |
|---:|---|---|
| 10 | Management | Network and infrastructure management |
| 20 | Servers | Core infrastructure services |
| 30 | Trusted | Trusted user devices |
| 40 | Security | Security monitoring and security tools |
| 50 | Attack | Kali and intentionally vulnerable systems |
| 60 | IoT | Internet-connected IoT devices |
| 70 | Guest | Guest wireless access |
| 80 | NAS | Backup Storage |

## Security Philosophy

The lab follows a defense-in-depth model:

1. Network segmentation
2. Least privilege
3. Default-deny firewall policies
4. Centralized logging
5. Network monitoring
6. Endpoint monitoring
7. Vulnerability management
8. Controlled attack simulation
9. Incident response
10. Continuous validation

## Security Testing

Security testing will follow an:

Attack → Detection → Investigation → Containment → Remediation → Retest methodology.

All attack simulations are conducted against intentionally authorized laboratory systems.

## Future Development

Planned capabilities include:

- Wazuh
- Security Onion
- Nessus
- Kali Linux
- Active Directory
- AdGuard Home
- Tailscale
- RustDesk
- Azure security laboratory
- Detection engineering
- Incident response exercises
- Disaster recovery testing
- FortiGate to OPNsense migration

## Disclaimer

This repository documents an authorized personal laboratory.

Security testing is performed only against systems owned or explicitly
authorized by the lab operator.
