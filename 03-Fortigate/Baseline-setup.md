# FortiGate Baseline Setup

## Objective

Establish a known-good FortiGate 61E baseline before implementing VLAN segmentation and security policies.

## 1. Factory/reset baseline

The lab FortiGate has been reset and the administrator password has been changed.

Record:

```text
Hostname: FG-LAB-01
Model: FortiGate 61E
FortiOS: 7.2.10
VDOM: root
Mode: NAT/Route
```

## 2. Administrative security

Immediately:

- Change the default administrator password.
- Use HTTPS for GUI administration.
- Restrict administrative access to trusted management networks.
- Disable HTTP administration if not required.
- Disable insecure management protocols.
- Create named administrator accounts for additional operators if needed.
- Use least-privilege administrator profiles where practical.

Fortinet documents administrator profiles and password policy as core system configuration areas. citeturn0search0

## 3. Hostname

Recommended:

```text
FG-LAB-01
```

CLI example:

```text
config system global
    set hostname "FG-LAB-01"
end
```
<img width="925" height="362" alt="Screenshot 2026-10-04 155318" src="https://github.com/user-attachments/assets/11c88ff0-bcb4-4b0a-a75e-ae95104bfa01" />


## 4. Time

Use a reliable NTP source.

GUI location varies slightly by FortiOS build, but the target is:

```text
System → Settings → Time / NTP
```

Verification:

```text
get system status
```

The clock must be correct before relying on logs for incident-response evidence.

## 5. DNS

Initial DNS:

```text
1.1.1.1
1.0.0.1
```

Later, the lab will place AdGuard and the domain controller in the DNS path. 

<img width="708" height="178" alt="Screenshot 2026-10-04 160941" src="https://github.com/user-attachments/assets/20a31172-e2f3-48ee-93bf-0dac95b347f9" />

## 6. Firmware

The current documented baseline is FortiOS 7.2.10.

## 7. Initial backup

After the basic system settings work:

```text
Admin username/password changed
Hostname set
Time verified
DNS configured
WAN/LAN baseline tested
```

perform a configuration backup.

Fortinet recommends backing up configuration after successful configuration and before firmware changes. Encrypted backups are recommended. citeturn0search1turn0search6

## Baseline acceptance criteria

- [x] Administrator password changed
- [x] Hostname set
- [x] Time synchronized
- [x] DNS configured
- [x] WAN link established
- [x] LAN management reachable
- [x] Internet reachable
- [x] First encrypted backup completed

