# Lab 03 — Simulate a Certificate Expiration Scenario

## Overview

In this lab, I simulated a certificate expiration scenario to understand how expiration impacts system availability and how engineers detect and respond to it.

Unlike revocation (which is reactive and event-ddriven) expiration is a predictable lifecycle event. The focus of this lab was to explore how expiration is enforced, how it can be detected before failure occurs, and how to execute a full replacement workflow to restore trust.


## Steps Performed

First, I generated a private key and created a CSR this represented a system requesting a certificate.

I then Issued a short-lived certificate (1 day validity) to simulate an approaching expiration scenario.

Next, I used openssl X.509 -checkend with different times to evaluate when the certificate would expire.

I created an already-expired certificate by setting the validity window in the past.

Validated the expired certificate using OpenSSL and observed verification failures.

Last, generated a new private key and CSR, then issued a replacement certificate to simulate the renewal process/workflow.

---

## Results

Created a short-lived certificate with a limited lifetime:
Confirmed using:notBefore and notAfter fields

-checkend to evaluate expiration thresholds
expiration detection:
-checkend 3600 → Certificate will not expire (within 1 hour)
-checkend 86400 → Certificate will expire (within 24 hours)

Created an expired certificate:
Validity window set to January 2023

Confirmed expired using:
-dates -noout
-checkend 0 → Certificate will expire

Validation results for expired certificate:
OpenSSL verification failed with:
error 10: certificate has expired

verification failed
Replacement certificate:

Generated a new certificate with a valid future expiration window

Confirmed that the certificate was valid and did not expire within the defined vaildation period



## Key Findings
-Certificate expiration is strictly enforced at validation time and results in immediate rejection.

-Expiration is deterministic and can be predicted in advance, unlike revocation.

-Even a correctly structured and signed certificate becomes unusable once it passes its notAfter date.

-The correct response to expiration is certificate replacement, not reuse or extension of the expired certificate.

- The -checkend flag returns an exit code that can be used in automation:
  - Exit code 0 indicates the certificate will NOT expire within the specified time window
  - Exit code 1 indicates the certificate WILL expire within the specified time window

---

## Explanation

This lab highlights the infrastucture side of PKI, specifically how certificate expiration affects a system stability.

When a certificate expires, it fails validation during the TLS handshake. This prevents clients from establishing secure connections, leading to service outages. Unlike revocation, which requires external communication with a CA (OCSP/CRL), expiration is enforced locally by comparing the current system time to the certificate’s validity period.

Because expiration is predictable, organizations are expected to monitor certificate lifetimes and renew them proactively. The use of -checkend demonstrates how automation can be used to detect certificates nearing expiration and trigger alerts or renewal workflows.

The replacement process reinforces a best practice in PKI:

New certificates should be issued with new key material rather than extending the use of an existing key

This reduces risk and ensures continued security over time.

- Certificate replacement is preferred over renewal when:
  - A private key is suspected to be compromised
  - Organizational or domain details change
  - The original key algorithm no longer meets current security standards

## Challenges / Troubleshooting

Encountered issues generating CSRs using the -subj flag due to formatting conflicts in the Windows Git Bash environment.

Initial attempts to create an expired certificate failed due to unsupported OpenSSL flags (-startdate / -enddate).
Resolved by using the correct flags (-not_before and -not_after) supported by the environment.

Verified each step using ls and OpenSSL inspection commands to confirm that files were created before proceeding.

---

## Artifacts
test_cert_short.pem — Short-lived certificate used to simulate near-expiration
test_cert_expired.pem — Certificate with a past validity window used to simulate failure
test_cert_replacement.pem — Replacement certificate issued after expiration
lab-03-expiration-stretch.md — Lab write-up

![expiredcertificate](../../../assets/screenshots/certitificate-expired.png)
```
![checkend](../../../assets/screenshots/check-end-strech.png)
```
![validationfailed](../../../assets/screenshots/validation-failed-stretch-expired.png)
---

*CVI PKI Career Pathway — Foundations Phase*
