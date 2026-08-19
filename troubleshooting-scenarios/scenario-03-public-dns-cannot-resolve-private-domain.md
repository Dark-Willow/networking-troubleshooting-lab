# Scenario 03 — Public DNS Cannot Resolve Private Active Directory Domain

## Issue

The Windows 10 client could resolve the internal Active Directory domain using the domain controller DNS server, but public DNS could not resolve the same domain.

## Environment

| Component | Details |
|---|---|
| Client | WIN10-CLIENT |
| Domain | shirleylab.local |
| Domain Controller | AD-DC01 |
| Internal DNS Server | 192.168.10.10 |
| Public DNS Server Tested | 8.8.8.8 |

## Symptoms

When testing the private domain with Google public DNS, the lookup failed:

```cmd
nslookup shirleylab.local 8.8.8.8
```

The result showed that public DNS could not find the domain:

```text
dns.google can't find shirleylab.local: Non-existent domain
```

However, when using the internal domain controller DNS server, the lookup succeeded:

```cmd
nslookup shirleylab.local 192.168.10.10
```

## Investigation

The DNS tests showed that `shirleylab.local` is an internal Active Directory domain.

Public DNS servers, such as `8.8.8.8`, do not hold records for private internal domains.

The domain controller DNS server at `192.168.10.10` was able to resolve the domain correctly.

## Cause

The issue occurred because the client was testing a private Active Directory domain against a public DNS server.

Public DNS can resolve internet domains, but it cannot resolve private lab domains such as `shirleylab.local`.

## Resolution

The correct DNS server for resolving the internal Active Directory domain is the domain controller DNS server:

```text
192.168.10.10
```

The client should use the internal DNS server for Active Directory domain resolution.

DNS cache commands were also used to support troubleshooting:

```cmd
ipconfig /displaydns
ipconfig /flushdns
```

## Verification

The following commands were used to verify DNS behaviour:

```cmd
nslookup shirleylab.local 8.8.8.8
nslookup shirleylab.local 192.168.10.10
ping shirleylab.local
ipconfig /displaydns
ipconfig /flushdns
nslookup shirleylab.local
```

## Skills Demonstrated

- DNS troubleshooting
- Internal vs public DNS testing
- Active Directory DNS checks
- `nslookup`
- DNS cache review
- DNS cache flushing
- Ping testing
- Service desk documentation
