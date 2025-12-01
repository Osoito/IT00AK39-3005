# 1️⃣ Introduction

**Tester(s):**  
- Name:  Chen Zhu

**Purpose:**  
- Identify vulnerabilities in registration and authentication flows.

**Scope:**  
- Tested components:  Registration page of Booking system
- Exclusions:  Login and post-authentication functionalities (not accessible in test environment) 
- Test approach: Gray-box

**Test environment & dates:**  
- Start:  24.11.2025
- End:  25.11.2025
- Test environment details (OS, runtime, DB, browsers): Windows OS, Edge browser, Docker container (lohalhost:8000)

**Assumptions & constraints:**  
- None

---

# 2️⃣ Executive Summary

**Short summary (1-2 sentences):**  The registration of the system is lacking validation features in backend and frontend. The password storage is lacking hashing and is now in plaintext.

**Overall risk level:** High

**Top 5 immediate actions:**  
1.  Password validation to disallow unsecure passwords
2.  Backend validation for form inputs to ensure legit data (Currently it's either only in frontend and can be overpassed, or not implemented in frontend neither like DOB)
3.  Remove authority for user to choose their role during registrationf
4.  Password hashing in its storage
5.  DOB validation to suit system needs (to be over 15 years old, and to be legal date)

---

# 3️⃣ Severity scale & definitions

|  **Severity Level**  | **Description**                                                                                                              | **Recommended Action**           |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|      🔴 **High**     | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | *Immediate fix required*         |
|     🟠 **Medium**    | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF).                              | *Fix ASAP*                       |
|      🟡 **Low**      | A minor issue or configuration weakness (e.g., server version disclosure).                                                   | *Fix soon*                       |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers).                                            | *Monitor and fix in maintenance* |


---

# 4️⃣ Findings (filled with examples → replace)

> Fill in one row per finding. Focus on clarity and the most important issues.

| ID | Severity | Finding | Description | Evidence / Proof |
|------|-----------|----------|--------------|------------------|
| F-01 | 🔴 High | Privilege Escalation via Role Selection | Users can select "administrator" role during registration. | ![alt text](.\proof1.png) |
| F-02 | 🟡 Low | Weak Password Handling | System accepts weak passwords (e.g., "123") |![alt text](.\proof3.png) |
| F-03 | 🟡 Low | Email Validation | Emails should be verified. | ![alt text](.\proof3.png) |
| F-04 | 🟡 Low | Birth Date Lack Validation | Accepts dates that make user underage or illegal date (e.g., future date) | ![alt text](.\proof3.png) |
| F-05 | 🔴 High | Password Storage Lack Hashing | Passwords are stored in plaintext | ![alt text](.\proof5.png) |

---

> [!NOTE]
> Include up to 5 findings total.   
> Keep each description short and clear.

---

# 5️⃣ OWASP ZAP Test Report (Attachment)

**Purpose:**  
- Attach or link your OWASP ZAP scan results (Markdown format preferred).

Link: [ZAPreport](./zap_report_round1.md)

---

**Instructions (CMD version):**
1. Run OWASP ZAP baseline scan:  
   ```bash
   zap-baseline.py -t https://example.com -r zap_report_round1.html -J zap_report.json
   ```
2. Export results to markdown:  
   ```bash
   zap-cli report -o zap_report_round1.md -f markdown
   ```
3. Save the report as `zap_report_round1.md` and link it below.

---
> [!NOTE]
> 📁 **Attach full report:** → `check itslearning` → **Add a link here**

---