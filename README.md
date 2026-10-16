## Network Traffic Investigation with Wireshark

**Project Overview**

This project demonstrates a beginner-level network traffic investigation using Wireshark. The goal was to observe and analyse DNS queries, TCP connections, and TLS traffic generated while browsing Wikipedia.

## Objectives

- Identify DNS queries and responses.
- Examine the TCP three-way handshake.
- Inspect TLS handshake messages.
- Identify TLS Application Data packets.
- Practise Wireshark display filters and packet inspection.

## Tools Used

- Wireshark
- Windows
- Wireshark display filters

**Investigation Process**

## 1. DNS Analysis
**Filter used:** dns

I examined DNS queries and responses generated during web browsing. The capture included a query for "www.wikipedia.org" and a DNS response containing a CNAME record and an IPv4 address.

**Finding:** DNS traffic showed how a domain name was resolved during the browsing session.


## 2. TCP Three-Way Handshake
**Filter used:**  ip.addr == 185.15.58.224 && tcp.port == 443


I inspected TCP packets associated with the destination on port 443 and identified the SYN, SYN-ACK, and ACK sequence.

**Finding:** The observed packet sequence was consistent with a completed TCP three-way handshake.


## 3. TLS Client Hello
**Filter used:**  ip.addr == 185.15.58.224 && tls


I inspected the TLS Client Hello message and located the Server Name Indication (SNI), where available.

**Finding:** The Client Hello provided information about the requested server name during TLS negotiation.


## 4. TLS Server Hello

I inspected the TLS Server Hello message to observe the server's response during the TLS handshake.

**Finding:** The capture contained a Server Hello message associated with the observed connection.


## 5. TLS Application Data
**Filter used:**  ip.addr == 185.15.58.224 && tls.app_data

I filtered for TLS Application Data packets to distinguish application traffic carried within the TLS connection.

**Finding:** TLS Application Data records were visible in the capture. Their encrypted contents were not interpreted.

## Key Learnings

- How DNS queries and responses appear in packet captures.
- How to identify TCP handshake packets.
- How to inspect TLS Client Hello and Server Hello messages.
- How to apply Wireshark display filters to investigate network traffic.
- Why encrypted application data cannot normally be read directly from a packet capture.

## Conclusion

This exercise provided practical experience inspecting network traffic with Wireshark. It helped build foundational skills in network protocol analysis relevant to entry-level IT support and Security Operations Centre (SOC) work.

The observations were consistent with the web-browsing activity generated during the exercise. This was a limited, controlled learning exercise and not a comprehensive security assessment.

## Evidence

Screenshots documenting the investigation are available in the `screenshots/` directory.

## Disclaimer

This project was conducted for educational purposes using traffic generated during normal web browsing.
