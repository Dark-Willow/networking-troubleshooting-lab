# Scenario 02 — Fixing Internet Connectivity with NAT Adapter

## Issue

The Windows 10 client could communicate with the internal Active Directory lab network but could not reach external internet addresses.

## Environment

| Component | Details |
|---|---|
| Client | WIN10-CLIENT |
| Domain | shirleylab.local |
| Domain Controller | AD-DC01 |
| Internal Network | AD-LAB |
| Internal Client IP Address | 192.168.10.20 |
| Domain Controller IP Address | 192.168.10.10 |
| NAT Adapter IP Address | 10.0.3.15 |
| NAT Default Gateway | 10.0.3.2 |

## Symptoms

In Lab 01, the client failed when testing external connectivity using:

```cmd
ping 8.8.8.8
```

The client had a working internal IP address and DNS server, but the default gateway field was blank.

## Investigation

The network adapter settings were reviewed.

The first adapter was configured for the internal Active Directory lab network:

- IP address: `192.168.10.20`
- Subnet mask: `255.255.255.0`
- DNS server: `192.168.10.10`
- Default gateway: blank

This allowed the client to communicate with the domain controller but did not provide a route to the internet.

## Cause

The client only had an internal lab network adapter configured.

Because there was no default gateway, the client had no route to external networks.

## Resolution

A second network adapter was added to WIN10-CLIENT in VirtualBox.

The adapter setup was:

| Adapter | Purpose | Configuration |
|---|---|---|
| Adapter 1 | Internal Active Directory lab network | Internal Network / AD-LAB |
| Adapter 2 | Internet access | NAT |

After adding the NAT adapter, the client received:

- NAT IP address: `10.0.3.15`
- NAT default gateway: `10.0.3.2`

The client was then able to reach external internet addresses using:

```cmd
ping 8.8.8.8
```

The client was also still able to communicate with the domain controller using:

```cmd
ping 192.168.10.10
```

## Verification

The following commands were used to confirm the fix:

```cmd
ipconfig /all
ping 8.8.8.8
ping 192.168.10.10
nslookup shirleylab.local
```

## Skills Demonstrated

- Network adapter troubleshooting
- VirtualBox NAT configuration
- Default gateway troubleshooting
- Internal vs external network testing
- Ping testing
- DNS testing
- Active Directory lab networking
- Service desk documentation
