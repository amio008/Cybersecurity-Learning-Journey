Protocol Flow Notes — HTTP, SMTP, POP3

## Background: how these protocols relate

**HTTP (web browsing)**
Client ---- 1. HTTP Request ----> Server
Client <--- 2. HTTP Response ---- Server
A single request/response pair between a browser (client) and a web server.

**Email (SMTP to send, POP3 to receive)**
Mail never travels directly between sender and receiver — it always passes
through at least one server on each side:
Sender --SMTP--> Sender's mail server --SMTP--> Receiver's mail server --POP3--> Receiver
(sender-initiated)         (server-initiated)              (receiver-initiated)
SMTP is used for both hops on the "sending" side (push). POP3 is only used
on the very last hop, when the receiver actively pulls mail down from their
own mail server.

**DNS**
Before any of the above can happen, the client needs the IP address of the
target server (web server or mail server). DNS is the lookup step that
converts a human-readable name into that IP address — it runs before HTTP,
before SMTP, and before POP3 in every one of these exchanges.

---

## HTTP Task

**Packet 1 — What kind of HTTP packet is this?**
HTTP Request packet. Inspecting the inbound PDU details shows a `GET`
request with headers like `Accept-Language: en-us` and `Accept: */*` — this
confirms the client is asking the server for a resource (an HTTP GET
request).

**Packet 2 — What kind of HTTP packet is this?**
HTTP Response packet. The inbound PDU details show `Connection: close` and
`Content-Length: 151`, meaning the web server is sending back the requested
data after processing the client's GET request. The source/destination port
pairing (server port 80 as source) also confirms this is the response
direction, not the request.

---

## SMTP Task

**DNS packet purpose:**
This DNS query resolves the domain name of the mail server to its IP
address, so the client knows where to actually send the outgoing SMTP
traffic.

**SMTP request/response exchange:**
The client sends an SMTP packet to its mail server to initiate the transfer
of an outgoing email. The mail server replies with its own SMTP packet to
acknowledge the connection and confirm it's ready to accept/process the
message — establishing the send process from both ends before the actual
mail content is transferred.

---

## POP3 Task

**DNS packet purpose:**
Same role as in the SMTP case — this DNS query resolves the mail server's
domain name to an IP address so the client (now acting as a receiver) knows
where to connect to check for new mail.

**POP3 request/response exchange:**
Unlike SMTP (which is server/sender-initiated push), POP3 is always
**client-initiated** — the receiving client actively connects to its mail
server and requests any waiting messages. The server responds with a POP3
packet either delivering the mail or confirming the mailbox status. This is
the "pull" step that finally gets the message from the receiver's mail
server into the receiver's inbox.

---

## Overall takeaway
The consistent pattern across all three protocols is: **DNS resolves the
destination first, then the application-layer protocol takes over** — and
the direction of "who initiates" differs meaningfully (HTTP: client always
initiates; SMTP: whoever is pushing mail initiates; POP3: only the receiver
initiates). This directionality matters a lot when reasoning about firewall
rules, mail server security, and where an attacker could realistically
intercept or inject traffic.