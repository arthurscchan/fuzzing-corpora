# strongSwan Fuzzing Corpora
Corpora for fuzzing parts of the strongSwan code base

- **certs**: X.509 certificates, initially 1000 files, half of them in DER and half of them im PEM format (obtained from certificate-transparency.org)
- **crls**: X.509 CRLs, initially 190 files in DER format, four in PEM format, one empty and five HTML error pages (obtained from certificates from certificate-transparency.org)
- **ids**: Identification strings/blobs, initially 21 identities from the strongSwan unit tests
- **ike**: IKE protocol messages, initially 10 files covering IKEv2 with various exchange types, derived from the strongSwan unit tests
- **ocsp_req**: OCSP requests, initially 2 files in DER format derived from the strongSwan KVM regression tests
- **ocsp_rsp**: OCSP responses, initially 4 files in DER format derived from the strongSwan KVM regression tests
- **pa_tnc**: RFC 5792 PA-TNC messages, initially 18 messages derived from the strongSwan KVM regression tests
- **pb_tnc**: RFC 5793 PB-TNC batches, initially 6 batches derived from the strongSwan KVM regression tests
- **vici_cred**: Inputs for `fuzz_vici_cred`, initially 20 seeds covering all nine command handlers of the `vici_cred` plugin (clear-creds, flush-certs, load-cert, load-key, unload-key, get-keys, load-shared, unload-shared, get-shared). Each seed starts with a 1-byte command selector followed by command-specific selector bytes and a trailing data blob (e.g. an X.509 DER/PEM certificate for load-cert, a PEM private key for load-key, raw bytes for load-shared). A matching `vici_cred.dict` provides the command selector bytes, type/flag/owner strings and ASN.1/PEM tokens.
- **tls**: TLS messages (prefixed with 0x00 for server replies and 0x01 for client requests), initially 10 files derived from the strongSwan libtls unit tests

The `*-crash` directories contain input generated while fuzzing that caused crashes (or timeouts etc.).

The name of every file is the SHA-256 hash of its contents.
