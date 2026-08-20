# Scenario 04 — Disabled NAT Adapter Causing No Internet Access

## Issue

The Windows 10 client lost external internet connectivity because the NAT network adapter was disabled.

## Environment

| Component | Details |
|---|---|
| Client | WIN10-CLIENT |
| Domain | shirleylab.local |
| Domain Controller | AD-DC01 |
| Internal Lab Network | AD-LAB |
| Internal DNS Server | 192.168.10.10 |
| NAT Adapter | Ethernet 2 |
| NAT Default Gateway | 10.0.3.2 |

## Symptoms

The client could no longer reach external internet addresses after the NAT adapter was disabled.

External connectivity failed when testing with:

```cmd
ping 8.8.8.8
```

## Investigation

The network adapter settings were reviewed using the Windows Network Connections panel.

The client had two adapters:

- Internal Active Directory lab adapter
- NAT adapter for internet access

The NAT adapter was found to be disabled.

The IP configuration was also checked using:

```cmd
ipconfig /all
```

## Cause

The issue occurred because the NAT adapter used for internet access was disabled.

Without the NAT adapter, the client no longer had the external route needed to reach internet addresses such as `8.8.8.8`.

## Resolution

The NAT adapter was enabled again through the Windows Network Connections panel.

After the adapter was enabled, external connectivity was tested again using:

```cmd
ping 8.8.8.8
```

The ping test succeeded after the NAT adapter was restored.

Internal DNS was also tested using:

```cmd
nslookup shirleylab.local
```

This confirmed that the Active Directory lab DNS still worked.

## Verification

The following checks were used to verify the issue and resolution:

```cmd
ipconfig /all
ping 8.8.8.8
nslookup shirleylab.local
```

## Skills Demonstrated

- Network adapter troubleshooting
- Windows Network Connections
- Disabled adapter investigation
- Internet connectivity testing
- `ipconfig /all`
- Ping testing
- Active Directory DNS checks
- Service desk documentation
