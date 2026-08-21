# Ticket 01 — No Default Gateway Configured

## Ticket Details

| Field | Details |
|---|---|
| Ticket Number | NET-001 |
| Category | Network Connectivity |
| Priority | Medium |
| Status | Resolved |
| Affected Device | WIN10-CLIENT |
| User Impact | User can access internal network resources but cannot reach external internet addresses |

## User Issue

The user reports that they can access internal company resources but cannot connect to external internet services.

## Symptoms

The client could successfully communicate with the internal domain controller:

```cmd
ping 192.168.10.10
```

However, external connectivity failed when testing:

```cmd
ping 8.8.8.8
```

The ping test returned a general failure message.

## Troubleshooting Steps

1. Checked the full IP configuration using:

```cmd
ipconfig /all
```

2. Confirmed that the client had a valid internal IP address:

```text
192.168.10.20
```

3. Confirmed that the DNS server was set to the domain controller:

```text
192.168.10.10
```

4. Checked the IPv4 adapter settings.

5. Identified that the default gateway field was blank.

## Root Cause

The client did not have a default gateway configured.

This meant the computer could communicate with devices on the internal lab network but had no route to external networks or the internet.

## Resolution

The issue was documented as a default gateway configuration problem.

In a real environment, the next step would be to confirm the correct gateway address and configure it manually or through DHCP.

## Closure Note

The client’s internal network configuration was working, but external connectivity failed because no default gateway was configured. The issue was identified and documented.

## Skills Demonstrated

- Network troubleshooting
- IP configuration review
- Default gateway troubleshooting
- Ping testing
- IPv4 adapter review
- Service desk documentation
