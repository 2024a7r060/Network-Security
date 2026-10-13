Aim: To use Wireshark to observe and dissect the TLS handshake process during HTTPS communication.
Theory
TLS (Transport Layer Security): TLS is a cryptographic protocol that provides confidentiality, integrity, and authentication for communication over a network.
HTTPS (Hypertext Transfer Protocol Secure): HTTPS is the secure version of HTTP that uses TLS to protect communication between a web browser and a web server.
TLS Handshake: It is the process through which a client and server negotiate security parameters, establish shared cryptographic keys, and authenticate the server before secure communication begins.
TLS Key Logging: It is a mechanism for saving session secrets so that Wireshark can decrypt the corresponding captured TLS traffic for analysis.
Methodology
1. Capture HTTPS Traffic: Wireshark was opened and the active network interface was selected. HTTPS traffic was captured using the filter tcp.port == 443 while accessing https://www.wireshark.org. The capture was saved in .pcapng format.
2. Analyse Client Hello Message: The display filter tls.handshake.type == 1 was applied to locate the Client Hello packets. The TLS version, supported cipher suites, server name, and key-share information were examined.
3. Analyse Server Hello Message: The filter tls.handshake.type == 2 was applied to inspect the Server Hello packets. The negotiated TLS version, selected cipher suite, and key-share information were observed.
4. Configure TLS Key Logging: The browser was configured to save TLS session secrets in a key log file. Wireshark was then configured to use this file to decrypt the corresponding captured TLS session.
5. Inspect the Decrypted Handshake: A fresh HTTPS session was captured, and the TLS handshake messages were examined. Messages such as Encrypted Extensions, Certificate, Certificate Verify, and Finished were identified where applicable.
6. Inspect the Server Certificate: The certificate message was expanded to examine the certificate's subject, issuer, validity period, Subject Alternative Name (SAN), public-key information, and signature algorithm.
7. Extend the Handshake Analysis: The captured TLS sessions were compared to identify differences in handshake messages and certificate information. The analysis helped in understanding the negotiation process and identifying HTTPS traffic.
Visualisation
Start → Capture HTTPS Traffic using Wireshark → Identify Client Hello and Server Hello → Configure TLS Key Logging and Decrypt the Session → Inspect Handshake Messages and Server Certificate → Record Observations → End
Results
- The Client Hello message showed support for TLS 1.2 and TLS 1.3, along with the offered cipher suites and key-share information, where applicable.
- The Server Hello message indicated the negotiated TLS version and selected cipher suite.
- The decrypted handshake displayed messages such as Encrypted Extensions, Certificate, Certificate Verify, and Finished, depending on the TLS version and session.
- Certificate inspection revealed the subject, issuer, validity dates, SAN, and public-key information.
- The captured traffic provided evidence of TLS negotiation, server certificate information, and the establishment of a secure HTTPS session.
- The captured session and screenshots could be used to demonstrate the TLS handshake analysis.
Discussion
The Client Hello and Server Hello messages demonstrated how the client and server negotiate TLS security parameters. TLS key logging enabled the inspection of handshake messages that would otherwise remain encrypted. Certificate analysis provided information about the server's identity, certificate validity, and public key. The experiment demonstrated how TLS supports authentication and encrypted HTTPS communication.
Improvements
The basic packet capture was extended by examining multiple TLS handshake sessions and inspecting their negotiated security parameters and certificate information. Comparing different sessions provided a better understanding of TLS negotiation and differences in server security configurations.

