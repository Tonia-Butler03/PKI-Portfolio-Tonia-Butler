Week 3 Lab 04 — Certificate Misconfiguration Analysis
Scenario 1 — Missing Subject Alternative Name (SAN)

Question:
Would modern browsers trust this certificate?

Answer:
No, modern browsers would not trust this certificate.

Analysis:
Modern browsers require the Subject Alternative Name (SAN) because it is the field used to verify the website. Without a SAN, the browser cannot confirm the identity of the server, so the certificate fails validation.

Fix:
Reissue the certificate with a valid SAN that includes the correct domain name.

Scenario 2 — Incorrect Extended Key Usage (EKU)

Question:
Would a browser accept this certificate for a web server?

Answer:
No, the browser would not accept this certificate.

Analysis:
Extended Key Usage (EKU) defines what the certificate is allowed to be used for. In this scenario, the certificate is only valid for client authentication. HTTPS requires "TLS Web Server Authentication," so the browser will reject the certificate because it is being used for the wrong purpose.

Fix:
Reissue the certificate with the correct EKU, including Server Authentication.

Scenario 3 — Expired Certificate

Question:
What happens if this certificate is used today?

Answer:
The certificate will fail validation and the browser will show a security warning.

Analysis:
Certificates are only valid within their date range. Once the expiration date passes, the certificate is no longer trusted. This prevents the use of outdated or potentially compromised certificates. Certificate lifecycle management is important to ensure certificates are renewed before they expire.

Fix:
Renew or replace the certificate with a valid, non-expired one.

Scenario 4 — Missing Intermediate Certificate

Question:
What error would a browser likely display?

Answer:
The browser would show an error such as "certificate not trusted" or "incomplete certificate chain."

Analysis:
Certificate chains establish trust by linking the server certificate to a trusted root CA through intermediate certificates. If the intermediate certificate is missing, the browser cannot complete the chain of trust. Even if the server certificate is valid, the connection will fail because the trust path is broken.

Fix:
Configure the server to include the full certificate chain, including intermediate certificates.


