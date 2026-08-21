# Ticket 03 — Public DNS Cannot Resolve Private Domain

## Ticket Details

| Field | Details |
|---|---|
| Ticket Number | NET-003 |
| Category | DNS |
| Priority | Low |
| Status | Resolved |
| Affected Device | WIN10-CLIENT |
| User Impact | Internal domain could not be resolved when tested against public DNS |

## User Issue

The user reports that the internal domain name does not resolve when tested against Google public DNS.

## Symptoms

The private Active Directory domain failed when tested using:

```cmd
nslookup shirleylab.local 8.8.8.8
```

The result showed that public DNS could not find the domain.

However, the same domain resolved when tested using the internal domain controller DNS server:

```cmd
nslookup shirleylab.local 192.168.10.10
```

## Troubleshooting Steps

1. Tested the private domain using Google public DNS:

```cmd
nslookup shirleylab.local 8.8.8.8
```

2. Confirmed that public DNS could not resolve the private lab domain.

3. Tested the private domain using the internal domain controller DNS server:

```cmd
nslookup shirleylab.local 192.168.10.10
```

4. Confirmed that the internal DNS server resolved the domain correctly.

5. Tested DNS cache commands:

```cmd
ipconfig /displaydns
ipconfig /flushdns
```

6. Tested DNS resolution again after clearing the cache.

## Root Cause

The domain `shirleylab.local` is a private Active Directory domain.

Public DNS servers such as `8.8.8.8` do not hold records for private internal domains.

## Resolution

Confirmed that the correct DNS server for resolving the internal Active Directory domain is the domain controller DNS server:

```text
192.168.10.10
```

## Closure Note

The issue was confirmed as expected DNS behaviour. Public DNS cannot resolve the private lab domain, but the internal Active Directory DNS server can.

## Skills Demonstrated

- DNS troubleshooting
- Public vs internal DNS testing
- Active Directory DNS checks
- `nslookup`
- DNS cache review
- DNS cache flushing
- Service desk documentation
