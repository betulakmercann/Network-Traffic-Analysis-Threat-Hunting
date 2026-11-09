## WIRESHARK ANALYSIS

In this study, I used **Wireshark** to examine raw network traffic files (`.pcap` / `.pcapng`).

**Objectives:**

- To gain an in-depth understanding of TCP connection mechanisms (3-Way Handshake).
- To analyze data transmitted over unencrypted web (HTTP) traffic.

## 1. TCP Traffic and Connection Establishment Analysis

- **Analyzed File:** `200722_win_scale_examples_anon.pcapng`
- **Applied Filter:** `tcp`

### Findings and Observations

1. **IP Structure:** I observed two-way communication between the source IP (`192.168.200.135`) and the destination IP (`192.168.200.21`).

2. **Port Information:** I identified the client's source port as `6711` and the server's destination port as `2000`.

3. **3-Way Handshake (TCP Connection Establishment):** I examined the first three packets in the packet list and verified the connection establishment process:
   - **Packet 1:** `[SYN]` (A connection request was sent.)
   - **Packet 2:** `[SYN, ACK]` (The request was accepted and a response was sent.)
   - **Packet 3:** `[ACK]` (The connection was acknowledged and established.)

4. **Stream Analysis (Follow TCP Stream):** When I followed the TCP stream associated with the connection, I captured the `"hello"` message transmitted between the devices as unencrypted plain text.

## 2. HTTP Web Traffic and Content Analysis

- **Analyzed File:** `http.cap`
- **Applied Filter:** `http`

### Findings and Observations

1. **Request Details:** I identified that the client with the IP address `145.254.160.237` sent a `GET` request to the web server at `65.208.228.223`, requesting the `/download.html` page.

2. **User-Agent and Browser Information:** By examining the client's header information, I analyzed the browser signature: `Mozilla/5.0 (Windows; U; Windows NT 5.1...)`.

3. **Server Response:** I observed that the server returned an `HTTP/1.1 200 OK` response, with a content length of `18070` bytes.

4. **Stream Analysis (Follow HTTP Stream):** By following the HTTP stream, I observed that the transmitted data was unencrypted (plaintext):
   - HTML code, `<body>` tags, and page image URLs were clearly readable.
   - I also identified an advertising/analytics request to a third-party service, `pagead2.googlesyndication.com`, within the captured traffic.

## Skills and Knowledge Gained

The technical skills I developed during this first stage include:

- [x] **Wireshark Interface:** Understanding the layered structure of the Packet List, Packet Details, and Packet Bytes (Hex) panels.
- [x] **Display Filters:** Using `tcp` and `http` filters to quickly isolate relevant data from complex network traffic.
- [x] **Stream Tracking:** Using `Follow Stream` to examine the communication between two devices as a complete conversation.
- [x] **Security Awareness:** Observing the risks of unencrypted protocols (HTTP, Telnet) through real network traffic analysis.
