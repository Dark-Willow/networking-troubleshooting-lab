# Ticket 04 — Disabled NAT Adapter Causing No Internet Access

## Ticket Details

| Field | Details |
|---|---|
| Ticket Number | NET-004 |
| Category | Network Adapter |
| Priority | Medium |
| Status | Resolved |
| Affected Device | WIN10-CLIENT |
| User Impact | User lost external internet connectivity because the NAT adapter was disabled |

## User Issue

The user reports that the computer can no longer access external internet services.

## Symptoms

External connectivity failed after the NAT adapter was disabled.

The client could not reach:

```cmd
ping 8.8.8.8
```

## Troubleshooting Steps

1. Opened Windows Network Connections.

2. Reviewed the available network adapters.

3. Confirmed that the client had two adapters:

- Internal Active Directory lab adapter
- NAT adapter for internet access

4. Confirmed that the NAT adapter was disabled.

5. Checked IP configuration using:

```cmd
ipconfig /all
```

6. Enabled the NAT adapter again.

7. Tested external connectivity using:

```cmd
ping 8.8.8.8
```

8. Confirmed internal DNS resolution using:

```cmd
nslookup shirleylab.local
```

## Root Cause

The NAT adapter used for internet access was disabled.

Without the NAT adapter, the client did not have the external route needed to reach internet addresses.

## Resolution

The NAT adapter was enabled again through Windows Network Connections.

After enabling the adapter, external connectivity was restored.

## Closure Note

The internet connectivity issue was resolved by enabling the disabled NAT adapter. Internal Active Directory DNS resolution was also confirmed.

## Skills Demonstrated

- Network adapter troubleshooting
- Windows Network Connections
- Disabled adapter investigation
- `ipconfig /all`
- Ping testing
- DNS testing
- Service desk documentation
