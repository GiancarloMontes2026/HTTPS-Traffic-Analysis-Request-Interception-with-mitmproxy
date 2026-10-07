HTTPS Traffic Analysis & Request Interception with mitmproxy
Overview
This project documents a hands-on network security and traffic analysis lab completed as part of CodePath’s Intermediate Cybersecurity (CYB102) program. The lab focused on analyzing encrypted HTTPS traffic with Wireshark and mitmproxy, configuring a proxy environment, intercepting network requests, and modifying requests in a controlled virtual machine.
The primary objective was to understand how encrypted web traffic appears from different network-analysis perspectives and how an authorized interception proxy can provide additional visibility into HTTPS requests.     CYB 102 UNIT 4 LAB
Objectives
The lab focused on:
- Capturing and analyzing encrypted HTTPS traffic with Wireshark.
- Installing and configuring mitmproxy.
- Running mitmproxy through Docker.
- Configuring Firefox to route web traffic through a local proxy.
- Installing and trusting the mitmproxy certificate within the lab browser.
- Comparing traffic visibility between Wireshark and mitmproxy.
- Intercepting HTTP requests.
- Examining request details and parameters.
- Modifying an intercepted request before allowing it to continue.
- Understanding how proxy-based traffic inspection differs from packet capture.
HTTPS Traffic Analysis with Wireshark
The investigation began by using Wireshark to capture network traffic generated while visiting an HTTPS website.
This provided an opportunity to examine what information remains visible during encrypted communication and understand the limitations of traditional packet analysis when application-layer data is protected by encryption.     CYB 102 UNIT 4 LAB
Configuring mitmproxy
Next, mitmproxy was deployed through Docker and configured to listen on port 8080.
sudo docker run --rm -it \
-v ~/.mitmproxy:/home/mitmproxy/.mitmproxy \
-p 8080:8080 mitmproxy/mitmproxy

Firefox was configured to route traffic through the proxy, and the appropriate mitmproxy certificate was installed in the browser's trust store within the controlled lab environment.     CYB 102 UNIT 4 LAB
This allowed HTTPS requests to be inspected through the authorized interception proxy and compared with the network packets previously observed using Wireshark.     CYB 102 UNIT 4 LAB
Request Interception & Modification
The final portion of the lab focused on actively intercepting and modifying an HTTP request.
A request was generated through the local proxy using curl:
curl --proxy http://127.0.0.1:8080 \
"http://wttr.in/Dunedin?0"

mitmproxy was used to intercept the request before it reached its destination. The request path was then modified from Dunedin to Innsbruck before allowing the request to continue.
The resulting response reflected the modified request, demonstrating how an interception proxy can inspect and alter application-layer network communication.     CYB 102 UNIT 4 LAB
Tools & Technologies
Wireshark • mitmproxy • Docker • Linux/Ubuntu • Firefox • curl • HTTP • HTTPS • TLS • Proxy Servers • Linux CLI
Skills Demonstrated
Network Traffic Analysis • Packet Analysis • HTTPS/TLS Analysis • Proxy Configuration • HTTP Request Analysis • Traffic Interception • Request Manipulation • Network Security • Linux Administration • Blue Team Security
Key Takeaways
This lab demonstrated the difference between passively capturing encrypted network traffic and inspecting application-layer requests through an authorized proxy.
The overall workflow was:
Capture traffic → Analyze encrypted packets → Configure proxy → Route browser traffic → Inspect requests → Intercept traffic → Modify request → Observe response
The project strengthened my understanding of HTTPS, TLS, proxy servers, packet analysis, web requests, and network traffic inspection, while providing hands-on experience with industry-relevant tools such as Wireshark and mitmproxy.
Disclaimer
This project was completed in an authorized educational lab environment as part of CodePath's Intermediate Cybersecurity program. All network interception and request modification activities were performed within the designated lab environment for educational and cybersecurity training purposes.
