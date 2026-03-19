# Week 01 Lab — Certificate Inspection

## Screenshot Evidence

1. Capture a screenshot of the certificate details in your browser.
2. Save it as:

assets/screenshots/week-01/certificate-inspection.png

3. Embed the screenshot below:

![Certificate Inspection](../../assets/screenshots/week-01/certificate-inspection.png)


## Website Information

**Website inspected:**  
https://www.homedepot.com/

**Issuer (Certificate Authority):**  
DigiCert

**Valid from:**  
Sunday, August 3, 2025 at 8:00:00 PM

**Valid until:**  
Tuesday, April 14, 2026 at 7:59:59 PM

**Signature algorithm:**  
PKCS #1 SHA-256 With RSA Encryption

---

## Subject Alternative Names (SAN Entries)

List at least 2–3 SAN entries:

- api.homedepot.com
- apionline.homedepot.com
- secure2.homedepot.com

---

## Observations

Document three observations about the certificate.

### Observation 1
I noticed that my desktop showed an alernative thrid party CA due to the installed fortinet firewall, while my mobil device showed the issuing CA as Digicert.

### Observation 2
I noticed that there were several SAN's, some of the names were easily identifiable as being apart of the company  while other SAN's were not as easily reognizable as the company name was not included.

### Observation 3
I noticed that the certificate viewer provides critical details of a digital certificate.This helps you verify identity, check trust, and troubleshoot HTTPS or PKI-related issues.

---

## Reflection

Based on your inspection, explain how this certificate contributes to secure HTTPS communication.

Based off my inspection, the certificate enables secure HTTPS communication by verifying the identity of the web address (homedpot.com) and providing the public key needed to establish encrypted communication of data in transit. The browser validates the certificate using trusted certificate authorities and then uses the public key during the TLS handshake, this creates a secure session. This process ensures authentication, encryption, and data integrity for web communications.
