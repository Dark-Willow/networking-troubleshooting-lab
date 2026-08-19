# Networking Troubleshooting Lab

## Project Overview

This repository documents a hands-on networking troubleshooting lab using a Windows 10 client in an Active Directory lab environment.

The purpose of this project is to practise common IT Support and Service Desk network checks, including IP configuration review, ping testing, DNS testing, traceroute checks, IPv4 adapter review, default gateway troubleshooting, NAT adapter configuration, and troubleshooting documentation.

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
| DNS Server | 192.168.10.10 |
| NAT Adapter IP Address | 10.0.3.15 |
| NAT Default Gateway | 10.0.3.2 |

## Completed Labs

| Lab | Topic | Status |
|---|---|---|
| Lab 01 | Basic Network Configuration & Connectivity Testing | Complete |
| Lab 02 | Fixing Internet Connectivity with NAT Adapter | Complete |

## Lab Notes

- [Lab 01 — Basic Network Configuration & Connectivity Testing](notes/lab-01-basic-network-connectivity.md)
- [Lab 02 — Fixing Internet Connectivity with NAT Adapter](notes/lab-02-nat-adapter-internet-connectivity.md)

## Troubleshooting Scenarios

- [Scenario 01 — No Default Gateway Configured](troubleshooting-scenarios/scenario-01-no-default-gateway.md)
- [Scenario 02 — Fixing Internet Connectivity with NAT Adapter](troubleshooting-scenarios/scenario-02-fixing-internet-connectivity-with-nat.md)

## Lab 01: Basic Network Configuration & Connectivity Testing

### IP Configuration

Checked full network configuration using `ipconfig /all`.

![IP Configuration](screenshots/01-ipconfig-all.png)

### Ping Domain Controller

Tested connectivity from the Windows 10 client to the domain controller.

![Ping Domain Controller](screenshots/02-ping-domain-controller.png)

### Ping Google DNS Failed

Tested external connectivity using `ping 8.8.8.8`. The test failed because the client did not have a default gateway configured.

![Ping Google DNS Failed](screenshots/03-ping-google-dns-failed.png)

### No Default Gateway Identified

Reviewed IP configuration and confirmed that the default gateway field was blank.

![No Default Gateway](screenshots/04-ipconfig-no-default-gateway.png)

### DNS Lookup for Domain

Used `nslookup shirleylab.local` to test DNS resolution for the Active Directory domain.

![NSLookup Domain](screenshots/04-nslookup-domain.png)

### Traceroute to Google DNS Failed

Used `tracert 8.8.8.8` to test the route to an external IP address. The test failed because there was no route outside the internal lab network.

![Traceroute Google DNS Failed](screenshots/05-tracert-google-dns-failed.png)

### Network Adapter Settings

Reviewed IPv4 adapter settings and confirmed that the default gateway field was blank.

![Network Adapter Settings](screenshots/06-network-adapter-settings.png)

## Lab 02: Fixing Internet Connectivity with NAT Adapter

### VirtualBox NAT Adapter Enabled

Added a second network adapter to WIN10-CLIENT and configured it as NAT for internet access.

![VirtualBox NAT Adapter Enabled](screenshots/07-virtualbox-nat-adapter-enabled.png)

### IP Configuration After NAT Adapter

Checked `ipconfig /all` and confirmed that the client now had two network adapters: one for the internal AD-LAB network and one NAT adapter with a default gateway.

![IP Configuration After NAT Adapter](screenshots/08-ipconfig-after-nat-adapter.png)

### Ping Google DNS Success

Tested external connectivity again using `ping 8.8.8.8`. The test succeeded after adding the NAT adapter.

![Ping Google DNS Success](screenshots/09-ping-google-dns-success.png)

### Ping Domain Controller After NAT

Confirmed that the client could still communicate with the domain controller after adding the NAT adapter.

![Ping Domain Controller After NAT](screenshots/10-ping-domain-controller-after-nat.png)

### DNS Lookup After NAT

Confirmed that Active Directory DNS resolution still worked using `nslookup shirleylab.local`.

![NSLookup Domain After NAT](screenshots/11-nslookup-domain-after-nat.png)

## Commands Used

```cmd
ipconfig /all
ping 192.168.10.10
ping 8.8.8.8
nslookup shirleylab.local
tracert 8.8.8.8
```

## Skills Practised

- Network troubleshooting
- Windows command-line networking
- IP configuration review
- Ping testing
- DNS testing
- Traceroute testing
- IPv4 adapter review
- Default gateway troubleshooting
- NAT adapter configuration
- VirtualBox networking
- Internal vs external network testing
- Active Directory DNS checks
- Service desk documentation
- Technical documentation

## What I Learned

This lab helped me practise basic networking checks used in IT Support and Service Desk roles.

In Lab 01, I learned how to check IP configuration, test connectivity to an internal domain controller, test DNS resolution, and identify why a client could reach internal resources but not external internet addresses.

The main issue identified was that the Windows client had no default gateway configured. This explained why communication inside the lab network worked, but external connectivity to `8.8.8.8` failed.

In Lab 02, I added a second VirtualBox network adapter and configured it as NAT. This allowed the Windows client to keep its internal Active Directory lab connection while also gaining internet access through a separate NAT adapter.

This helped me understand the difference between internal lab networking, DNS, default gateways, NAT, and internet connectivity troubleshooting.
