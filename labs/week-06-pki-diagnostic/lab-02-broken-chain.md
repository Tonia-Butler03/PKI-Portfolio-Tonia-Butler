# Lab 2 — broken-chain

**Week 6 · PKI Incident Diagnosis & Troubleshooting**
---

## Incident Summary

**Target system:** Radiology imaging platform (simulated via incomplete-chain.badssl.com)
**Diagnosed by:** Tonia Butler
**Date of diagnosis:** 04/11/2026

---

### What failed

The TLS failure was caused by the server presenting only the leaf certificate and omitting the required intermediate certificate, this prevented the use of a complete trust chain.


---


### Evidence

- Leaf certificate subject: CN=*.badssl.com 
- Issuer CN (missing intermediate): CN=R13 (Let's Encrypt) 
- openssl verify leaf_cert.pem error before fix: error 20 at 0 depth lookup: unable to get local issuer certificate 
- Result after adding the intermediate-Pending — intermediate certificate not successfully downloaded or applied
- The server sent only one certificate in the Certificate chain section, proving that the intermediate CA was not presented.
- openssl verify leaf_cert.pem returned an error such as "unable to get local issuer certificate" and  "unable to verify the first certificate".
- The Issuer field in the leaf certificate identified the intermediate CA that should have been present in the chain.
- The Authority Information Access extension included a CA Issuers URI that pointed to the missing intermediate certificate.
- After downloading the intermediate and verifying with openssl verify untrusted issuer_cert.pem leaf_cert.pem`, validation was successful.

---

### Why it failed

TLS client (Radiology imaging platform) did not trust the leaf certificate by itself. The process requires a certificate path from the leaf certificate to the trusted root CA, this process also includes the intermediate CA certificate presented by the server. In this case, the server renewed the leaf certificate but failed to include the intermediate CA, the Radiology imaging platformc could not complete path building and returned a chain validation error.

This connects directly to Week 5 lifecycle management and troubleshooting. A certificate can be valid but fail when the full chain chain is required to validate trust.

---

### Chain status

The certificate chain was not complete on the server. Only the leaf certificate was presented, so the required intermediate CA certificate was missing from the chain.

While parsing the certificate I found that there were no signs that the primary issue was expiration, hostname mismatch, or revocation. The failure was specifically an incomplete chain configuration problem caused by the missing intermediate.

---

### Remediation path

1. Confirm the affected server and hostname that are failing TLS validation.
2. Retrieve the currently presented certificate.
3. Parse the leaf certificate to identify the Issuer CN and locate the missing intermediate CA.
4. Use the Authority Information Access CA Issuers URI to download the correct intermediate certificate.
5. Convert the downloaded certificate to PEM format.
6. Validate the leaf certificate locally with the intermediate using openssl verify -untrusted issuer_cert.pem leaf_cert.pem.
7. Install the intermediate certificate on the Radiology imaging platform 
8. Re-test with `openssl s_client` and confirm that the server now sends the leaf plus intermediate certificate.
9. Confirm verification was successful
10. Document the incident and update the team.
---

### Prevention

A concrete way to prevent this failure is to require a certficate validation check that confirms the Radiology imaging platform is presenting the full certificate chain every 90 days.

---

## Diagnostic Steps


### Step 1 — Retrieve

Command used:
openssl s_client -connect incomplete-chain.badssl.com:443 -showcerts </dev/null 2>/dev/null \
  | openssl x509 -outform PEM > leaf_cert.pem
openssl s_client -connect incomplete-chain.badssl.com:443 </dev/null 2>&1

What I observed:

The leaf certificate was successfully retrieved and saved as leaf_cert.pem. When I reviewed the full server output, the Certificate chain section showed that the server was not sending the full chain. The verify output reported a chain validation error, confirming that the problem was not a connection issue but a trust path problem.

Step 2 — Parse

Command used:

openssl x509 -in leaf_cert.pem -text -noout
openssl x509 -in leaf_cert.pem -noout -text | grep -A3 "Authority Information Access"

Key fields from the certificate:

Field	Value
Subject CN	 CN=*.badssl.com
Issuer       US, O=Let's Encrypt, CN=R13- URI:http://r13.i.lencr.org/
Not Before	 Mar 24 20:02:52 2026 GMT
Not After    Jun 22 20:02:51 2026 GMT
SAN entries	DNS:*.badssl.com, DNS:badssl.com

What I found:

The leaf certificate was valid and reveled the expected identity information. The most important clue was the Authority Information Access extension  which pointed to the missing intermediate certificate needed to rebuild the chain.

Step 3 — Validate the Chain

Command used:

openssl verify leaf_cert.pem
curl -s "https://[URI from CA Issuers extension]" -o intermediate.der
openssl x509 -inform DER -in intermediate.der -out issuer_cert.pem
openssl verify -untrusted issuer_cert.pem leaf_cert.pem

Result:

verification failed with an error such as:unable to get local issuer certificate/unable to verify the first certificate

After adding the missing intermediate with -untrusted, verification was succesful

What I found:

This step confirmed that the leaf certificate itself was not the main problem. The failure happened because OpenSSL could not build a path from the leaf certificate to a trusted root without the missing intermediate. Once the intermediate was supplied, validation completed successfully.

Step 4 — Check Revocation and Trust

Command used:

openssl s_client -connect incomplete-chain.badssl.com:443 -showcerts </dev/null 2>/dev/null \
  | grep "Verify return code"

What you found:

The roblem was caused by an incomplete chain of trust. Once the intermediate was available during verification, the chain could be built to a trusted root and validation succeeded. There was no indication that revocation was the cause of the failure, so this incident was a chain configuration issue rather than a revocation or trust anchor problem.

***Reflection


This lab reinforced that a certificate can look completely fine when viewed by itself and still fail  if the server does not present the full chain. It clarified the difference between a valid leaf certificate and a valid certificate path.

The step that made me slow down was parsing the Issuer field and connecting it to the missing intermediate CA. That was the moment where the issue stopped looking like a generic TLS error and started making sense as a specific chain-building failure.


