# Lab 01 — expired-certificate

**Week 6 · PKI Incident Diagnosis & Troubleshooting**

---

## Incident Summary

**Target system:** portal.metrogeneral.org
**Diagnosed by:** Tonia Butler
**Date of diagnosis:** 4/10/2026

---

### What failed
The TLS failure was caused by the server presenting an expired leaf certificate for *.badssl.com, which made the certificate invalid during client validation.


---

### Evidence
- Not Before: Apr  9 00:00:00 2015 GMT
- Not After : Apr 12 23:59:59 2015 GMT
- Subject: OU=Domain Control Validated, OU=PositiveSSL Wildcard, CN=*.badssl.com
- Issuer: C=GB, ST=Greater Manchester, L=Salford, O=COMODO CA Limited, CN=COMODO RSA Domain Validation Secure Server CA
- OpenSSL returned Verification error: certificate has expired
- OpenSSL verify return code: 10 (certificate has expired)
- The server presented a 3-certificate chain: leaf, intermediate, and root
- OCSP responder URL was present: http://ocsp.comodoca.com
- Days expired: 4,016 days

---

### Why it failed

TLS clients validate whether the presented certificate is currently valid by checking the X.509 validity window, including the Not Before and Not After fields. In this case, the Not After date had already passed, so the certificate could no longer be trusted even though the Subject, SAN, and issuing CA information were present and readable.

This connects directly to certificate lifecycle management from Week 5 and the Week 6 troubleshooting framework. A certificate that is expired fails validation immediately because expiration is a hard stop in the trust decision process. Even if other parts of the certificate appear correct, the connection fails because the certificate is no longer valid for use.

---

### Chain status

The certificate chain presnted all components. The server presented three certificates: the leaf certificate , the intermediate certificate COMODO RSA Domain Validation Secure Server CA, and a root certificate tied to AddTrust External CA Root.

There were no obvious gaps such as a missing intermediate. However, the primary validation failure was certificate expiration. The presence of an older root in the chain structure could cause additional trust concerns in some environments, but it was not the main cause of the TLS failure in this incident.

openssl s_client -connect expired.badssl.com:443 -showcerts </dev/null 2>/dev/null


### Remediation path

1.Confirm the affected hostname and service that are presenting the expired certificate.
2.Review the current certificate details, including Subject CN, SAN entries, issuer, and expiration date.
3.Generate a replacement certificate that includes the correct SAN values for the affected hostname.
4. Complete the required validation process with the issuing CA.
5. Install the renewed leaf certificate on the server.
6. Install the correct intermediate certificate bundle alongside the new leaf certificate so the full operational chain is presented.
7. Restart the affected service so the replacement certificate is active.
8. Re-test the endpoint with openssl s_client to confirm the new certificate is present.
9. Verify the new certificate's Not Before and Not After dates.
10.Update the certificate inventory with the new expiration date.

### Prevention
A concrete way to prevent this failure is to implement certificate expiration monitoring with automated alerts well before the renewal deadline, such as 60, 30, 14, and 7 days before expiration.

## Diagnostic Steps

Step 1 — Retrieve**Command used:**```bashopenssl s_client -connect expired.badssl.com:443 -servername expired.badssl.com -showcerts </dev/null 2>/dev/null \  | openssl x509 -outform PEM > expired_cert.pem\


What was observed:
The certificate was successfully retrieved and saved in PEM format as expired_cert.pem. Although the  endpoint is intentionally broken, the certificate was still retrievable for inspection. This reinforced the difference between retrieving a certificate and successfully establishing a trusted TLS session.

Step 2 — Parse
Command used:
openssl x509 -in expired_cert.pem -text -noout
Key fields from the certificate:
FieldValueSubject CN*.badssl.comIssuerCOMODO RSA Domain Validation Secure Server CANot BeforeApr 9 00:00:00 2015 GMTNot AfterApr 12 23:59:59 2015 GMTSAN entriesDNS:*.badssl.com, DNS:badssl.com

What I found:
The parsed certificate showed that the leaf certificate was issued to *.badssl.com and included SAN entries for both *.badssl.com and badssl.com. The most important finding was that the Not After date had already passed, confirming that the certificate was expired and no longer valid for TLS use.

Step 3 — Validate the Chain
Command used:
openssl s_client -connect expired.badssl.com:443 -servername expired.badssl.com -showcerts </dev/null 2>/dev/null
Result:
The server presented a 3-certificate chain. OpenSSL reported:
Verification error: certificate has expiredVerify return code: 10 (certificate has expired)
What I found:
This step confirmed that the server was presenting a complete chain that included the leaf certificate, an intermediate CA, and a root certificate. That helped rule out a missing intermediate as the primary issue. The failure was tied to expiration rather than a broken chain.

Step 4 — Check Revocation and Trust
Command used:
openssl x509 -in expired_cert.pem -noout -text | grep -A1 "OCSP"
What I found:
The certificate included an OCSP responder URL:
OCSP - URI:http://ocsp.comodoca.com
This showed that revocation information was available in the certificate. However, revocation was not the deciding factor in this incident because the certificate was already expired. Once a certificate is outside its validity period, it is already invalid, so the remediation priority is renewal and redeployment rather than revocation checking.

Reflection:
This lab reinforced that PKI troubleshooting has to be a systematic process. Even when the answer seems obvious, like an expired certificate, it is still important to retrieve the actual certificate, parse the X.509 fields, and confirm the chain instead of guessing.
The step that made me slow down the most was chain validation. I had to separate the idea of a structurally complete chain from the idea of a trusted or valid certificate. That helped me better understand how expiration, chain presentation, and trust all work together during TLS validation.

---



*CVI PKI Career Pathway — Foundations Phase*
