# Layer-by-Layer Breakdown of a Captured HTTP Request/Response

## 1. Frame (Physical layer representation)
- Shows the raw frame as captured on the wire — total frame size in bytes,
  capture timestamp, and encapsulation type (Ethernet).
- This is Wireshark's bookkeeping layer, not a real header on the wire, but
  it tells you exactly when the packet was seen and how big it is.

## 2. Ethernet II (Data Link layer)
- Contains the **source MAC address** (local machine) and **destination MAC
  address** (default gateway/router, not the actual remote server — MACs
  don't cross networks).
- Confirms that at this layer, communication is only ever "next hop," never
  end-to-end.

## 3. IPv4 (Network layer)
- Header length (usually 20 bytes) vs total packet length (header + payload).
- **TTL (Time To Live)**: max number of hops before the packet is dropped —
  useful for traceroute-style reasoning and for spotting suspicious hop
  counts in unusual traffic.
- **Protocol field**: identifies the next layer up (6 = TCP, 17 = UDP).
- Source and destination IP addresses — the actual end-to-end addressing.

## 4. TCP (Transport layer)
- Source port (ephemeral, e.g. 50133) and destination port (80 for HTTP) —
  ports are what let a single IP host multiple simultaneous services/sessions.
- **Sequence number**: position of the first byte of this segment in the
  overall byte stream.
- **Acknowledgement number**: confirms receipt of previously sent bytes.
- **Flags** (e.g. PSH, ACK): PSH tells the receiving stack to push buffered
  data up to the application immediately; ACK acknowledges data received.
- **Window size**: how many bytes the sender is willing to receive before
  requiring an ACK (flow control).
- **Checksum**: integrity check for the segment.
- **Urgent pointer**: 0 when no urgent/out-of-band data is present.

## 5. HTTP (Application layer)

### Request
- `GET /path HTTP/1.1` — method, requested resource, protocol version.
- `Host:` — which virtual host/domain is being asked for (critical on shared
  hosting/CDNs where one IP serves many domains).
- `Connection: keep-alive` — reuse the same TCP connection for further
  requests instead of opening a new one each time.
- `Accept-Encoding: gzip, deflate` — client says it can handle compressed
  responses (smaller payloads).
- `Accept-Language` — client's preferred language.
- `Referer` — the page that linked to this request; can leak internal URLs
  or search terms if not handled carefully by developers.

### Response
- `HTTP/1.1 200 OK` — status line; 200 means success.
- `Content-Type: text/html; charset=UTF-8` — tells the client how to
  interpret the payload.
- `Transfer-Encoding: chunked` — body sent in segments rather than one fixed
  length block.
- `Vary: Accept-Encoding` — tells caches to store separate versions based on
  what encoding was negotiated.
- `X-Powered-By: PHP` — reveals backend technology. From a security
  standpoint this is a small piece of recon information handed out for free;
  well-hardened servers often suppress this.
- `X-Frame-Options` — mitigates clickjacking by controlling whether the page
  can be embedded in an iframe.
- `X-XSS-Protection` — legacy browser-side XSS filter toggle (mostly
  deprecated in modern browsers, but still seen in the wild).

## Security-relevant observations
- Everything above — headers, cookies (if present), request bodies — is
  fully visible because the site used plain HTTP. The exact same capture
  against an HTTPS site would show only encrypted TCP payload at the
  application layer, with the request/response contents hidden. This is the
  practical reason "HTTP vs HTTPS" matters far beyond a padlock icon.
- The presence/absence of security headers (`X-Frame-Options`,
  `X-XSS-Protection`, and in modern terms `Content-Security-Policy`,
  `Strict-Transport-Security`) is something worth checking on any site during
  a basic security review — it's visible directly in a capture like this.