# Simulated HTTP, SMTP & POP3 Traffic — Cisco Packet Tracer

## Goal
Build understanding of how application-layer protocols actually behave on
the wire — specifically HTTP (web browsing), SMTP (sending mail), and POP3
(retrieving mail) — using a simulated network so the full request/response
event sequence is visible and inspectable, without background noise.

## What I did
- Set up a simple client–server topology in Packet Tracer.
- **HTTP**: requested a web page from a client PC, captured the DNS lookup +
  HTTP request/response exchange, and inspected the PDU details at each
  layer for both the request and response packets.
- **SMTP**: composed and sent an email from a client, filtered the event list
  down to DNS/SMTP/POP3 only, and inspected the DNS lookup for the mail
  server plus the SMTP request/response exchange.
- **POP3**: reset the simulation and had a client retrieve mail, inspecting
  the DNS lookup and POP3 request/response exchange the same way.

## Why this matters for security
- HTTP, SMTP, and POP3 are all **plaintext-by-default** protocols. Watching
  them work packet-by-packet makes it obvious why credential sniffing on
  POP3/SMTP (without STARTTLS) and session/data exposure on HTTP are
  real, practical attack surfaces — not abstract warnings.
- Understanding that mail never goes directly sender → receiver, but instead
  sender → sender's mail server → receiver's mail server → receiver, is
  the foundation for understanding **email spoofing, SPF/DKIM/DMARC, and
  open relay abuse** later on.
- DNS resolution happening before every one of these exchanges is a reminder
  of how much of the internet depends on DNS integrity — which is exactly
  why DNS spoofing/poisoning and DNS-based exfiltration/C2 are such common
  attack techniques.

See `notes.md` for the specific packet-level answers and protocol
explanations.