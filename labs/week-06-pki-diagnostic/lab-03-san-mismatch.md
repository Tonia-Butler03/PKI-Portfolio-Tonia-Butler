# Lab 03-san-mismatch

**Week 6 · PKI Incident Diagnosis & Troubleshooting**
**CVI PKI Career Pathway — Phase 1 Foundations**

---

## Incident Summary

**Target system:** Staff scheduling portal (simulated via wrong.host.badssl.com) 
**Diagnosed by:** Tonia Butler
**Date of diagnosis:** 04/12/2026



### What failed

The TLS failure was caused by a hostname mismatch between the requested domain and the Subject Alternative Name (SAN) entries in the certificate.

---

### Evidence

- Subject CN:
  CN=*.badssl.com 

- SAN entries:
  DNS:*.badssl.com

- Hostname connected to:
  wrong.host.badssl.com 

- Hostname accessed: wrong.host.badssl.com 

- OpenSSL verification:
  error 20 at 0 depth lookup: unable to get local issuer certificate 
- The SAN entries do not include wrong.host.badssl.com


### Why it failed
TLS clients validate that the hostname being accessed matches one of the identities listed in the certificate’s Subject Alternative Name (SAN) extension. In this case, the certificate was issued for *.badssl.com and badssl.com, but the client connected to wrong.host.badssl.com. Because the hostname was not included in the SAN, TLS validation fails even though the certificate itself is valid and the chain is trusted.



### Chain status

The certificate chain was complete and valid. The server presented both the leaf certificate and the intermediate CA (Let's Encrypt R13), and the chain successfully validated to a trusted root CA (ISRG Root X1).

There were no chain-related issues. The failure was not related to trust, expiration, or revocation. It was strictly a hostname mismatch.



### Remediation path
1. First, I Identified the correct hostname being used by clients (wrong.host.badssl.com).
2. Next step was to review the existing certificate to confirm its SAN entries.
3. Then, Request a new certificate that includes the correct hostname in the SAN 
4. Complete domain validation with the CA.
5. Install the new certificate on the server.
6. Restart or reload the service to apply the updated certificate.
7. Validate the new certificate using openssl s_client and confirm the hostname matches the SAN.
8. Test in a browser to confirm the TLS warning is resolved.


---

### Prevention

Implement a certificate request and validation process that requires verification of all required hostnames (SAN entries) before certificate issuance and deployment. This ensures that certificates are issued with the correct identities and prevents hostname mismatch errors.

---

## Diagnostic Steps

### Step 1 — Retrieve

**Command used:**

openssl s_client -connect wrong.host.badssl.com:443 -servername wrong.host.badssl.com </dev/null 2>&1


**What I observed:**

The connection successfully retrieved the server certificate and showed a complete certificate chain. The Verify return code was 0 (ok), indicating that the certificate chain was valid and trusted. No connection or trust errors were observed at this stage.



### Step 2 — Parse

**Command used:**

openssl x509 -in mismatch_cert.pem -text -noout

openssl x509 -in mismatch_cert.pem -noout -text | grep -A5 "Subject Alternative Name"




**Key fields from the certificate:**

| Field       | Value                            |
--------------------------------------------------
| Subject CN  | CN=*.badssl.com                  |
| Issuer      | CN=R13 (Let's Encrypt)           |
| Not Before  | Mar 24 20:02:52 2026 GMT         |
| Not After   | Jun 22 20:02:51 2026 GMT         |
| SAN entries | DNS:*.badssl.com, DNS:badssl.com |


**What I found:**

The certificate was valid and within its validity period. However, the hostname used for the connection (wrong.host.badssl.com) was not included in the SAN entries. This caused the hostname mismatch.


### Step 3 — Validate the Chain

**Command used:**


openssl verify mismatch_cert.pem

**Result:**
Verification returned an error when using the default trust store, but the full connection output showed:
Verify return code: 0 (ok)

**What I found:**
The certificate chain was valid and complete, including the intermediate CA (R13) and trusted root (ISRG Root X1). This confirmed that the failure was not related to a broken chain or missing intermediate certificate.



### Step 4 — Check Revocation and Trust

**Command used:**

openssl x509 -in mismatch_cert.pem -noout -text | grep -A2 "OCSP"


**What you found:**
No OCSP URL was observed in the parsed output. There was no indication of a revocation issue. The certificate was valid and trusted, and the failure occurred due to hostname mismatch rather than revocation or trust store issues.



## Reflection

This lab reinforced that a certificate can be fully valid and trusted and still fail TLS validation if the hostname does not match the SAN entries. It clarified the importance of the SAN extension over the Subject CN in TLS validation.

I had to slow down and carefully compare the requested hostname to the SAN entries to clearly identify the mismatch.The certificate was trusted, but it wasn’t the right identity.



*CVI PKI Career Pathway — Foundations Phase*
