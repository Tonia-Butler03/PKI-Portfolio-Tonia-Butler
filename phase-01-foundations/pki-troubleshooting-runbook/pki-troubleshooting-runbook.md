# PKI Troubleshooting Runbook

---

**Title:**
TLS Certificate Validation Failure Due to Hostname Mismatch

---

## Problem Statement
A TLS connection was expected to validate successfully when connecting to a secure HTTPS endpoint. Instead, certificate verification failed because the hostname requested did not match the identities listed in the certificate.

---

## Environment

*Note the relevant context so someone reading this knows whether it applies to their situation.*

**Tool(s) used:**
- OpenSSL (`openssl s_client`, `openssl x509`)

**Certificate type or component involved:**
- Public TLS leaf certificate  
- Subject Alternative Name (SAN) extension  

**Any relevant configuration details:**
- Target: `wrong.host.badssl.com:443`  
- SNI specified using the `-servername` flag  
- Certificate retrieved and analyzed locally in PEM format  

---

## Symptoms
- TLS handshake completed but certificate validation failed  
- OpenSSL returned a hostname mismatch error  
- Certificate appeared valid (not expired, properly signed)
- 

**Command executed:**

```bash
openssl s_client -connect wrong.host.badssl.com:443 -servername wrong.host.badssl.com
_Observed output (relevant portion):

```bash
openssl s_client -connect wrong.host.badssl.com:443 -servername wrong.host.badssl.com
Verify return code: 62 (Hostname mismatch)
_TLS handshake completed successfully
Certificate validation failed due to hostname mismatch_
-


****## Diagnostic Steps****



**1.Establish TLS connection and observe validation result**
-openssl s_client -connect wrong.host.badssl.com:443 -servername wrong.host.badssl.com
-Confirmed connection succeeded
-Identified Verify return code: 62 (Hostname mismatch)

**2.Retrieve the certificate for inspection**
-openssl s_client -connect wrong.host.badssl.com:443 -servername wrong.host.badssl.com \
</dev/null 2>/dev/null | openssl x509 -outform PEM > mismatch_cert.pem
-Saved the certificate for analysis

**3.Inspect certificate details**
-openssl x509 -in mismatch_cert.pem -text -noout
-Reviewed Subject and Issuer fields
-Located X509v3 Subject Alternative Name section

**4. Compare hostname against SAN entries**
-Requested hostname: wrong.host.badssl.com
-SAN entries did not include this hostname
-Determined the root cause was a mismatch between the requested domain and certificate identity



## Resolution

The issue was caused by a mismatch between the requested hostname and the certificate’s SAN entries.

Resolution actions:

Use the correct hostname that matches the certificate
OR configure the server/load balancer to present the correct certificate
OR reissue the certificate with the correct SAN entries

---

## Prevention Note

Always verify that the requested hostname is included in the certificate’s SAN before deployment. During testing, validate certificate-to-hostname alignment using tools like OpenSSL or SSL Labs.

---

**Lab this scenario is drawn from:*labs/week-06-incident-diagnosis/submissions/

---

*CVI PKI Career Pathway — Phase 1 Foundations*
