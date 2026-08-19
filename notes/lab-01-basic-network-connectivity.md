# Lab 01 — Basic Network Configuration & Connectivity Testing

## Objective

The objective of this lab was to practise basic Windows networking checks used in IT Support and Service Desk troubleshooting.

## Lab Environment

| Component | Details |
|---|---|
| Virtualisation | Oracle VirtualBox |
| Client OS | Windows 10 Pro |
| Client Name | WIN10-CLIENT |
| Domain | shirleylab.local |
| Domain Controller | AD-DC01 |
| Client IP Address | 192.168.10.20 |
| Domain Controller IP Address | 192.168.10.10 |
| DNS Server | 192.168.10.10 |

## Tasks Completed

- Checked full network configuration using `ipconfig /all`
- Tested connectivity to the domain controller using `ping`
- Tested internet connectivity using `ping 8.8.8.8`
- Tested DNS resolution for `shirleylab.local` using `nslookup`
- Tested route path using `tracert`
- Reviewed IPv4 network adapter settings
- Identified that the client had no default gateway configured

## Commands Used

```cmd
ipconfig /all
ping 192.168.10.10
ping 8.8.8.8
nslookup shirleylab.local
tracert 8.8.8.8
