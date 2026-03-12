# Networking Labs Index

This index is the source of truth for **lab ordering** and **naming conventions**.

## Lab naming + ordering standard
- **File naming**: `NN-short-kebab-title.md` (zero-padded, e.g. `08-wireless-network-analysis.md`)
- **Lab ID**: the `NN` prefix is the stable ordering (don’t renumber unless you intend to change the sequence)
- **Add new labs**: create the new `NN-*.md` file, then add a row in the table below

## Current labs (recommended sequence)

| Lab | Title | Track | Difficulty | Duration |
| --- | ----- | ----- | ---------- | -------- |
| 01 | [TCP/IP Fundamentals](01-tcp-ip-fundamentals.md) | Fundamentals | Beginner | 30–45m |
| 02 | [DNS Troubleshooting](02-dns-troubleshooting.md) | Troubleshooting | Intermediate | 45–60m |
| 03 | [IP Addressing & Subnetting](03-ip-addressing.md) | Fundamentals | Intermediate | 60–90m |
| 04 | [Local Network Diagnostics](04-local-network-diagnostics.md) | Troubleshooting | Advanced | 45–75m |
| 05 | [Network Security Fundamentals](05-network-security-fundamentals.md) | Security | Intermediate | 60–90m |
| 06 | [Firewall Configuration](06-firewall-configuration.md) | Security | Advanced | 45–60m |
| 07 | [Network Performance Monitoring](07-network-performance-monitoring.md) | Performance | Advanced | 60–75m |

## Upcoming labs (stubs)
- [Lab 8: Wireless Network Analysis](08-wireless-network-analysis.md)
- [Lab 9: VPN Configuration & Troubleshooting](09-vpn-configuration-troubleshooting.md)

## Lab progression (tracks)
- **Fundamentals**: 01 → 03
- **Troubleshooting**: 02 → 04
- **Security**: 05 → 06
- **Performance**: 07

## Templates
- **New lab template**: see `labs/_templates/lab-template.md`

## Assumptions / environment
Right now these labs are written primarily for **Windows built-in tools** (CMD/PowerShell). If you want, we can add Linux/macOS equivalents as optional sections per lab.
