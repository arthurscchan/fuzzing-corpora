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

The `*-crash` directories contain input generated while fuzzing that caused crashes (or timeouts etc.).

The name of every file is the SHA-256 hash of its contents.

## Dictionaries

Each `<name>.dict` is a libFuzzer/OSS-Fuzz dictionary that supplies magic byte sequences and structural tokens (ASN.1 tags, OIDs, payload type codes, attribute IDs, etc.) so the mutator can land on otherwise hard-to-reach code paths. The OSS-Fuzz `build.sh` copies `<name>.dict` to `$OUT/fuzz_<name>{,_def,_cus}.dict` next to the matching binary, where libFuzzer auto-loads it at runtime.

The format follows libFuzzer's strict dictionary syntax: one quoted token per line, C-style escapes, no comments and no blank lines.

- **certs.dict**: ASN.1 universal tags, X.509 extension OIDs (subjectAltName, basicConstraints, keyUsage, CRL distribution points, ...), RDN attribute OIDs, signature and key algorithm OIDs, PEM markers
- **crls.dict**: ASN.1 tags, CRL extension OIDs (CRLNumber, ReasonCode, IssuingDistributionPoint, FreshestCRL, ...) and signature algorithm OIDs
- **ike.dict**: IKEv1 / IKEv2 version + exchange-type byte pairs, payload type codes, transform type and algorithm IDs, common notify message types
- **ocsp_req.dict**: ASN.1 tags and OCSP request OIDs (id-pkix-ocsp, id-pkix-ocsp-nonce, id-sha256)
- **ocsp_rsp.dict**: ASN.1 tags, OCSP response status enum, responseType OIDs, signature algorithm OIDs
- **pa_tnc.dict**: PA-TNC version byte, Private Enterprise Numbers (IETF, TCG, ITA) and IETF PA-TNC attribute type IDs
- **pb_tnc.dict**: PB-TNC batch types (CDATA, SDATA, RESULT, CRETRY, SRETRY, CLOSE), vendor IDs and message type IDs
- **pkcs7.dict**: ASN.1 tags, PKCS#7 contentType OIDs (data, signedData, envelopedData, encryptedData, ...), signed attribute OIDs and content-encryption algorithm OIDs
- **pkcs8.dict**: ASN.1 tags, PKCS#5/#8 algorithm OIDs (PBES2, PBKDF2, AES-CBC, 3DES, PBE-SHA1-3DES, ...) and key algorithm OIDs
- **pkcs12.dict**: ASN.1 tags, PKCS#12 SafeBag OIDs (keyBag, pkcs8ShroudedKeyBag, certBag, secretBag, safeContentsBag, ...), friendlyName / localKeyID OIDs and content-encryption OIDs
- **pubkey.dict**: ASN.1 tags, key algorithm OIDs (RSA, ECDSA, Ed25519 / Ed448, X25519 / X448), DNSKEY flag/protocol/algorithm bytes, SSH wire-format key prefixes (ssh-rsa, ssh-ed25519, ecdsa-sha2-nistp256, ...), PGP packet tags
- **radius.dict**: RADIUS code bytes (Access-Request / Accept / Reject / Challenge / Accounting-Request / Status-Server / ...), common attribute type+length pairs and Vendor-IDs (Cisco, Microsoft, 3GPP, Funk)
- **simaka.dict**: EAP-SIM and EAP-AKA subtype codes and AT_* attribute type codes (AT_RAND, AT_AUTN, AT_RES, AT_MAC, AT_ENCR_DATA, AT_IV, AT_NOTIFICATION, ...)
- **tls.dict**: TLS record types, record version pairs, handshake message types, TLS 1.2 / 1.3 cipher suite codes, extension type codes and alert codes
- **trusted_pubkey.dict**: ASN.1 tags and SubjectPublicKeyInfo algorithm OIDs (RSA, EC P-256/P-384/P-521, Ed25519 / Ed448) plus PEM markers
- **vici.dict**: VICI wire-format type codes (SECTION_START, SECTION_END, KEY_VALUE, LIST_START, LIST_ITEM, LIST_END) and common section / key names

`fuzz_ids` has no dictionary because its identification-type enum space is small enough for the mutator to enumerate naturally.
