# Network Traffic Investigation Report

## 1. Executive Summary

This report documents a basic network traffic investigation conducted using Wireshark on Windows. The investigation focused on DNS resolution, TCP connection establishment, and TLS traffic generated while browsing Wikipedia.

The objective was to develop practical packet-analysis skills relevant to entry-level IT support and Security Operations Centre (SOC) operations.

The observed traffic was consistent with the browsing activity generated during the exercise. This investigation was limited in scope and should not be treated as a comprehensive security assessment.

## 2. Investigation Objectives

The investigation aimed to:

- Examine DNS queries and responses.
- Identify TCP connection establishment using packet flags.
- Inspect TLS Client Hello and Server Hello messages.
- Identify TLS Application Data records.
- Practise using Wireshark display filters.
- Document observations and communicate findings clearly.

## 3. Environment and Tools

| Item | Description |
|---|---|
| Operating system | Windows |
| Analysis tool | Wireshark |
| Activity | Normal web browsing |
| Traffic examined | DNS, TCP and TLS |
| Target domain | www.wikipedia.org |
| Destination port | TCP 443 |

The capture was generated during a web-browsing session. The analysis was performed on the resulting packet capture in Wireshark.

## 4. Methodology

The investigation followed these steps:

1. Opened Wireshark and selected the active network interface.
2. Generated network traffic by browsing Wikipedia.
3. Captured packets and inspected relevant protocol exchanges.
4. Applied display filters to isolate DNS, TCP and TLS traffic.
5. Examined packet details and recorded observations.
6. Captured screenshots as supporting evidence.

## 5. Findings and Analysis

### 5.1 DNS Query and Response Analysis

**Display filter:**

`dns`

**Observation:**

The capture contained DNS queries associated with Wikipedia browsing. The inspected DNS response included a canonical name (CNAME) record and an IPv4 address record.

**Analysis:**

DNS translates domain names into information that clients can use to locate network services. Examining DNS packets helps an analyst understand which names a device attempted to resolve and whether responses were received.

**Evidence:** `screenshots/01-dns-analysis.png`

### 5.2 TCP Three-Way Handshake

**Display filter:**

`ip.addr == 185.15.58.224 && tcp.port == 443`

**Observation:**

The inspected packet sequence showed the following TCP flags:

1. SYN — the client initiated a connection.
2. SYN-ACK — the other endpoint responded.
3. ACK — the client acknowledged the response.

**Analysis:**

This sequence is consistent with a completed TCP three-way handshake. The handshake establishes the TCP connection before application data is exchanged.

**Evidence:** `screenshots/02-tcp-handshake.png`

### 5.3 TLS Client Hello

**Display filter:**

`ip.addr == 185.15.58.224 && tls`

**Observation:**

A TLS Client Hello message was visible. The packet details included the Server Name Indication (SNI) value `www.wikipedia.org`.

**Analysis:**

The Client Hello begins the TLS negotiation and carries information used to establish secure communication. When visible, SNI can help an analyst associate a TLS connection with a requested hostname.

**Evidence:** `screenshots/03-tls-client-hello.png`

### 5.4 TLS Server Hello

**Display filter:**

`ip.addr == 185.15.58.224 && tls`

**Observation:**

A TLS Server Hello message was present in the inspected traffic.

**Analysis:**

The Server Hello is part of the TLS negotiation in which the server communicates parameters for the connection. Its presence provides evidence of TLS handshake activity, although a single packet alone does not establish that every stage of the negotiation succeeded.

**Evidence:** `screenshots/04-tls-server-hello.png`

### 5.5 TLS Application Data

**Display filter:**

`ip.addr == 185.15.58.224 && tls.app_data`

**Observation:**

TLS Application Data records were visible in the capture.

**Analysis:**

TLS Application Data carries application-layer information within the TLS connection. Its contents are generally encrypted, so the packet listing alone does not reveal the underlying web content.

**Evidence:** `screenshots/05-tls-application-data.png`

## 6. Security Assessment

The inspected packets were consistent with ordinary web-browsing activity during this exercise.

No malicious activity was established from the limited observations documented here. However, this does not prove that the device or network was free of threats.

A more comprehensive investigation would require a wider capture, additional protocol analysis, and relevant contextual information.

## 7. Limitations

- The investigation covered a short, manually generated traffic capture.
- The analysis focused on a single browsing activity and selected packets.
- Encrypted TLS application contents were not decrypted or inspected.
- No comprehensive threat detection, endpoint investigation, or malware analysis was performed.
- The destination IP address alone cannot establish the identity or trustworthiness of a remote service.

## 8. Recommended Next Steps for a SOC Analyst

If investigating potentially suspicious traffic in a real SOC environment, I would:

1. Review the surrounding packets and connection timeline.
2. Correlate DNS queries with destination IP addresses and connection activity.
3. Check destination reputation using approved threat-intelligence sources.
4. Investigate unusual ports, repeated failed connections, and unexpected outbound traffic.
5. Correlate packet evidence with endpoint logs and other available telemetry before drawing conclusions.

These steps would help determine whether further investigation is warranted.

## 9. Skills Practised

- Network packet capture and inspection
- DNS query and response analysis
- TCP handshake analysis
- TLS handshake inspection
- Wireshark display-filter usage
- Technical documentation
- Evidence-based reporting

## 10. Conclusion

This project provided practical experience analysing common network protocols using Wireshark. It demonstrated how to isolate DNS traffic, examine TCP connection establishment, inspect TLS negotiation messages, and identify encrypted application data.

The exercise strengthened foundational network-analysis skills that can support further learning in defensive cybersecurity and SOC operations.

## Disclaimer

This project was conducted for educational purposes using traffic generated during normal web browsing. The findings apply only to the traffic examined in this exercise.
