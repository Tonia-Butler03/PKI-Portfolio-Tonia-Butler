# Lab 01: Environment Verification & VM Connectivity Check

**Student Name:** Tonia Butler
**Date Completed:**
**Phase:** 2 | **Week:** 9
**Submission Path:** `labs/week-09-environment-foundations/lab-01-environment-verification.md`

---

## Step 1 – VM Startup & Login

**VMs started in correct order (DC01 → PKI-SRV01 → Root-CA):**

* [x ] Yes
* [ ] No — describe what happened:

**Login credentials used:**

| VM        | Account Used    | Login Successful? |
| --------- | --------------- | ----------------- |
| DC01      | CORP\pki.admin  | Yes        
| PKI-SRV01 | CORP\pki.admin  | Yes          
| Root-CA   | .\Administrator | Yes          

**Notes / issues encountered:**
Initial setup required troubleshooting network configuration. The VMs initially had incorrect IP settings and network adapter issues, which prevented connectivity between systems. These issues were resolved by correctly configuring static IP addresses and ensuring both VMs were on the same network.
```

```

---

## Step 2 – VM Connectivity Test

**Command run on PKI-SRV01:**

```powershell
Test-Connection -ComputerName DC01 -Count 2
```

**Output received:**

Source        Destination     IPV4Address     Bytes    Time(ms)
------        -----------     -----------     -----    --------
PKI-SRV01     192.168.10.10   192.168.10.10   32       1
PKI-SRV01     192.168.10.10   192.168.10.10   32       1

**DC01 responded successfully:**

* [ x] Yes
* [ ] No — troubleshooting steps taken:

---

## Step 3 – CertSvc Service Status
The CertSvc (Active Directory Certificate Services) service was verified to be running on PKI-SRV01. This confirms that the Certificate Authority is operational and capable of issuing and managing certificates.

**Command run on PKI-SRV01:**

```powershell
Get-Service -Name CertSvc
```

**Output received:**

Status   Name     DisplayName
------   ----     -----------
Running  CertSvc  Active Directory Certificate Services


**CertSvc status shown:** Running

**Service was Running:**

* [X ] Yes
* [ ] No — action taken:

---

## Step 4 – Certification Authority Console

Confirmed CA name visible: CVI Issuing CA 1  
Confirmed CA status: Running  

The Certification Authority (certsrv.msc) opened successfully. 
The CA was visible with a healthy status indicator, confirming that the PKI server is properly configured and operational. 
The console displayed standard CA folders including Issued Certificates, Revoked Certificates, and Pending Requests.

**Steps completed on PKI-SRV01:**

* [x ] Opened certsrv.msc via Run dialog
* [x] Confirmed CA name visible: CVI Issuing CA 1
* [x] Confirmed CA status: Running
* [x] Expanded left pane — folders visible (Revoked Certificates, Issued Certificates, etc.)

**Screenshot or description of what you observed in certsrv.msc:**
The Certification Authority console displayed "CVI Issuing CA 1" with a green status indicator, confirming the CA is operational. The console included standard folders such as Issued Certificates, Revoked Certificates, Pending Requests, and Failed Requests.



---

## Step 5 – Certificate Log File Path

**Command run on PKI-SRV01:**

```powershell
Get-ChildItem "C:\Windows\System32\CertLog"
```

**Output received:**


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



---

## Reflection

**One thing that went well during this lab:**

```
Once the network configuration was corrected, the environment functioned as expected. I was able to successfully verify connectivity, confirm services were running, and access the Certification Authority console.
```

**One thing that was confusing or unexpected:**

```
It was initially confusing understanding the difference between running commands on my local machine versus inside the virtual machine. Additionally, network configuration issues such as IP conflicts and incorrect adapters required troubleshooting before connectivity could be established.
```

---

## Submission Checklist

* [x] All five steps completed
* [x] All command outputs pasted
* [x] Reflection section filled in
* [x] File saved as `lab-01-environment-verification.md`
* [x] File committed to my portfolio repo under `labs/week-09-environment-foundations/`
