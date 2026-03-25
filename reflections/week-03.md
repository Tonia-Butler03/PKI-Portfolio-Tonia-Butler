# Week 3 Reflection

---

## Prompts

1. What did you learn this week?

This week I learned how certificate validation actually works and why small misconfigurations can break TLS connections. I focused on things like SAN, EKU, expiration, and certificate chains and how each one plays a role in trust. It helped me understand that certificates are not just created, they have to be correctly configured to work. Overall, I now see how validation is what enforces security in PKI.

2. What concept was most challenging?
   
The most challenging concept was understanding how all the certificate fields and extensions work together during validation. It was a lot to keep track of between SAN, EKU, and the certificate chain. At first, it felt like small details, but I realized each one has a specific purpose. Once I connected each field to a validation rule, it started to make more sense.

3. Where does this concept appear in real-world systems?
This concept appears anytime we use HTTPS, access secure websites, or connect to systems that require encryption. Browsers, APIs, enterprise systems all rely on certificate validation to establish trust. Misconfigurations like expired certificates or missing intermediates can cause outages. This is why companies have strict certificate management processes and PKI skills are valuable. 
   
4. How would you explain this topic to a non-technical audience?
I would explain it as a a process to verify that a website or system is really who it says it is before sharing any information. Certificates are like digital IDs, and the system checks them before allowing a secure connection. If something is missing or incorrect, the system blocks the connection to keep you safe. It’s similar to showing proper identification before entering a secure building or a club. 
   
7. What questions remain?

I still want to understand more about how certificate management. I’m also curious about how tools automatically monitor and renew certificates before they expire. Another area I want to explore is how misconfigurations are detected in real time. Overall, I want to get more hands-on with troubleshooting real certificate issues.


## Professional Growth Check

- Did you document clearly? Yes
- Did you use structured formatting? Yes
- Was your commit message meaningful? Yes
