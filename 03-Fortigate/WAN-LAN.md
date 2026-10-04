# WAN and LAN Configuration

## Objective

Establish the basic routed topology before adding VLANs.

## Physical topology

```text
Apartment Ethernet
       │
       ▼
FortiGate WAN1
       │
FortiGate LAN
       │
       ▼
MokerLink switch
       │
       ▼
Lab devices
```

## WAN

### Recommended initial configuration

Use DHCP on WAN1 because my apartment/provider network is expected to assign the upstream address.

GUI:

```text
Network → Interfaces → WAN1
```
<img width="505" height="57" alt="image" src="https://github.com/user-attachments/assets/cf451d2d-2cb1-4f0f-80d5-87f74752a195" />

### WAN verification

```text
get system interface physical
get router info routing-table all
```
<img width="468" height="177" alt="image" src="https://github.com/user-attachments/assets/f66e6d63-b9ae-4dc5-82ec-5fb59a7cf5c5" />

Confirm:

- WAN link is up
- DHCP address exists
- Default route exists
- No unexpected administrative exposure exists

## Temporary LAN

Before VLAN deployment, use a simple management LAN:

```text
IP:      192.168.10.1/24
DHCP:    192.168.10.100–192.168.10.199
Gateway: 192.168.10.1
DNS:     1.1.1.1
```

Connect:

```text
FortiGate LAN → MokerLink → Administration PC
```

The PC should receive a 192.168.10.x address.

## Internet test

From the administration PC:

```powershell
ipconfig
ping 192.168.10.1
ping 1.1.1.1
nslookup example.com
```

Expected:

1. Local gateway responds.
2. 1.1.1.1 responds if ICMP is permitted upstream.
3. DNS resolution works.

A failed ping to 1.1.1.1 does not automatically prove that Internet access is broken because ICMP may be filtered. Test HTTPS/DNS as well.

## LAN-to-WAN policy

Create the initial policy:

```text
Name: LAB-LAN-to-INTERNET
Incoming: LAN
Outgoing: WAN1
Source: LAN subnet
Destination: all
Schedule: always
Service: DNS, HTTP, HTTPS, NTP initially
Action: ACCEPT
NAT: enabled
Log allowed traffic: enabled during testing
```

After the baseline is proven, replace broad temporary rules with VLAN-specific policies.

## Acceptance criteria

- [ ] WAN DHCP works
- [ ] Default route exists
- [ ] LAN client gets DHCP
- [ ] Client reaches FortiGate
- [ ] DNS works
- [ ] HTTPS Internet access works
- [ ] Firewall policy hit counter increments
- [ ] NAT sessions appear

