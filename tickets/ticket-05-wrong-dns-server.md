# Ticket 05 — Wrong DNS Server Causing Internal Domain Resolution Failure

## Ticket Details

| Field | Details |
|---|---|
| Ticket Number | NET-005 |
| Category | DNS |
| Priority | Medium |
| Status | Resolved |
| Affected Device | WIN10-CLIENT |
| User Impact | User had network connectivity but could not resolve the internal Active Directory domain |

## User Issue

The user reports that the computer has network connectivity but cannot resolve the internal domain name.

## Symptoms

The client could still reach an external IP address:

```cmd
ping 8.8.8.8
```

However, the client could not resolve the internal Active Directory domain:

```cmd
nslookup shirleylab.local
```

## Troubleshooting Steps

1. Confirmed that IP connectivity was working by running:

```cmd
ping 8.8.8.8
```

2. Tested internal domain name resolution using:

```cmd
nslookup shirleylab.local
```

3. Reviewed the IPv4 DNS settings.

4. Identified that the client was using the wrong DNS server:

```text
8.8.8.8
```

5. Restored the DNS server to the internal domain controller:

```text
192.168.10.10
```

6. Flushed the DNS resolver cache:

```cmd
ipconfig /flushdns
```

7. Tested internal domain name resolution again:

```cmd
nslookup shirleylab.local
```

## Root Cause

The client was configured to use public DNS instead of the internal Active Directory DNS server.

Public DNS can resolve internet domains, but it cannot resolve private Active Directory domains such as `shirleylab.local`.

## Resolution

The DNS server was restored to the internal domain controller DNS server:

```text
192.168.10.10
```

The DNS cache was then flushed, and internal domain resolution worked again.

## Closure Note

The DNS issue was resolved by restoring the correct internal DNS server and clearing the DNS resolver cache.

## Skills Demonstrated

- DNS troubleshooting
- DNS misconfiguration investigation
- Public vs internal DNS testing
- Active Directory DNS checks
- `nslookup`
- Ping testing
- DNS cache flushing
- IPv4 configuration review
- Service desk documentation
