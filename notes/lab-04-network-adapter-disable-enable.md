# Lab 04 — Network Adapter Disable/Enable Troubleshooting

## Objective

The objective of this lab was to practise troubleshooting a network connectivity issue caused by a disabled network adapter.

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
| NAT Adapter | Ethernet 2 |
| NAT Default Gateway | 10.0.3.2 |

## Tasks Completed

- Reviewed the Windows network adapters
- Disabled the NAT network adapter
- Checked IP configuration after disabling the adapter
- Tested external connectivity using `ping 8.8.8.8`
- Confirmed that internet connectivity failed while the NAT adapter was disabled
- Enabled the NAT adapter again
- Tested external connectivity after enabling the adapter
- Confirmed that internal DNS resolution still worked

## Commands Used

```cmd
ipconfig /all
ping 8.8.8.8
nslookup shirleylab.local
```

## Evidence Collected

- `18-network-adapters-before-disable.png`
- `19-nat-adapter-disabled.png`
- `20-ipconfig-after-nat-disabled.png`
- `21-ping-google-dns-failed-after-disable.png`
- `22-nat-adapter-enabled-again.png`
- `23-ping-google-dns-success-after-enable.png`
- `24-nslookup-domain-after-adapter-enable.png`

## Troubleshooting Notes

The Windows 10 client had two network adapters: one for the internal Active Directory lab network and one NAT adapter for internet access.

The NAT adapter was disabled to simulate a common connectivity issue. After disabling the adapter, external connectivity to `8.8.8.8` failed because the client no longer had access to the NAT route used for internet connectivity.

The NAT adapter was then enabled again. After re-enabling the adapter, external connectivity was restored and the client could successfully ping `8.8.8.8`.

Internal DNS resolution was also tested using `nslookup shirleylab.local` to confirm that the Active Directory lab network still worked.

## What I Learned

This lab helped me understand how a disabled network adapter can cause connectivity problems.

I learned how to check adapter status, disable and enable a network adapter, test internet connectivity, and confirm that internal DNS resolution still works after restoring the adapter.

This is a common troubleshooting step in IT Support and Service Desk roles when a user reports that they have lost network or internet access.
