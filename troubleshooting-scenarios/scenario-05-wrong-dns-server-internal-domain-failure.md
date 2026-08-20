# Scenario 05 — Wrong DNS Server Causing Internal Domain Resolution Failure

## Issue

The Windows 10 client had network connectivity, but it could not resolve the internal Active Directory domain because the wrong DNS server was configured.

## Environment

| Component | Details |
|---|---|
| Client | WIN10-CLIENT |
| Domain | shirleylab.local |
| Domain Controller | AD-DC01 |
| Internal Lab Network | AD-LAB |
| Internal Client IP Address | 192.168.10.20 |
| Correct Internal DNS Server | 192.168.10.10 |
| Incorrect DNS Server Tested | 8.8.8.8 |

## Symptoms

The client could still reach an external IP address using:

```cmd
ping 8.8.8.8
```

However, the client could not resolve the internal Active Directory domain using:

```cmd
nslookup shirleylab.local
```

## Investigation

The IPv4 DNS configuration was reviewed.

The client was expected to use the internal domain controller DNS server:

```text
192.168.10.10
```

However, the DNS server was changed to:

```text
8.8.8.8
```

This meant the client was using public DNS instead of the internal Active Directory DNS server.

## Cause

The issue occurred because the client was configured with the wrong DNS server.

Public DNS servers such as `8.8.8.8` can resolve public internet domains, but they cannot resolve private Active Directory domains such as `shirleylab.local`.

## Resolution

The DNS server was restored to the internal domain controller DNS server:

```text
192.168.10.10
```

After restoring the correct DNS server, the DNS resolver cache was cleared using:

```cmd
ipconfig /flushdns
```

The internal domain was then tested again using:

```cmd
nslookup shirleylab.local
```

The lookup succeeded after the correct DNS server was restored.

## Verification

The following checks were used to verify the issue and resolution:

```cmd
ping 8.8.8.8
nslookup shirleylab.local
ipconfig /flushdns
nslookup shirleylab.local
```

## Skills Demonstrated

- DNS troubleshooting
- DNS misconfiguration investigation
- Internal vs public DNS testing
- Active Directory DNS checks
- `nslookup`
- Ping testing
- DNS cache flushing
- IPv4 configuration review
- Service desk documentation
