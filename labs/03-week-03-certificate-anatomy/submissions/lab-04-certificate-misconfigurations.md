# Lab — 04-certificate-misconfigurations

## Overview
The purpose of this lab was to understand how common certificate misconfigurations can cause TLS validation to fail. I reviwed different scenarios that break trust, such as missing SAN fields, incorrect EKU settings, expired certificates, and other validation problems. This lab helped me see how certificate details directly affect whether a secure connection succeeds or fails.

What PKI concept or system behavior were you investigating?
I was investigating how certificate validation works in real-world TLS connections. The lab focused on how clients check certificate fields and extensions before deciding whether to trust a certificate. It showed that even if a certificate exists, a misconfiguration can still make the connection fail.

## Environment
Document the environment used to complete the lab.

- Operating System:Windows
- Terminal Used:Git bash
- OpenSSL Version (if applicable):3.4.4

---

## Steps Performed
Summarize the key steps you performed to complete the lab.
First, I created the submissions file in my repository and documented my analysis for each misconfiguration scenario. 

Next, I reviewed each certificate, including missing SAN, incorrect EKU, expired certificates, and missing intermediate, and determined why each one would fail validation. 

Then, I connected each issue to the specific TLS validation rule being violated. 

Finally, I saved the file and pushed it to GitHub.

---

## Results

-  Hostname validation fails because modern TLS clients rely on the Subject Alternative Name instead of the Common Name.

- The certificate is rejected because it is not valid for TLS Web Server Authentication.

- The certificate fails validation because it is outside of its valid date range.

- The chain cannot be completed to a trusted root, so the certificate is not trusted.
  
The results showed that each misconfiguration caused certificate validation to fail for a specific reason. These findings showed how strict TLS validation is and how small configuration issues can prevent secure connections.


## Key Findings
-A certificate without a Subject Alternative Name (SAN) can fail hostname validation in modern TLS.

-An incorrect Extended Key Usage (EKU) can make a certificate invalid for server authentication.

-An expired certificate fails validation because it is no longer within its trusted date range.

-Broken certificate conditions, such as hostname mismatch or chain issues, prevent the client from trusting the certificate.

---

## Explanation
These results matter because TLS depends on strict certificate validation to protect secure communications. The SAN is important because modern browsers and clients use it to confirm the certificate matches the website or server name. EKU matters because it defines what the certificate is allowed to be used for, and expiration matters because trust is only valid for a limited time. If any of these conditions are wrong, the connection fails to protect users from impersonation or misissued certificates.

---

## Challenges / Troubleshooting
One challenge in this lab was keeping track of which field caused the validation failure. I had to look closely at each certificate condition to understand whether the problem was identity, usage, or validity period. This helped me better understand how small certificate errors can create real TLS outages. Another challenge was ensuring that my repo was correctly organized to submit the completed assignment. I nneded to recolne my repo and trouble shoot the issue prior to moving forward witht he assignment. 


## Artifacts


---

CVI PKI Career Pathway — Foundations Phase
