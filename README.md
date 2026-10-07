# HTTPS Traffic Analysis & Request Interception with mitmproxy

## Overview

This project documents a hands-on **network security and traffic analysis lab** completed as part of CodePath's Intermediate Cybersecurity (CYB102) program.

The lab focused on analyzing encrypted HTTPS traffic using **Wireshark and mitmproxy**, configuring a local proxy environment, inspecting web requests, and modifying intercepted traffic within an authorized virtual lab environment.

The primary objective was to understand how encrypted web traffic appears from different network-analysis perspectives and how an authorized interception proxy can provide visibility into application-layer HTTPS requests.

## Objectives

The lab focused on:

- Capturing and analyzing encrypted HTTPS traffic with Wireshark.
- Installing and configuring mitmproxy.
- Running mitmproxy through Docker.
- Configuring Firefox to route web traffic through a local proxy.
- Installing and trusting the mitmproxy certificate within the lab browser.
- Comparing traffic visibility between Wireshark and mitmproxy.
- Inspecting HTTP and HTTPS requests.
- Examining request details and parameters.
- Intercepting requests before they reached their destination.
- Modifying an intercepted request before allowing it to continue.
- Understanding how proxy-based inspection differs from packet capture.

## HTTPS Traffic Analysis with Wireshark

The investigation began by using **Wireshark** to capture network traffic generated while visiting an HTTPS website.

This provided an opportunity to examine what information remains observable during encrypted communication while demonstrating the limitations of traditional packet analysis when application-layer content is protected by TLS encryption.

Wireshark provided visibility into the network communication, while the encrypted application-layer contents were not directly readable from the packet capture alone.

## Configuring mitmproxy

Next, **mitmproxy** was deployed through Docker and configured to listen on port `8080`.

```bash
sudo docker run --rm -it \
  -v ~/.mitmproxy:/home/mitmproxy/.mitmproxy \
  -p 8080:8080 mitmproxy/mitmproxy
```

Firefox was then configured to route web traffic through the local proxy.

Within the controlled lab environment, the appropriate mitmproxy certificate was installed and trusted by the browser. This allowed HTTPS requests routed through the proxy to be inspected and compared with the network traffic previously observed using Wireshark.

## Wireshark vs. mitmproxy

The lab demonstrated two different perspectives for analyzing network communication.

### Wireshark

Wireshark provided packet-level visibility into network communication and allowed traffic to be captured and analyzed as it traversed the network.

### mitmproxy

mitmproxy provided application-layer visibility into requests routed through the configured proxy.

Using both tools demonstrated how packet capture and proxy-based inspection can provide different forms of visibility during a network security investigation.

## Request Interception & Modification

The final portion of the lab focused on actively intercepting and modifying a request within the authorized environment.

A request was generated through the local proxy using `curl`:

```bash
curl --proxy http://127.0.0.1:8080 \
"http://wttr.in/Dunedin?0"
```

mitmproxy was used to intercept the request before it reached its destination.

The request path was then modified from:

```text
Dunedin
```

to:

```text
Innsbruck
```

before allowing the request to continue.

The resulting response reflected the modified request, demonstrating how an interception proxy can inspect and alter application-layer network communication before forwarding it to its destination.

## Traffic Analysis Workflow

The overall investigation followed this workflow:

**Capture Traffic → Analyze Encrypted Packets → Configure Proxy → Route Traffic → Inspect Requests → Intercept Traffic → Modify Request → Observe Response**

This workflow demonstrated the relationship between packet-level network analysis and application-layer proxy inspection.

## Tools & Technologies

- Wireshark
- mitmproxy
- Docker
- Linux / Ubuntu
- Firefox
- curl
- HTTP
- HTTPS
- TLS
- Proxy Servers
- Linux CLI

## Skills Demonstrated

- Network Traffic Analysis
- Packet Analysis
- HTTPS / TLS Analysis
- Proxy Configuration
- HTTP Request Analysis
- Traffic Inspection
- Request Interception
- Request Modification
- Network Security
- Linux Administration
- Network Troubleshooting

## Key Takeaways

This lab demonstrated the difference between **passively capturing encrypted network traffic** and inspecting application-layer requests through an authorized interception proxy.

Using Wireshark provided experience examining network packets and understanding what information remains visible when application-layer communication is encrypted.

Using mitmproxy demonstrated how a properly configured interception proxy within an authorized environment can provide additional visibility into web requests and allow those requests to be inspected and modified.

The project strengthened my understanding of **HTTPS, TLS, proxy servers, packet analysis, HTTP requests, and network traffic inspection** while providing hands-on experience with tools such as Wireshark and mitmproxy.

## Disclaimer

This project was completed in an **authorized educational lab environment** as part of CodePath's Intermediate Cybersecurity (CYB102) program. All network interception and request modification activities were performed within the designated lab environment for educational and cybersecurity training purposes.
