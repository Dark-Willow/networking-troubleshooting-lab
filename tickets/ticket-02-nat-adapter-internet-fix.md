# Ticket 02 — Internet Connectivity Restored with NAT Adapter

## Ticket Details

| Field | Details |
|---|---|
| Ticket Number | NET-002 |
| Category | Network Connectivity |
| Priority | Medium |
| Status | Resolved |
| Affected Device | WIN10-CLIENT |
| User Impact | User could not reach external internet addresses until NAT connectivity was restored |

## User Issue

The user reports that the computer cannot access external internet services.

## Symptoms

The client could communicate with the internal Active Directory lab network but could not reach external internet addresses.

External connectivity failed when testing:

```cmd
ping 8.8.8.8
```

## Troubleshooting Steps

1. Checked the client IP configuration using:

```cmd
ipconfig /all
```

2. Confirmed that the internal adapter was connected to the AD-LAB network.

3. Confirmed that the internal adapter had the correct internal IP address:

```text
192.168.10.20
```

4. Confirmed that the client could still reach the domain controller:

```cmd
ping 192.168.10.10
```

5. Added a second VirtualBox network adapter and configured it as NAT.

6. Confirmed that the NAT adapter received a default gateway:

```text
10.0.3.2
```

7. Tested internet connectivity again using:

```cmd
ping 8.8.8.8
```

## Root Cause

The client only had an internal lab network adapter configured and did not have an external route for internet access.

## Resolution

A second network adapter was added to the Windows 10 client and configured as NAT.

This allowed the client to keep its internal Active Directory lab network connection while also gaining internet access through the NAT adapter.

## Closure Note

External connectivity was restored after adding and verifying the NAT adapter. Internal Active Directory DNS resolution continued to work.

## Skills Demonstrated

- VirtualBox network adapter configuration
- NAT troubleshooting
- Default gateway checks
- Ping testing
- Internal vs external connectivity testing
- Active Directory DNS checks
- Service desk documentation
