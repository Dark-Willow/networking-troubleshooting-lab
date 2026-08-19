# Lab 03 — DNS Troubleshooting & DNS Cache Commands

## Objective

The objective of this lab was to practise DNS troubleshooting commands used in IT Support and Service Desk roles.

## Lab Environment

| Component | Details |
|---|---|
| Virtualisation | Oracle VirtualBox |
| Client OS | Windows 10 Pro |
| Client Name | WIN10-CLIENT |
| Domain | shirleylab.local |
| Domain Controller | AD-DC01 |
| Domain Controller IP Address | 192.168.10.10 |
| Internal DNS Server | 192.168.10.10 |
| Public DNS Server Tested | 8.8.8.8 |

## Tasks Completed

- Tested the internal Active Directory domain using public DNS
- Confirmed that public DNS could not resolve the private domain
- Tested the internal Active Directory domain using the domain controller DNS server
- Confirmed that the domain controller could resolve `shirleylab.local`
- Pinged the domain name
- Displayed the DNS resolver cache
- Flushed the DNS resolver cache
- Tested DNS resolution again after clearing the cache

## Commands Used

```cmd
nslookup shirleylab.local 8.8.8.8
nslookup shirleylab.local 192.168.10.10
ping shirleylab.local
ipconfig /displaydns
ipconfig /flushdns
nslookup shirleylab.local
```

## Evidence Collected

- `12-nslookup-public-dns-failed.png`
- `13-nslookup-domain-controller-dns-success.png`
- `14-ping-domain-name.png`
- `15-display-dns-cache.png`
- `16-flush-dns-cache.png`
- `17-nslookup-after-dns-flush.png`

## Troubleshooting Notes

Public DNS was tested using `8.8.8.8`. This failed to resolve `shirleylab.local` because the domain is a private Active Directory domain and is not known to public DNS servers.

The domain controller DNS server at `192.168.10.10` was then tested. This successfully resolved `shirleylab.local`, showing that internal DNS was working correctly.

The DNS cache was displayed using `ipconfig /displaydns`, then cleared using `ipconfig /flushdns`. DNS resolution was tested again after the cache was cleared.

## What I Learned

This lab helped me understand the difference between public DNS and internal Active Directory DNS.

I learned that private domains such as `shirleylab.local` should be resolved by the internal domain controller DNS server, not by public DNS servers like `8.8.8.8`.

I also practised using DNS cache commands to display and clear cached DNS records during troubleshooting.
