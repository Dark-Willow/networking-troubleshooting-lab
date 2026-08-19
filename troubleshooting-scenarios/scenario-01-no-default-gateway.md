# Scenario 01 — No Default Gateway Configured

## Issue

The Windows 10 client could reach the internal Active Directory domain controller but could not reach an external IP address.

## Environment

| Component | Details |
|---|---|
| Client | WIN10-CLIENT |
| Domain | shirleylab.local |
| Client IP Address | 192.168.10.20 |
| Domain Controller IP Address | 192.168.10.10 |
| DNS Server | 192.168.10.10 |

## Symptoms

The client successfully reached the domain controller using:

```cmd
ping 192.168.10.10

Investigation

The IPv4 network adapter settings were checked.

The client had:

IP address: 192.168.10.20
Subnet mask: 255.255.255.0
DNS server: 192.168.10.10
Default gateway: blank
Cause

The client did not have a default gateway configured.

This meant the computer could communicate with devices on the internal lab network but had no route to external networks or the internet.

Resolution

For this lab, the issue was documented rather than changed.

In a real environment, the next step would be to confirm the correct gateway address and configure it manually or through DHCP.

Skills Demonstrated
Network troubleshooting
ipconfig /all
Ping testing
DNS testing
Default gateway troubleshooting
IPv4 configuration review
Service desk documentation
