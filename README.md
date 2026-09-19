# 🛡️ DVWA Penetration Testing

A hands-on web application penetration testing project using **Damn Vulnerable Web Application (DVWA)** in a local Windows lab environment.

The project demonstrates the identification, exploitation, evidence collection, and remediation of common web application vulnerabilities.

---
# 🧠 What I Learned

### 🔐 Web Application Security

![SQL Injection](https://img.shields.io/badge/SQL%20Injection-Tested-red?style=for-the-badge)
![XSS](https://img.shields.io/badge/XSS-Tested-orange?style=for-the-badge)
![Command Injection](https://img.shields.io/badge/Command%20Injection-Tested-yellow?style=for-the-badge)
![LFI](https://img.shields.io/badge/LFI-Tested-blue?style=for-the-badge)
![File Upload](https://img.shields.io/badge/File%20Upload-Tested-purple?style=for-the-badge)
![Brute Force](https://img.shields.io/badge/Brute%20Force-Tested-red?style=for-the-badge)
![CSRF](https://img.shields.io/badge/CSRF-Tested-green?style=for-the-badge)

### 🛠️ Security Tools & Technologies

![Burp Suite](https://img.shields.io/badge/Burp%20Suite-Web%20Security-orange?style=for-the-badge)
![DVWA](https://img.shields.io/badge/DVWA-Web%20Application%20Lab-blue?style=for-the-badge)
![XAMPP](https://img.shields.io/badge/XAMPP-Lab%20Environment-FB7A24?style=for-the-badge)
![Firefox](https://img.shields.io/badge/Firefox-Browser-FF7139?style=for-the-badge)
![HTTP](https://img.shields.io/badge/HTTP-Request%20Analysis-blue?style=for-the-badge)

### 🔎 Practical Skills

![HTTP Analysis](https://img.shields.io/badge/HTTP%20Traffic-Analysis-informational?style=for-the-badge)
![Payload Testing](https://img.shields.io/badge/Payload-Testing-critical?style=for-the-badge)
![Burp Repeater](https://img.shields.io/badge/Burp%20Repeater-Testing-orange?style=for-the-badge)
![Burp Intruder](https://img.shields.io/badge/Burp%20Intruder-Brute%20Force-red?style=for-the-badge)
![Vulnerability Analysis](https://img.shields.io/badge/Vulnerability-Analysis-success?style=for-the-badge)
![Security Reporting](https://img.shields.io/badge/Security-Reporting-blueviolet?style=for-the-badge)

---

## 🎯 Project Objective

The objective of this project is to gain practical experience in:

- Web application vulnerability assessment
- Manual penetration testing
- HTTP request analysis
- Burp Suite usage
- Vulnerability exploitation in a controlled lab
- Security impact analysis
- Basic remediation recommendations
- Security documentation and reporting

---

## 🧪 Lab Environment

| Component | Details |
|---|---|
| Operating System | Windows |
| Web Server | Apache |
| Database | MySQL / MariaDB |
| Application | DVWA |
| Proxy / Testing Tool | Burp Suite |
| Browser | Firefox |
| DVWA Security Level | Low |
| Target | Localhost |

---

## 🛠️ Tools Used

- **DVWA** – Damn Vulnerable Web Application
- **Burp Suite** – Web application security testing and HTTP interception
- **Firefox** – Browser used for testing
- **XAMPP** – Apache and MySQL environment
- **Windows** – Host operating system

---

## 🔍 Vulnerabilities Tested

| # | Vulnerability | Status |
|---|---|---|
| 01 | SQL Injection (SQLi) | ✅ Completed |
| 02 | Cross-Site Scripting (XSS) | ✅ Completed |
| 03 | Command Injection | ✅ Completed |
| 04 | File Inclusion (LFI) | ✅ Completed |
| 05 | File Upload | ✅ Completed |
| 06 | Brute Force | ✅ Completed |
| 07 | Cross-Site Request Forgery (CSRF) | ✅ Completed |

---

# 📂 Project Structure

```text
DVWA-Penetration-Testing/
│
├── README.md
│
├── reports/
│   ├── sqli.md
│   ├── xss.md
│   ├── command-injection.md
│   ├── file-inclusion.md
│   ├── file-upload.md
│   ├── brute-force.md
│   └── csrf.md
│
└── screenshots/
    ├── sqli/
    ├── xss/
    ├── command-injection/
    ├── file-inclusion/
    ├── file-upload/
    ├── brute-force/
    └── csrf/
```

---

# 🧪 Testing Methodology

The following methodology was used throughout the project:

1. Configure the DVWA local testing environment.
2. Set the DVWA security level to **Low**.
3. Establish a baseline request and response.
4. Identify the vulnerable functionality.
5. Construct a controlled test payload.
6. Analyze the application response.
7. Intercept and inspect HTTP traffic using Burp Suite.
8. Capture screenshots as evidence.
9. Document the vulnerability and impact.
10. Provide basic remediation recommendations.

---

# 🔴 01. SQL Injection

### Description

SQL Injection occurs when user-controlled input is incorporated into SQL queries without proper validation or parameterization.

### Testing

A normal request was first tested using:

```text
1
```

A SQL Injection payload was then tested:

```text
1' OR '1'='1
```

The application returned multiple database records instead of a single expected record.

### Evidence

📄 [SQL Injection Report](reports/sqli.md)

Screenshots:

- `01-sqli-normal-request.png`
- `02-sqli-basic-payload.png`
- `03-sqli-burp-request.png`

---

# 🟠 02. Cross-Site Scripting (XSS)

### Description

Cross-Site Scripting allows attacker-controlled JavaScript or HTML to be reflected or executed in a victim's browser.

### Testing

A normal input was tested first:

```text
test
```

The following payload was then tested:

```html
<img src=x onerror=alert(1)>
```

The JavaScript execution was confirmed through the browser alert.

### Evidence

📄 [XSS Report](reports/xss.md)

Screenshots:

- `01-xss-normal.png`
- `02-xss-reflected.png`
- `03-xss-burp-request.png`

---

# 🟡 03. Command Injection

### Description

Command Injection occurs when user input is passed to an operating system command without proper validation.

### Testing

Baseline input:

```text
127.0.0.1
```

Test payload:

```text
127.0.0.1 && whoami
```

The command execution returned the local Windows username, demonstrating that additional operating system commands could be executed through the vulnerable input.

### Evidence

📄 [Command Injection Report](reports/command-injection.md)

Screenshots:

- `01-command-normal.png`
- `02-command-injection.png`
- `03-command-injection-burp.png`

---

# 🔵 04. File Inclusion (LFI)

### Description

Local File Inclusion (LFI) occurs when an application allows user-controlled input to determine which local file is loaded.

### Testing

A normal file was first loaded:

```text
file1.php
```

A traversal payload was then used to access the Windows system configuration file:

```text
../../../../../windows/system.ini
```

The contents of `system.ini` were displayed by the application.

### Evidence

📄 [File Inclusion Report](reports/file-inclusion.md)

Screenshots:

- `01-file-inclusion-normal.png`
- `02-file1-normal.png`
- `03-lfi-system-ini.png`
- `04-lfi-burp-request.png`

---

# 🟣 05. File Upload

### Description

Unrestricted File Upload vulnerabilities occur when an application does not properly validate uploaded files.

### Testing

A normal text file was uploaded:

```text
test.txt
```

The upload was successful and the file was accessible from the uploads directory.

A PHP file was then uploaded:

```text
test.php
```

The PHP file executed successfully when accessed through the application.

### Evidence

📄 [File Upload Report](reports/file-upload.md)

Screenshots:

- `01-normal-upload.png`
- `02-uploaded-file-access.png`
- `03-php-upload.png`
- `04-php-file-access.png`
- `05-file-upload-burp.png`

---

# 🟤 06. Brute Force

### Description

A Brute Force attack attempts multiple username and password combinations until valid credentials are identified.

### Testing

Valid credentials used in the DVWA lab:

```text
Username: admin
Password: password
```

An invalid authentication attempt was also tested:

```text
Username: admin
Password: wrongpassword
```

Burp Suite Intruder was used to send multiple password candidates.

The valid credential produced a different response length from the invalid attempts, providing a response-based indicator for identifying the successful login.

### Evidence

📄 [Brute Force Report](reports/brute-force.md)

Screenshots:

- `01-valid-login.png`
- `02-invalid-login.png`
- `03-brute-force-burp.png`
- `04-intruder-results.png`

---

# 🟢 07. Cross-Site Request Forgery (CSRF)

### Description

CSRF allows an attacker-controlled webpage to cause an authenticated user's browser to perform an unwanted action.

### Testing

A normal password change was first performed through DVWA.

The request was then inspected using Burp Suite.

A local HTML proof-of-concept page was created that submitted the password-change request while the victim browser was authenticated to DVWA.

The password change was successfully triggered through the PoC.

### Evidence

📄 [CSRF Report](reports/csrf.md)

Screenshots:

- `01-normal-password-change.png`
- `02-csrf-burp-request.png`
- `03-csrf-poc.png`
- `04-csrf-burp-poc.png`

---

# 🛡️ Remediation Summary

| Vulnerability | Recommended Mitigation |
|---|---|
| SQL Injection | Use parameterized queries / prepared statements |
| XSS | Apply context-aware output encoding and input validation |
| Command Injection | Avoid shell execution where possible; validate and allowlist input |
| LFI | Use allowlists for permitted files and prevent path traversal |
| File Upload | Validate file type, extension, content, and storage location |
| Brute Force | Implement rate limiting, account lockout controls, and MFA |
| CSRF | Use anti-CSRF tokens and appropriate cookie protections |

---

# 📊 Testing Summary

| Category | Result |
|---|---|
| SQL Injection | Vulnerable |
| Reflected XSS | Vulnerable |
| Command Injection | Vulnerable |
| Local File Inclusion | Vulnerable |
| File Upload | Vulnerable |
| Brute Force | Vulnerable |
| CSRF | Vulnerable |

All testing was performed against a deliberately vulnerable application in a controlled local lab environment.

---

# 📚 Key Learning Outcomes

Through this project, I gained hands-on experience with:

- Web application reconnaissance and testing
- SQL Injection testing
- Cross-Site Scripting
- OS command injection
- Directory traversal and LFI
- File upload security testing
- Authentication and brute-force testing
- CSRF testing
- Burp Suite HTTP interception
- Burp Suite Repeater and Intruder
- HTTP request/response analysis
- Security evidence collection
- Vulnerability documentation
- Basic vulnerability remediation

---

# ⚠️ Disclaimer

This project was performed in a controlled local lab environment using DVWA, an intentionally vulnerable web application.

The techniques demonstrated in this repository are intended for:

- Security education
- Authorized penetration testing
- CTFs
- Security research in controlled environments

Do not use these techniques against systems or applications without explicit authorization.

---

## 👨‍💻 Project

**DVWA Penetration Testing**

A practical web application security testing project demonstrating common vulnerabilities, exploitation techniques, HTTP analysis, and remediation concepts.
