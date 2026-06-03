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
- **pubkey**: Public keys in four wire formats, initially 10 hand-crafted samples covering DER-encoded SubjectPublicKeyInfo (RSA-2048, EC P-256, EC P-384, Ed25519), SSH wire format (RSA, ECDSA-P256, Ed25519), DNSKEY records (RSA/SHA-256, ECDSA-P256/SHA-256) and a PGP v4 RSA public-key packet, matching the four `BUILD_BLOB_*` paths exercised by `fuzz_pubkey`
- **trusted_pubkey**: Bare public-key DERs (RSA-2048, EC P-256, EC P-384, Ed25519), initially 4 samples used as `CRED_CERTIFICATE / CERT_TRUSTED_PUBKEY / BUILD_BLOB` input for `fuzz_trusted_pubkey`
- **tls**: TLS messages (prefixed with 0x00 for server replies and 0x01 for client requests), initially 10 files derived from the strongSwan libtls unit tests

The `*-crash` directories contain input generated while fuzzing that caused crashes (or timeouts etc.).

The name of every file is the SHA-256 hash of its contents.
