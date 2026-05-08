# Lab 01: Environment Verification & VM Connectivity Check

**Student Name:** Tonia Butler
**Date Completed:**
**Phase:** 2 | **Week:** 9
**Submission Path:** `labs/week-09-environment-foundations/lab-01-environment-verification.md`

---

## Step 1 – VM Startup & Login

**VMs started in correct order (DC01 → PKI-SRV01 → Root-CA):**

* [ ] Yes
* [ ] No — describe what happened:

**Login credentials used:**

| VM        | Account Used    | Login Successful? |
| --------- | --------------- | ----------------- |
| DC01      | CORP\pki.admin  | Yes / No          |
| PKI-SRV01 | CORP\pki.admin  | Yes / No          |
| Root-CA   | .\Administrator | Yes / No          |

**Notes / issues encountered:**

```
(enter notes here)
```

---

## Step 2 – VM Connectivity Test

**Command run on PKI-SRV01:**

```powershell
Test-Connection -ComputerName DC01 -Count 2
```

**Output received:**

```
(paste your output here)
```

**DC01 responded successfully:**

* [ ] Yes
* [ ] No — troubleshooting steps taken:

---

## Step 3 – CertSvc Service Status
The CertSvc (Active Directory Certificate Services) service was verified to be running on PKI-SRV01. This confirms that the Certificate Authority is operational and capable of issuing and managing certificates.

**Command run on PKI-SRV01:**

```powershell
Get-Service -Name CertSvc
```

**Output received:**

```
(paste your output here)
```

**CertSvc status shown:** ________________

**Service was Running:**

* [ ] Yes
* [ ] No — action taken:

---

## Step 4 – Certification Authority Console

Confirmed CA name visible: CVI Issuing CA 1  
Confirmed CA status: Running  

The Certification Authority console (certsrv.msc) opened successfully. 
The CA was visible with a healthy status indicator, confirming that the PKI server is properly configured and operational. 
The console displayed standard CA folders including Issued Certificates, Revoked Certificates, and Pending Requests.
**Steps completed on PKI-SRV01:**

* [ ] Opened certsrv.msc via Run dialog
* [ ] Confirmed CA name visible: ________________
* [ ] Confirmed CA status: ________________
* [ ] Expanded left pane — folders visible (Revoked Certificates, Issued Certificates, etc.)

**Screenshot or description of what you observed in certsrv.msc:**

```
(describe or reference your screenshot here)
```

---

## Step 5 – Certificate Log File Path

**Command run on PKI-SRV01:**

```powershell
Get-ChildItem "C:\Windows\System32\CertLog"
```

**Output received:**

```
(paste your output here)
```

**Files found in CertLog:**

| File Name                | Approximate Size |
|-------------------------|------------------|
| CVI Issuing CA 1.edb    | ~1 MB            |
| CVI Issuing CA 1.jfm    | ~16 KB           |
| edb.chk                 | ~8 KB            |
| edb.log                 | ~1 MB            |
| edbres00001.jrs         | ~1 MB            |
| edbres00002.jrs         | ~1 MB            |
| edbtmp.log              | ~1 MB            |
| tmp.edb                 | ~20 KB           |

| File Name | Approximate Size |
| --------- | ---------------- |
|           |                  |
|           |                  |

---

## Reflection

**One thing that went well during this lab:**

```
(your response here)
```

**One thing that was confusing or unexpected:**

```
(your response here)
```

---

## Submission Checklist

* [ ] All five steps completed
* [ ] All command outputs pasted
* [ ] Reflection section filled in
* [ ] File saved as `lab-01-environment-verification.md`
* [ ] File committed to my portfolio repo under `labs/week-09-environment-foundations/`
