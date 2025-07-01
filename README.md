# VAPT Report on Credential Security in Windows 10 Based Healthcare Infrastructure

### This report documents a simulated internal VAPT engagement targeting Windows 10 systems to assess credential storage risks via SAM enumeration and NTLM hash cracking.

## **🔐 Introduction:**

In the ever-evolving landscape of cybersecurity, even the most fundamental components of an operating system—like user account management—can become serious liabilities if left unguarded. In this writeup, I take you through a real-world red team simulation where the objective was to evaluate how easily an internal adversary could gain access to user credentials from a Windows 10-based system using local enumeration, password dumping, and brute-force techniques.

This hands-on assessment mimicked a post-exploitation scenario inside a healthcare-oriented infrastructure—one of the most targeted industries today. What followed was a detailed Vulnerability Assessment and Penetration Testing (VAPT) exercise involving enumeration of SAM files, NTLM hash extraction, and offline password cracking using Cain and Abel. The results highlight just how crucial it is for enterprises to adopt strong password policies, enforce multi-factor authentication, and align with industry-grade frameworks like NIST and ISO/IEC 27001.

Let’s dive into the technicals and findings 👇

---

# Vulnerability Assessment and Penetration Testing (VAPT) Report

## Target: Windows 10 Host Machine (Healthcare Infrastructure)

**Prepared by:** Aditya Bhatt <br/>
**Designation:** VAPT Analyst | Cybersecurity Professional <br/>
**Contact:** [info.adityabhatt3010@gmail.com](mailto:info.adityabhatt3010@gmail.com) | +91-9818993884 <br/>

---

## Executive Summary

This report presents a comprehensive vulnerability assessment and penetration testing exercise conducted on a Windows 10-based host environment used within a healthcare infrastructure. The core objective was to simulate a realistic insider threat scenario where unauthorized access to user credentials via the SAM (Security Account Manager) database could potentially compromise sensitive medical data. Various enumeration and attack methodologies were used including SAM hash extraction, NTLM hash enumeration, and dictionary-based password cracking using well-known open-source tools.

The findings reinforce the critical importance of robust password policies, access controls, and multi-factor authentication within legacy environments. Immediate mitigation measures and long-term strategic recommendations have been provided to harden the target infrastructure.

---

## Introduction

Legacy operating systems and internal endpoints remain a major attack surface in healthcare and logistics sectors. This project focused on emulating a malicious internal actor attempting to escalate privileges and gain access to sensitive account credentials via the local SAM database on a Windows 10 virtual machine.

The report encapsulates:

* Reconnaissance and enumeration
* Hash extraction from SAM
* NTLM hash cracking via Cain & Abel
* Recommendations based on modern standards (NIST, ISO)

---

## Objectives

* Enumerate local user accounts via SAM database.
* Extract and crack NTLM hashes using dictionary attacks.
* Demonstrate post-exploitation risks due to weak passwords.
* Provide actionable defense recommendations.

---

## Methodology

### Task 1: Reconnaissance and Environment Setup

* **Identified Host Machine:**
  IP: `192.168.178.142`
  Subnet Mask: `255.255.255.0`

* **Command Used:**

  ```bash
  ipconfig
  ```

* **SAM Database Location Identified:**
  `C:\Windows\System32\config\SAM`

---

### Task 2: Installation & Configuration of Cracking Tools

* **Tools Used:**

  * WinPcap
  * Cain & Abel

* **Steps:**

  1. Install dependencies (WinPcap).
  2. Install Cain & Abel and configure DNS settings.
  3. Disable IPv6 to prevent DNS registration issues.
  4. Navigate to Cain & Abel → Cracker → Import Local Hashes.

---

### Task 3: NTLM Hash Enumeration & Cracking

* NTLM hashes of local users were successfully extracted.
* Dictionary-based attacks were performed on the extracted hashes.
* Tools used: Cain & Abel’s internal dictionary attack engine.

#### **Attack Steps:**

1. Right-click user → NTLM Hashes → Dictionary Attack.
2. Load custom wordlist.
3. Execute and monitor the cracking process.
4. Retrieve cracked passwords from result table.

---

## Findings

* NTLM hashes were successfully extracted and cracked.
* Multiple weak passwords were identified using common dictionary terms.
* No account lockout mechanisms observed during brute force attempts.
* NTLM hash storage without sufficient salting increases risk exposure.

---

## Risk Analysis

| Risk                         | Impact | Likelihood | Risk Score |
| ---------------------------- | ------ | ---------- | ---------- |
| Password Cracking via NTLM   | High   | High       | Critical   |
| Lack of MFA                  | High   | Medium     | High       |
| Absence of Password Rotation | Medium | High       | High       |
| Insecure SAM Access          | High   | Medium     | High       |

---

## Recommendations

### 1. **Password Policy Enforcement**

* Enforce complexity (minimum 12–14 characters).
* Include uppercase, lowercase, digits, and special characters.
* Disallow dictionary words and personal identifiers.

### 2. **Password History & Reuse Prevention**

* Maintain password history (last 8-10 versions).
* Enforce unique passwords across systems.

### 3. **Password Expiration**

* Trigger mandatory resets post-breach or policy violations.
* Avoid forced rotations unless necessary.

### 4. **Multi-Factor Authentication (MFA)**

* Implement MFA for all user accounts.
* Utilize OTP apps, biometric verification, or hardware tokens.

### 5. **Secure Password Storage**

* Use salted hashes with Bcrypt, PBKDF2, or Scrypt.
* Never store passwords in plaintext or logs.

### 6. **User Education**

* Promote passphrases over complex sequences.
* Conduct phishing awareness training.
* Encourage the use of password managers.

### 7. **Monitoring and Auditing**

* Enable failed login tracking and lockout thresholds.
* Use tools like “Have I Been Pwned” to detect exposed credentials.

### 8. **Compliance with Standards**

* Align policies with:

  * **ISO/IEC 27001** (Access Control)
  * **NIST SP 800-63B** (Digital Identity Guidelines)
  * **CIS Controls (v8)** (MFA and Password Handling)

---

## Conclusion

The simulation exposed significant security gaps in the current Windows 10 host deployment. Despite the outdated tooling used in this exercise, the fact that local hashes were easily crackable underscores the urgent need for strong password hygiene and multi-factor authentication enforcement. Organizations operating in healthcare or logistics must harden their endpoints, follow security best practices, and continuously monitor credential handling mechanisms to prevent internal breaches.

---

## **🛡️ Final Thoughts:**

The exercise served as a strong reminder that passwords—often treated as trivial—can become the softest entry point for attackers, especially in legacy environments. By following best practices in password hygiene, MFA adoption, and monitoring, organizations can drastically reduce the attack surface that hackers love to exploit.

Security isn’t just about firewalls or tools—it’s about posture, policy, and awareness. And sometimes, all it takes is one cracked password to bring it all crashing down.

Thanks for reading. If you found this insightful, do share it with your fellow cybersecurity folks and drop a comment.
For more writeups like this, follow me on GitHub and Medium — I regularly break things (ethically) and document the lessons.

---
