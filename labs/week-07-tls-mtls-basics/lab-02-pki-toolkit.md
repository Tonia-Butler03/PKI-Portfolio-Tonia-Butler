# My PKI Toolkit  
**CVI PKI Career Pathway — Phase 1 Foundations**  
Completed: April 2026  

---

## About This Document

This document captures the PKI tools that I used throughout Phase 1 labs, including how I applied them in real scenarios. It reflects my hands-on experience retrieving, analyzing, and validating certificates, and serves as a reference for future PKI troubleshooting and analysis.

---

## Core Command-Line Tools

### openssl s_client — Retrieve Live Certificates

**What it does:**  
Establishes a TLS connection to a remote server and retrieves the certificate chain presented during the handshake.

**When to use it:**  
I use this when I need to inspect a live endpoint and understand what certificate is actually being presented.

**Example command from my labs:**
openssl s_client -connect epic.com:443 -showcerts </dev/null 2>/dev/null

**What the output tells you:**
Shows the full certificate chain, TLS version, cipher suite, and verification result.

_Phase 1 source: Week 7 — Enterprise Certificate Analysis

_
**openssl x509 — Parse Certificate Details**

**What it does:**
Reads a certificate file and displays all fields in a human-readable format.

**When to use it:**
I use this after retrieving a certificate to inspect its validity, issuer, subject, and extensions.

**Example command from my labs:**
openssl x509 -in enterprise_cert.pem -text -noout

**What the output tells you:**
Shows validity period, SAN entries, issuer, and certificate type.

_Phase 1 source: Week 7 — Enterprise Certificate Analysis_


**openssl req — Generate a CSR**

**What it does:**
Creates a Certificate Signing Request (CSR) for certificate issuance.

**When to use it:**
Used when generating a new certificate request during lifecycle management labs.

**Example command from my labs:**
openssl req -new -key test.key.pem -out test_csr.pem

**What the output tells you:**
Produces a CSR file containing subject and public key information for a CA.

_Phase 1 source: Week 5 — CSR Generation_


**openssl verify — Validate Certificate Chain**

**What it does:**
Verifies that a certificate chains back to a trusted root CA.

**When to use it:**
Used when checking whether a certificate is trusted or diagnosing trust failures.

**Example command from my labs:**
openssl verify -CAfile root_cert.pem leaf_cert.pem

**What the output tells you:**
Returns OK if valid or identifies where the trust chain fails.

_Phase 1 source: Week 4 — Trust Chain Validation_



**openssl ocsp — Check Revocation Status**

**What it does:**
Checks certificate revocation status using OCSP.

**When to use it:**
Used when validating whether a certificate is still valid or revoked.

**Example command from my labs:**
openssl ocsp -issuer issuer_cert.pem -cert leaf_cert.pem -url http://ocsp.example.com

_Phase 1 source: Week 5 — Revocation Analysis_



**openssl pkcs12 — Bundle Certificates**

**What it does:**
Packages certificates and private keys into a .pfx/.p12 file.

**When to use it:**
Used when preparing certificates to import into the system or deployment.

**Example command from my labs:**
openssl pkcs12 -export -out bundle.pfx -inkey key.pem -in cert.pem

**What the output tells you:**
Creates a bundled certificate file used for applications or OS environments.

_Phase 1 source: Week 4 — Certificate Formats_



**Network and Inspection Tools**
curl — Inspect Server Headers

**What it does:**
Sends HTTP requests and retrieves response headers.

**When to use it:**
Used to inspect infrastructure and help determine where TLS terminates.

**Example command from my labs:**
curl -sI https://epic.com | grep -i "server\|via\|x-cache\|cf-ray\|x-amz"

**What the output tells you:**
Reveals server type and potential load balancer or proxy indicators.

_Phase 1 source: Week 7 — TLS Termination Analysis_



**Reference and Analysis Services**
SSL Labs SSL Server Test

**What it does:**
Analyzes TLS configuration and assigns a security grade.

**When to use it:**
Used to validate TLS posture and identify weaknesses.

**Example:**
https://www.ssllabs.com/ssltest/

**What the output tells you:**
Shows TLS versions, cipher strength, HSTS, and overall grade.

_Phase 1 source: Week 7 — TLS Configuration Analysis_



**crt.sh — Certificate Transparency Search**

**What it does:**
Searches CT logs to view certificate issuance for a domain.

**When to use it:**
Used to analyze certificate history and identify multiple certificate authorities.

**Example:**
https://crt.sh/?q=epic.com

**What the output tells you:**
Shows issuance patterns, subdomains, and CA distribution.

_Phase 1 source: Week 7 — CT Log Analysis_



**Workflow and Repository Management**
mkdir — Create Directory Structure

**What it does:**
Creates directories for organizing lab submissions.

**When to use it:**
Used when setting up structured folders for consistent project organization.

**Example command from my labs:**
mkdir -p labs/week-07-tls-mtls-basics/submissions/pki-toolkit

**What the output tells you:**
Creates directories if they do not already exist.

_Phase 1 source: Week 7 — Lab Setup_

**Phase 1 Skills Summary**

_Phase 1 helped me move from understanding PKI concepts to applying them in real-world scenarios. I used tools like OpenSSL and curl to retrieve and analyze certificates, validate trust chains, and inspect TLS configurations. I also used Certificate Transparency logs to understand how organizations manage certificates at scale. These skills directly support real-world tasks such as diagnosing certificate failures, validating trust relationships, and analyzing enterprise PKI environments._

