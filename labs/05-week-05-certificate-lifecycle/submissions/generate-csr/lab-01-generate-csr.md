# Lab 01 — Generate a CSR and Simulate the Issuance Workflow

## Overview
In this lab, I simulated the certificate issuance process by generating a private key, creating a Certificate Signing Request (CSR), and issuing a self-signed certificate using OpenSSL.

The objective was to understand how identity is established in Public Key Infrastructure (PKI), specifically how a subject proves ownership of a private key and requests a certificate from a Certificate Authority (CA). This lab focused on the relationship between cryptographic keys, identity factors, and the trust model used in certificate-authentication.

---

## Steps Performed
1. First, I generated a private key using OpenSSL to establish a secure identity.
2. Then, I created a CSR using the private key and defined subject details (Common Name, Organization, Country).
3. Next, I used the private key to self-sign the CSR and generate a certificate.
4. Last, I inspected the certificate to review subject, issuer, and validity details.


## Results

-Successfully generated a private key and CSR.
-Created a self-signed certificate using the CSR.
-Verified certificate details using OpenSSL:
-Subject: identifies the entity (e.g., domain or system)
-Issuer: same as subject (self-signed)
-Validity window: defined certificate lifetime
-Confirmed that the certificate structure matches X.509 format.

If you include screenshots, store them in `assets/screenshots/` at the root of your repo and reference them here.

**How to embed an image:**

**Option A — Terminal / Local Editor**

Save your screenshot to `assets/screenshots/` in your repo, then reference it using a relative path from your submission file:

```markdown
![Description of your screenshot](../../../assets/screenshots/test-confirmed-key.png)
```
![Description of your screenshot](../../../assets/screenshots/test-confirmed-key.png)
```
![Description of your screenshot](../../../assets/screenshots/test-confirmed-key.png)
```
![Description of your screenshot](../../../assets/screenshots/test-confirmed-key.png)
```

> The `../../../` moves up three levels: `submissions/` → `week-03/` → `labs/` → repo root, then into `assets/screenshots/`.

**Option B — GitHub Web (Easiest)**

Open your `.md` file on GitHub, click the pencil icon to edit, then **drag and drop your image directly into the text editor**. GitHub will upload it automatically and insert the correct link for you.

Example of what an embedded image looks like:

```markdown
![Certificate output showing SAN field](../../../assets/screenshots/san-field.png)
```

---

## Key Findings
Document the most important observations from the lab.

Examples:

- What you discovered about the certificate, key, or protocol
- How a specific field or extension affected the outcome
- What a validation result indicated
- Any unexpected behavior or results

-
-
-

---

## Explanation
Explain **why the results matter**.

Examples:

- Why a specific field or extension is required
- Why a validation succeeded or failed
- What the result means in a real-world PKI context
- How this connects to the week's learning outcomes

---

## Challenges / Troubleshooting
Document any issues encountered during the lab and how you resolved them.

Examples:

- Command errors
- Missing files or dependencies
- Verification failures and how you diagnosed them

---

## Artifacts
List the files generated or submitted during this lab.

Examples:

- Any `.pem`, `.crt`, or `.key` files produced
- Your completed lab write-up `.md` file
- Screenshots stored in `assets/screenshots/`

---

*CVI PKI Career Pathway — Foundations Phase*
