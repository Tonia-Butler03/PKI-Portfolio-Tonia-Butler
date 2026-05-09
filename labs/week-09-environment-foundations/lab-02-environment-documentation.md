# Lab 02: AD CS Console Exploration & CA Hierarchy Documentation

**Student Name:** Tonia Butler
**Date Completed:**  05/08/2026
**Phase:** 2 | **Week:** 9  
**Submission Path:** `labs/week-09/lab-02-environment-documentation.md`

---

## Part A — AD CS Console Exploration (PKI-SRV01)


### CA Console Nodes — Observations

| Node | Contents / Observations |
|------|------------------------|
| Revoked Certificates | No revoked certificates present. |
| Issued Certificates | No certificates issued yet; list is currently empty. |
| Pending Requests | No pending certificate requests. |
| Failed Requests | No failed requests observed. |
| Certificate Templates | Templates available. |


### CA Properties — Key Settings

**General Tab**
- CA Name:CA Name: CVI Issuing CA 1
- Computer Name:PKI-SRV01

**Extensions Tab — CRL Distribution Points (CDP):**

```

C:\Windows\System32\CertSrv\CertEnroll\<CaName><CRLNameSuffix>

ldap:///CN=<CATruncatedName><CRLNameSuffix>,CN=<ServerShortName>,CN=CDP,CN=Public Key Services,CN=Services,CN=Configuration,DC=corp,DC=cvilab,DC=local
```

**Extensions Tab — Authority Information Access (AIA):**

```
C:\Windows\System32\CertSrv\CertEnroll\<ServerDNSName>_<CaName>

ldap:///CN=<CATruncatedName>,CN=AIA,CN=Public Key Services,CN=Services,CN=Configuration,DC=corp,DC=cvilab,DC=local
```

**Storage Tab**

- Database Path:C:\Windows\System32\CertLog  
- Log Path:C:\Windows\System32\CertLog

### Certificate Templates Console (certtmpl.msc)

Templates visible in the forest (list what you observed):

```
Administrator  
Authenticated Session  
Basic EFS  
CA Exchange  
CEP Encryption  
Code Signing  
Computer  
Directory Email Replication  
Domain Controller  
Domain Controller Authentication  
EFS Recovery Agent  
Enrollment Agent  
Exchange User  
IPSec  
Kerberos Authentication  
Key Recovery Agent  
OCSP Response Signing  
RAS and IAS Server  
Root Certification Authority  
Smartcard Logon  
Smartcard User  
Subordinate Certification Authority  
User  
Web Server  
Workstation Authentication  

```

---

## Part B — CA Hierarchy Verification (PKI-SRV01)

### Command: certutil -store -enterprise Root

```
Root "Trusted Root Certification Authorities"
================ Certificate 0 ================
Serial Number: 26373e51a6ab669340c47caef2232ce1
Issuer: CN=CVI Root CA, DC=corp, DC=cvilab, DC=local
 NotBefore: 4/25/2026 6:15 PM
 NotAfter: 4/25/2046 6:25 PM
Subject: CN=CVI Root CA, DC=corp, DC=cvilab, DC=local
CA Version: V0.0
Signature matches Public Key
Root Certificate: Subject matches Issuer
Cert Hash(sha1): b805e6ab548f6e7c57d3989f61de7fe6a51031d1
No key provider information
Cannot find the certificate and private key for decryption.
CertUtil: -store command completed successfully.

```

**What did you see?** (Subject, Issuer, Thumbprint — describe in your own words):

```
The Root store contains the CVI Root CA certificate. The Subject and Issuer are the same, indicating that it is a self-signed certificate. This confirms it is the trust anchor of the PKI hierarchy. The thumbprint uniquely identifies the Root CA certificate.
```

### Command: certutil -store -enterprise CA
```
Serial Number: 5800000002f7714edc7f317c46000000000002
Issuer: CN=CVI Root CA, DC=corp, DC=cvilab, DC=local
 NotBefore: 4/25/2026 7:26 PM
 NotAfter: 4/25/2027 7:36 PM
Subject: CN=CVI Issuing CA 1, DC=corp, DC=cvilab, DC=local
CA Version: V0.0
Certificate Template Name (Certificate Type): SubCA
Non-root Certificate
Template: SubCA, Subordinate Certification Authority
Cert Hash(sha1): 5137a597de2c3085ec5816c7f11edc18cfcdbaf8
No key provider information
Missing stored keyset
CertUtil: -store command completed successfully.
```
**What did you see?**
The CA store contains the CVI Issuing CA 1 certificate. The Subject identifies the issuing CA, while the Issuer references the CVI Root CA. This confirms that the Issuing CA certificate was signed by the Root CA, establishing the trust chain.

## Part C — Active Directory Structure (DC01)

### Active Directory Users and Computers (dsa.msc)

**PKI Admins OU — accounts found:**

```
### Active Directory Users and Computers (dsa.msc)

PKI Admins OU — accounts found:

Cert Manager  
PKI Admin  
PKI Admins (Security Group)
```

**pki.admin account — group memberships:**

```
PKI Admins group — members:

Cert Manager  
PKI Admin
```

**cert.manager account — group memberships:**

```
None
```

**Domain-joined computer accounts found:**

```
DC01  

```

### Active Directory Sites and Services (dssite.msc)

**Server registered under Default-First-Site-Name:**

```
**Server registered under Default-First-Site-Name:**

DC01
```

### Certificate Templates Console (certtmpl.msc on DC01)

Did templates appear here, confirming they are stored in AD?
- [X] Yes
- [ ] No — describe what happened:

---

## Part D — Environment Summary Write-Up

> Write this section in your own words. Cover all five areas. Aim for clarity over length.

### 1. Environment Topology

The lab environment consists of three virtual machines operating within the same internal network (corpnet). DC01 serves as the Domain Controller and is responsible for Active Directory, DNS, and overall domain services. 

PKI-SRV01 is the Issuing Certificate Authority where Active Directory Certificate Services (AD CS) is installed and actively issuing certificates. 

The Root-CA operates as the offline Root Certificate Authority and is not continuously running, which aligns with security best practices.

The IP addressing scheme is consistent across the environment:
- DC01: 192.168.10.10
- PKI-SRV01: 192.168.10.20
- Root-CA: 192.168.10.30

All systems are connected through an internal VirtualBox network, allowing controlled communication without external exposure.

### 2. CA Hierarchy

This environment follows a two-tier PKI hierarchy consisting of an offline Root CA and an online Issuing CA. The Root CA is responsible for signing the certificate of the Issuing CA, establishing the chain of trust. The Issuing CA (CVI Issuing CA 1) handles certificate issuance to users, computers, and services.

The Root CA is kept offline to reduce the risk of compromise. Since it is the trust anchor of the entire PKI, limiting its exposure significantly strengthens the overall security of the environment.


### 3. Certificate Templates
Certificate templates are stored in Active Directory and are managed across the domain. The templates observed include common enterprise templates such as:

- User
- Computer
- Web Server
- Domain Controller Authentication
- Kerberos Authentication
- Subordinate Certification Authority

These templates define how certificates are issued, including their intended purposes. For example, the Web Server template is used to issue certificates for securing web services (HTTPS), while the Computer template is used for machine authentication within the domain.


### 4. Active Directory Structure

The Active Directory environment includes a dedicated Organizational Unit (OU) named "PKI Admins," which contains the accounts and group responsible for managing PKI operations. The accounts observed include:

- PKI Admin (pki.admin)
- Cert Manager (cert.manager)
- PKI Admins (Security Group)

The PKI Admins group serves as the primary administrative boundary for PKI-related tasks. 

The pki.admin account is responsible for overall PKI configuration and administration, while the cert.manager account is used for certificate lifecycle management, such as approving or revoking certificates.

This separation of roles supports the principle of least privilege.


### 5. One Thing I Found Interesting or Unexpected
One of the most interesting observations was that certificate templates are not stored locally on the Certificate Authority server but instead are stored within Active Directory. This allows multiple systems, including both DC01 and PKI-SRV01, to access the same templates, across the environment.


---

