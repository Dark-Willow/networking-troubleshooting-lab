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
