# strongSwan Fuzzing Corpora
Corpora for fuzzing parts of the strongSwan code base

- **certs**: X.509 certificates, initially 1000 files, half of them in DER and half of them im PEM format (obtained from certificate-transparency.org)
- **crls**: X.509 CRLs, initially 190 files in DER format, four in PEM format, one empty and five HTML error pages (obtained from certificates from certificate-transparency.org)
- **eap**: RFC 3748 EAP frames, initially 35 hand-crafted seeds covering EAP-Identity, EAP-Notification, EAP-Nak (single + extended desired-type list), EAP-MD5 (Type 4) challenge/response with length edge cases, EAP-MSCHAPv2 (Type 26) all five OpCodes (Challenge / Response / Success / Failure / Change-Password), EAP-OTP, EAP-GTC, EAP-Success / EAP-Failure code-only frames, EAP-Expanded (Type 254) with IETF and Microsoft vendor IDs, and malformed-length edge cases
- **ids**: Identification strings/blobs, initially 21 identities from the strongSwan unit tests
- **ike**: IKE protocol messages, initially 10 files covering IKEv2 with various exchange types, derived from the strongSwan unit tests
- **ocsp_req**: OCSP requests, initially 2 files in DER format derived from the strongSwan KVM regression tests
- **ocsp_rsp**: OCSP responses, initially 4 files in DER format derived from the strongSwan KVM regression tests
- **pa_tnc**: RFC 5792 PA-TNC messages, initially 18 messages derived from the strongSwan KVM regression tests
- **pb_tnc**: RFC 5793 PB-TNC batches, initially 6 batches derived from the strongSwan KVM regression tests
- **tls**: TLS messages (prefixed with 0x00 for server replies and 0x01 for client requests), initially 10 files derived from the strongSwan libtls unit tests

The `*-crash` directories contain input generated while fuzzing that caused crashes (or timeouts etc.).

The name of every file is the SHA-256 hash of its contents.
