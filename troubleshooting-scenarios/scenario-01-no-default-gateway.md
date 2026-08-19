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
