# Lab 05 — DNS Misconfiguration Troubleshooting

## Objective

The objective of this lab was to practise troubleshooting a DNS misconfiguration issue where the client still had network connectivity but could not resolve the internal Active Directory domain.

## Lab Environment

| Component | Details |
|---|---|
| Virtualisation | Oracle VirtualBox |
| Client OS | Windows 10 Pro |
| Client Name | WIN10-CLIENT |
| Domain | shirleylab.local |
| Domain Controller | AD-DC01 |
| Internal Lab Network | AD-LAB |
| Internal Client IP Address | 192.168.10.20 |
| Domain Controller IP Address | 192.168.10.10 |
| Correct Internal DNS Server | 192.168.10.10 |
| Incorrect DNS Server Tested | 8.8.8.8 |

## Tasks Completed

- Reviewed the correct DNS configuration before making changes
- Changed the client DNS server from `192.168.10.10` to `8.8.8.8`
- Confirmed that IP connectivity still worked using `ping 8.8.8.8`
- Tested internal domain name resolution using `nslookup shirleylab.local`
- Confirmed that internal DNS resolution failed while the wrong DNS server was configured
- Restored the DNS server to `192.168.10.10`
- Flushed the DNS resolver cache
- Confirmed that internal DNS resolution worked again after restoring the correct DNS server

## Commands Used

```cmd
ping 8.8.8.8
nslookup shirleylab.local
ipconfig /flushdns
```

## Evidence Collected

- `25-correct-dns-before-change.png`
- `26-wrong-dns-configured.png`
- `27-ping-google-dns-success-with-wrong-dns.png`
- `28-nslookup-domain-failed-wrong-dns.png`
- `29-dns-restored-to-domain-controller.png`
- `30-flush-dns-after-restore.png`
- `31-nslookup-domain-success-after-dns-restore.png`

## Troubleshooting Notes

The Windows 10 client originally used the domain controller at `192.168.10.10` as its DNS server. This is the correct DNS server for resolving the private Active Directory domain `shirleylab.local`.

The DNS server was then changed to `8.8.8.8` to simulate a DNS misconfiguration.

The client could still ping `8.8.8.8`, which showed that basic IP connectivity was working. However, `nslookup shirleylab.local` failed because Google public DNS does not hold records for the private Active Directory domain.

The DNS server was restored to `192.168.10.10`, and the DNS resolver cache was flushed using `ipconfig /flushdns`.

After restoring the correct DNS server, `nslookup shirleylab.local` worked again.

## What I Learned

This lab helped me understand how DNS misconfiguration can affect internal domain access even when the computer still has network connectivity.

I learned that being able to ping an external IP address does not always mean DNS is configured correctly.

I also learned that Active Directory domain clients should use the internal domain controller DNS server for private domain resolution, and that public DNS servers such as `8.8.8.8` cannot resolve private lab domains like `shirleylab.local`.

This is a common IT Support and Service Desk troubleshooting scenario when users can access some network resources but cannot access domain-based services.
