# DNS (Domain Name System)

## What is DNS?

DNS translates human-readable domain names into IP addresses.

Example:

google.com
↓
142.250.193.78

## Why DNS Matters in Cybersecurity

- DNS spoofing
- DNS tunneling
- Malware communication
- Reconnaissance

## Common DNS Record Types

| Record | Purpose |
|----------|----------|
| A | IPv4 Address |
| AAAA | IPv6 Address |
| MX | Mail Server |
| CNAME | Alias |

## Useful Commands

```bash
nslookup google.com
dig google.com