# Lab 02 — Check Certificate Revocation Status with OCSP

## Overview
In this lab, I investigated how certificate revocation is handled in real-world PKI systems by using the Online Certificate Status Protocol (OCSP) to check the validity of a live certificate.

The goal was to understand how systems determine whether a certificate is still trustworthy after issuance, and how OCSP and Certificate Revocation Lists (CRLs) are used to prevent compromised or invalid certificates from being trusted.

---

## Steps Performed


First, I retrieved the leaf certificate from (github.com) using OpenSSL.
I then, extracted and saved the certificate chain, identifying the intermediate CA (issuer certificate).
Parsed the certificate extensions to locate:OCSP responder URL and CRL Distribution Point
I then used OpenSSL to construct and send an OCSP request using:The leaf certificate,The issuer (intermediate) certificate
The OCSP responder URL
Last, I captured and analyzed the OCSP response, including certificate status and validity timing fields

---

## Results
Successfully retrieved and inspected the leaf certificate:
Subject: CN=github.com
Issuer: Sectigo Public Server Authentication CA DV E36
Identified revocation endpoints from certificate extensions:
OCSP URL: http://ocsp.sectigo.com
CA Issuer URL: http://crt.sectigo.com/...
Executed an OCSP query and received a valid response:
OCSP Response Status: successful
Certificate Status: good
This Update: timestamp of when the status was generated
Next Update: timestamp indicating how long the response can be cached
Verified that the certificate was not revoked and is currently trusted.


## Key Findings
OCSP provides real-time validation of a certificate’s revocation status, unlike CRLs which rely on periodically downloaded lists.

The OCSP query requires both the leaf certificate and the issuer certificate because revocation status is tracked by the issuing CA.
The "good" status confirms that the certificate has not been revoked, but does not guarantee overall trust (chain validation is still required).

## Explanation
This lab demonstrates how revocation checking is integrated into the certificate validation process.

OCSP allows a client (such as a browser or server) to query a CA in real time to determine whether a certificate has been revoked. This is critical in cases where a private key has been compromised or a certificate should no longer be trusted before its expiration date.

Compared to CRLs:
OCSP is more efficient because it checks the status of a single certificate on demand.

CRLs require downloading and parsing an entire list of revoked certificates, which can become large and outdated between updates.

This lab highlights a key principle of PKI:

Trust must be continuously validated throughout the certificate lifecycle

The OCSP response included "This Update" and "Next Update" timestamps, which defines how long the response can be cached by clients. This prevents clients from querying the OCSP on every TLS handshake and improves performance.

In scenarios where the OCSP responder returns an "unknown" status, the client cannot confirm the certificate’s validity. This may result in a soft fail (connection allowed) or hard fail (connection blocked), which has important implications for availability vs. security.

## Challenges / Troubleshooting
Initially encountered issues where the OCSP query failed due to a missing issuer certificate.

Resolved by extracting the correct intermediate certificate from the full certificate chain.

Observed that OCSP queries may fail if the responder is unavailable or blocked.

Verified that correct file paths and certificate pairing (leaf + issuer) are required for successful OCSP validation.


## Artifacts
leaf_cert.pem — Leaf certificate retrieved from live site
issuer_cert.pem — Intermediate CA certificate used for OCSP query
ocsp_response.txt — Captured OCSP response output



*CVI PKI Career Pathway — Foundations Phase*



