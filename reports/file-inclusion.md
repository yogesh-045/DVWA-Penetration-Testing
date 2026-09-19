# 📂 File Inclusion (LFI)

## 📌 Overview

File Inclusion occurs when an application uses user-controlled input to determine which file is loaded by the server.

In this lab, DVWA was configured with the **Low** security level. A Local File Inclusion (LFI) vulnerability was demonstrated by using directory traversal to access a local Windows system file.

---

## 🎯 Target

* **Application:** Damn Vulnerable Web Application (DVWA)
* **Vulnerability:** Local File Inclusion (LFI)
* **Security Level:** Low
* **Environment:** Local Windows XAMPP Lab
* **Target URL:** `http://127.0.0.1/DVWA/`

---

## 🎯 Objective

The objective was to determine whether the `page` parameter could be manipulated to load files outside the intended application directory.

---

## 🧪 Step 1: Normal File Inclusion

The application provided links to:

```text id="v5n7qk"
file1.php
file2.php
file3.php
```

The `file1.php` file was selected normally.

The application displayed:

```text id="k4m2pw"
File 1

Hello admin
Your IP address is: 127.0.0.1
```

### 📸 Screenshot

---

## 🧪 Step 2: Local File Inclusion

A directory traversal payload was supplied through the `page` parameter:

```text id="n8x3rt"
../../../../../windows/system.ini
```

The resulting request accessed:

```text id="w6c1fz"
http://127.0.0.1/DVWA/vulnerabilities/fi/?page=../../../../../windows/system.ini
```

The contents of the Windows `system.ini` file were displayed by the application.

This demonstrated that the application was able to include a local file outside the intended DVWA directory.

### 📸 Screenshot

---

## 🕵️ Step 3: Burp Suite Evidence

Burp Suite was used to inspect the HTTP request containing the directory traversal payload.

The relevant parameter was:

```text id="r2j9hs"
page=../../../../../windows/system.ini
```

### 📸 Screenshot

---

## ✅ Vulnerability Confirmation

The vulnerability was confirmed because:

1. The application accepted a user-controlled `page` parameter.
2. Directory traversal sequences were accepted.
3. A file outside the intended application directory was successfully loaded.
4. The contents of the Windows `system.ini` file were returned in the response.

---

## ⚠️ Impact

A Local File Inclusion vulnerability can potentially allow unauthorized access to files readable by the web server process.

Depending on the server configuration and application behavior, possible impact includes:

* Disclosure of configuration files
* Exposure of sensitive application information
* Disclosure of operating system files
* Exposure of credentials or secrets stored in readable files
* Potential escalation into other attacks when combined with additional vulnerabilities

---

## 🌐 Remote File Inclusion Note

The DVWA page reported that:

```text id="u7q3lm"
The PHP function allow_url_include is not enabled.
```

Therefore, Remote File Inclusion (RFI) was not demonstrated in this environment.

The testing focused on Local File Inclusion (LFI).

---

## 🛡️ Remediation

Recommended defenses include:

* Avoid using user-controlled input directly in file inclusion functions.
* Use an allowlist of permitted files.
* Map user-friendly identifiers to fixed server-side filenames.
* Reject directory traversal sequences such as `../`.
* Use secure path validation and canonicalization.
* Keep sensitive files outside web-accessible directories.
* Apply the principle of least privilege to the web server account.

---

## 📌 Conclusion

The DVWA Local File Inclusion vulnerability was successfully demonstrated.

A normal application file was first loaded, followed by a directory traversal payload that caused the application to include the Windows `system.ini` file. This confirmed that the `page` parameter could be manipulated to access local files outside the intended application directory.
