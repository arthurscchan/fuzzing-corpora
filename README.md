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
- **pkcs7**: PKCS#7/CMS containers in DER format, initially 5 hand-crafted samples covering SignedData (attached and detached), EnvelopedData (AES-256 and 3DES content encryption) and a cert-only PKCS#7 bag, signed/encrypted against the embedded RSA-2048 test certificate in `fuzz_pkcs7`
- **pkcs8**: PKCS#8 private keys in DER format, initially 4 samples covering an unencrypted key, PBES2 with AES-256-CBC, PBES2 with 3DES and legacy PBES1 with SHA1-3DES, all encrypted with passphrase `fuzz` matching `fuzz_pkcs8`
- **pkcs12**: PKCS#12 containers, initially 4 samples covering AES-256-CBC with SHA-256 MAC, legacy PBE-SHA1-3DES, a multi-certificate chain, and a bundle with friendlyName and CSP attribute, all encrypted with passphrase `fuzz` matching `fuzz_pkcs12`
- **tls**: TLS messages (prefixed with 0x00 for server replies and 0x01 for client requests), initially 10 files derived from the strongSwan libtls unit tests

The `*-crash` directories contain input generated while fuzzing that caused crashes (or timeouts etc.).

The name of every file is the SHA-256 hash of its contents.
