# Week 01 Mini Lab — Trust Chain Validation

## Screenshot Evidence

Capture a screenshot of the Certification Path (certificate chain) from your browser.

Save it as:

assets/screenshots/week-01/trust-chain-validation.png

Embed the screenshot below:

![Trust Chain Validation](../../assets/screenshots/week-01/trust-chain-validation.png)


## Website Information

**Website inspected:**  
https://www.homedepot.com/


## Certificate Chain Breakdown

**Leaf (Server) Certificate**  
<!-- Enter Common Name or Subject -->
www.homedepot.com

**Intermediate Certificate Authority**
<!-- Enter Intermediate CA name -->
Fortinet

**Root Certificate Authority (Trust Anchor)**
Certificate Authority Digicert

---

## Trust Anchor Verification

Is the Root CA marked as trusted by your system?

<!-- Yes 

If yes, explain where that trust comes from (OS/browser root store).
Trust is established in the fortnit is the intermidiate that issue certificates, inspect SSL/TLS traffic. Since it's a thrid party firewallc the trust is established becasue it is built within the sytem.

If no, explain what warning or behavior occurred.

---

## Observations

Document three observations about the certificate.

### Observation 1
<!-- What did you notice about the chain structure? -->

### Observation 2
<!-- What did you notice about the Root CA? -->

### Observation 3
<!-- What did you notice about how the browser determines trust? -->

---

## Reflection

In 3–5 sentences, explain:
- Why the Root certificate is called a trust anchor
- How validation walks the certificate chain
- What would happen if the Root CA were not trusted

Use your own words.
