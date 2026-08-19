# Lab 02 — Fixing Internet Connectivity with NAT Adapter

## Objective

The objective of this lab was to fix the internet connectivity issue identified in Lab 01 while keeping the Windows client connected to the internal Active Directory lab network.

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
| NAT Adapter IP Address | 10.0.3.15 |
| NAT Default Gateway | 10.0.3.2 |

## Tasks Completed

- Added a second network adapter to WIN10-CLIENT in VirtualBox
- Kept Adapter 1 connected to the internal AD-LAB network
- Set Adapter 2 to NAT for internet access
- Checked network configuration using `ipconfig /all`
- Confirmed the client received a NAT IP address
- Confirmed the NAT adapter had a default gateway
- Tested internet connectivity using `ping 8.8.8.8`
- Confirmed the client could still reach the domain controller using `ping 192.168.10.10`
- Tested Active Directory DNS resolution using `nslookup shirleylab.local`

## Network Adapter Setup

| Adapter | Purpose | Configuration |
|---|---|---|
| Adapter 1 | Internal Active Directory lab network | Internal Network / AD-LAB |
| Adapter 2 | Internet access | NAT |

## Commands Used

```cmd
ipconfig /all
ping 8.8.8.8
ping 192.168.10.10
nslookup shirleylab.local
