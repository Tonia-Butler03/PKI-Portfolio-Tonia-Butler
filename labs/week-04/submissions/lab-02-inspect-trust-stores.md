# Lab — [Lab Title]

## Overview
Briefly describe the purpose of this lab in your own words.
The purpose of this lab was to understand where trusted root certificates are stored on an operating system and how that trust store supports certificate validation. I investigated how the OS keeps a list of trusted root Certificate Authorities, how to view those certificates, and how that trust affects whether a certificate is accepted or rejected. This lab helped connect the idea of a “trusted root” to real systems like browsers, servers, and secure websites.
What PKI concept or system behavior were you investigating?

---

## Steps Performed

I located the trust store for my operating system and opened the area where trusted root certificates are stored. I then reviewed the list of trusted root CAs already installed by default and selected one certificate to inspect more closely. After that, I looked at the certificate details such as subject, issuer, validity period, and fingerprint to better understand why it is trusted. Finally, I connected what I saw in the trust store to how a browser or operating system validates a website certificate during a TLS connection.
Summarize the key steps you performed to complete the lab.

Do **not copy the lab instructions**.
Describe what you actually did.

1.
2.
3.

---

## Results
Include the important outputs or findings from the lab.

Examples may include:

- Command outputs
- Certificate fields or values
- Verification results
- Screenshots (if applicable)

If you include screenshots, store them in `assets/screenshots/` at the root of your repo and reference them here.

**How to embed an image:**

**Option A — Terminal / Local Editor**

Save your screenshot to `assets/screenshots/` in your repo, then reference it using a relative path from your submission file:

```markdown
![Description of your screenshot](../../../assets/screenshots/your-filename.png)
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
