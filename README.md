# Networking Troubleshooting Lab

## Project Overview

This repository documents a hands-on networking troubleshooting lab using a Windows 10 client in an Active Directory lab environment.

The purpose of this project is to practise common IT Support and Service Desk network checks, including IP configuration review, ping testing, DNS testing, traceroute checks, IPv4 adapter review, default gateway troubleshooting, NAT adapter configuration, DNS cache commands, network adapter troubleshooting, DNS misconfiguration troubleshooting, and troubleshooting documentation. The lab also includes service desk-style tickets to document each issue from a support workflow perspective.

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
| Internal DNS Server | 192.168.10.10 |
| Public DNS Server Tested | 8.8.8.8 |
| NAT Adapter | Ethernet 2 |
| NAT Adapter IP Address | 10.0.3.15 |
| NAT Default Gateway | 10.0.3.2 |
| Incorrect DNS Server Tested | 8.8.8.8 |

## Completed Labs

| Lab | Topic | Status |
|---|---|---|
| Lab 01 | Basic Network Configuration & Connectivity Testing | Complete |
| Lab 02 | Fixing Internet Connectivity with NAT Adapter | Complete |
| Lab 03 | DNS Troubleshooting & DNS Cache Commands | Complete |
| Lab 04 | Network Adapter Disable/Enable Troubleshooting | Complete |
| Lab 05 | DNS Misconfiguration Troubleshooting | Complete |

## Lab Notes

- [Lab 01 — Basic Network Configuration & Connectivity Testing](notes/lab-01-basic-network-connectivity.md)
- [Lab 02 — Fixing Internet Connectivity with NAT Adapter](notes/lab-02-nat-adapter-internet-connectivity.md)
- [Lab 03 — DNS Troubleshooting & DNS Cache Commands](notes/lab-03-dns-troubleshooting.md)
- [Lab 04 — Network Adapter Disable/Enable Troubleshooting](notes/lab-04-network-adapter-disable-enable.md)
- [Lab 05 — DNS Misconfiguration Troubleshooting](notes/lab-05-dns-misconfiguration-troubleshooting.md)

## Troubleshooting Scenarios

- [Scenario 01 — No Default Gateway Configured](troubleshooting-scenarios/scenario-01-no-default-gateway.md)
- [Scenario 02 — Fixing Internet Connectivity with NAT Adapter](troubleshooting-scenarios/scenario-02-fixing-internet-connectivity-with-nat.md)
- [Scenario 03 — Public DNS Cannot Resolve Private Active Directory Domain](troubleshooting-scenarios/scenario-03-public-dns-cannot-resolve-private-domain.md)
- [Scenario 04 — Disabled NAT Adapter Causing No Internet Access](troubleshooting-scenarios/scenario-04-disabled-nat-adapter-no-internet.md)
- [Scenario 05 — Wrong DNS Server Causing Internal Domain Resolution Failure](troubleshooting-scenarios/scenario-05-wrong-dns-server-internal-domain-failure.md)
  
## Service Desk Tickets

- [Ticket 01 — No Default Gateway Configured](tickets/ticket-01-no-default-gateway.md)
- [Ticket 02 — Internet Connectivity Restored with NAT Adapter](tickets/ticket-02-nat-adapter-internet-fix.md)
- [Ticket 03 — Public DNS Cannot Resolve Private Domain](tickets/ticket-03-public-dns-private-domain.md)
- [Ticket 04 — Disabled NAT Adapter Causing No Internet Access](tickets/ticket-04-disabled-nat-adapter.md)
- [Ticket 05 — Wrong DNS Server Causing Internal Domain Resolution Failure](tickets/ticket-05-wrong-dns-server.md)

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

## Lab 03: DNS Troubleshooting & DNS Cache Commands

### Public DNS Cannot Resolve Private Domain

Tested the private Active Directory domain using Google public DNS. The lookup failed because public DNS does not hold records for the internal domain.

![Public DNS Cannot Resolve Private Domain](screenshots/12-nslookup-public-dns-failed.png)

### Domain Controller DNS Success

Tested the private Active Directory domain using the internal domain controller DNS server. The lookup succeeded.

![Domain Controller DNS Success](screenshots/13-nslookup-domain-controller-dns-success.png)

### Ping Domain Name

Pinged `shirleylab.local` to test domain name resolution and connectivity.

![Ping Domain Name](screenshots/14-ping-domain-name.png)

### Display DNS Cache

Displayed the Windows DNS resolver cache using `ipconfig /displaydns`.

![Display DNS Cache](screenshots/15-display-dns-cache.png)

### Flush DNS Cache

Cleared the Windows DNS resolver cache using `ipconfig /flushdns`.

![Flush DNS Cache](screenshots/16-flush-dns-cache.png)

### DNS Lookup After Cache Flush

Tested DNS resolution again after clearing the DNS cache.

![DNS Lookup After Cache Flush](screenshots/17-nslookup-after-dns-flush.png)

## Lab 04: Network Adapter Disable/Enable Troubleshooting

### Network Adapters Before Disable

Reviewed the Windows network adapters before making any changes.

![Network Adapters Before Disable](screenshots/18-network-adapters-before-disable.png)

### NAT Adapter Disabled

Disabled the NAT adapter to simulate a loss of internet connectivity.

![NAT Adapter Disabled](screenshots/19-nat-adapter-disabled.png)

### IP Configuration After NAT Disabled

Checked `ipconfig /all` after disabling the NAT adapter.

![IP Configuration After NAT Disabled](screenshots/20-ipconfig-after-nat-disabled.png)

### Ping Google DNS Failed After Disable

Tested external connectivity using `ping 8.8.8.8`. The test failed while the NAT adapter was disabled.

![Ping Google DNS Failed After Disable](screenshots/21-ping-google-dns-failed-after-disable.png)

### NAT Adapter Enabled Again

Enabled the NAT adapter again through Windows Network Connections.

![NAT Adapter Enabled Again](screenshots/22-nat-adapter-enabled-again.png)

### Ping Google DNS Success After Enable

Tested external connectivity again. The ping test succeeded after the NAT adapter was enabled.

![Ping Google DNS Success After Enable](screenshots/23-ping-google-dns-success-after-enable.png)

### DNS Lookup After Adapter Enable

Tested internal Active Directory DNS resolution after enabling the adapter again.

![DNS Lookup After Adapter Enable](screenshots/24-nslookup-domain-after-adapter-enable.png)

## Lab 05: DNS Misconfiguration Troubleshooting

### Correct DNS Before Change

Verified that the client was correctly configured to use the domain controller as its DNS server.

![Correct DNS Before Change](screenshots/25-correct-dns-before-change.png)

### Wrong DNS Configured

Changed the preferred DNS server from `192.168.10.10` to Google's public DNS (`8.8.8.8`) to simulate a DNS configuration issue.

![Wrong DNS Configured](screenshots/26-wrong-dns-configured.png)

### Internet Connectivity Still Works

Confirmed that the client could still reach external IP addresses even though the DNS server was incorrect.

![Ping Google DNS Success With Wrong DNS](screenshots/27-ping-google-dns-success-with-wrong-dns.png)

### Internal Domain Resolution Failed

Confirmed that `shirleylab.local` could not be resolved while using the wrong DNS server.

![NSLookup Domain Failed](screenshots/28-nslookup-domain-failed-wrong-dns.png)

### DNS Restored

Changed the preferred DNS server back to the domain controller.

![DNS Restored](screenshots/29-dns-restored-to-domain-controller.png)

### DNS Cache Flushed

Cleared the DNS resolver cache.

![Flush DNS Cache](screenshots/30-flush-dns-after-restore.png)

### Internal Domain Resolution Restored

Confirmed that the Active Directory domain could once again be resolved after restoring the correct DNS server.

![NSLookup Domain Success](screenshots/31-nslookup-domain-success-after-dns-restore.png)

## Commands Used

```cmd
ipconfig /all
ping 192.168.10.10
ping 8.8.8.8
nslookup shirleylab.local
nslookup shirleylab.local 8.8.8.8
nslookup shirleylab.local 192.168.10.10
ping shirleylab.local
tracert 8.8.8.8
ipconfig /displaydns
ipconfig /flushdns
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
- Windows Network Connections
- Network adapter disable/enable troubleshooting
- Internal vs external network testing
- Public DNS vs internal DNS
- Active Directory DNS checks
- DNS cache review
- DNS cache flushing
- DNS misconfiguration troubleshooting
- DNS server configuration
- DNS cache management
- Service desk documentation
- Technical documentation
- Ticket documentation
- Incident documentation
- Root cause analysis

## What I Learned

This lab helped me practise basic networking checks used in IT Support and Service Desk roles.

In Lab 01, I learned how to check IP configuration, test connectivity to an internal domain controller, test DNS resolution, and identify why a client could reach internal resources but not external internet addresses.

The main issue identified was that the Windows client had no default gateway configured. This explained why communication inside the lab network worked, but external connectivity to `8.8.8.8` failed.

In Lab 02, I added a second VirtualBox network adapter and configured it as NAT. This allowed the Windows client to keep its internal Active Directory lab connection while also gaining internet access through a separate NAT adapter.

In Lab 03, I tested the difference between public DNS and internal Active Directory DNS. Public DNS could not resolve `shirleylab.local`, but the internal domain controller DNS server could resolve it successfully.

I also practised displaying and flushing the DNS resolver cache using `ipconfig /displaydns` and `ipconfig /flushdns`.

In Lab 04, I simulated a connectivity issue by disabling the NAT adapter. This showed how a disabled adapter can stop internet access and how enabling the adapter again restores connectivity.

In Lab 05, I learned that network connectivity and DNS resolution are two different things. A computer can successfully reach external IP addresses while still failing to resolve internal domain names if the wrong DNS server is configured. Restoring the correct Active Directory DNS server and flushing the DNS cache restored normal domain name resolution.

This helped me understand the difference between internal lab networking, DNS, default gateways, NAT, DNS cache, network adapter status, DNS server configuration, and internet connectivity troubleshooting.
