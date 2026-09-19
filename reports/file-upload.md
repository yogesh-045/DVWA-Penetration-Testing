# 📤 Unrestricted File Upload

## 📌 Overview

An unrestricted or insufficiently validated file upload vulnerability occurs when an application allows users to upload files without adequately validating their type, extension, content, or execution behavior.

In this lab, DVWA was configured with the **Low** security level. A normal text file and a PHP file were uploaded successfully.

---

## 🎯 Target

* **Application:** Damn Vulnerable Web Application (DVWA)
* **Vulnerability:** Unrestricted File Upload
* **Security Level:** Low
* **Environment:** Local Windows XAMPP Lab
* **Target URL:** `http://127.0.0.1/DVWA/`

---

## 🎯 Objective

The objective was to determine whether the application properly validates uploaded files and restricts potentially executable file types.

---

## 🧪 Step 1: Normal File Upload

A benign text file named:

```text id="w4r8n2"
test.txt
```

was uploaded through the File Upload functionality.

The application returned:

```text id="p7k3m1"
../../hackable/uploads/test.txt successfully uploaded!
```

### 📸 Screenshot

---

## 🧪 Step 2: Verify Uploaded File

The uploaded text file was accessed through the upload directory:

```text id="n5x2q9"
http://127.0.0.1/DVWA/hackable/uploads/test.txt
```

The uploaded file content was displayed successfully.

### 📸 Screenshot

---

## 🧪 Step 3: PHP File Upload

A simple PHP test file named:

```text id="c6v1t8"
test.php
```

was created with the following content:

```php id="z3h7k4"
<?php
echo "DVWA PHP Upload Test";
?>
```

The file was uploaded through the same upload functionality.

The application returned:

```text id="m9q2s5"
../../hackable/uploads/test.php successfully uploaded!
```

### 📸 Screenshot

---

## 🧪 Step 4: PHP File Access

The uploaded PHP file was accessed through:

```text id="r8f4p2"
http://127.0.0.1/DVWA/hackable/uploads/test.php
```

The PHP code executed and displayed:

```text id="y6k1w3"
DVWA PHP Upload Test
```

### 📸 Screenshot

---

## 🕵️ Step 5: Burp Suite Evidence

Burp Suite was used to inspect the HTTP multipart upload request.

The request contained the uploaded filename:

```text id="q2j7v5"
filename="test.php"
```

### 📸 Screenshot

---

## ✅ Vulnerability Confirmation

The vulnerability was confirmed because:

1. A normal text file could be uploaded.
2. The uploaded file was accessible from the upload directory.
3. A PHP file could also be uploaded without being blocked.
4. The uploaded PHP file was interpreted and executed by the server.

---

## ⚠️ Impact

An unrestricted file upload vulnerability can potentially allow an attacker to upload files that may be interpreted or executed by the server.

Depending on server configuration and application privileges, possible impact includes:

* Unauthorized code execution
* Modification of application files
* Access to sensitive information
* Defacement
* Further compromise of the affected application or server

---

## 🛡️ Remediation

Recommended defenses include:

* Allow only explicitly permitted file types.
* Validate file extensions using an allowlist.
* Validate the actual file content and MIME type.
* Rename uploaded files to server-generated filenames.
* Store uploaded files outside the executable web root where possible.
* Disable script execution in upload directories.
* Apply appropriate filesystem permissions.
* Enforce upload size limits.
* Reject files with executable extensions such as `.php` when they are not required.

---

## 📌 Conclusion

The DVWA File Upload vulnerability was successfully demonstrated.

The application accepted both a benign text file and a PHP file. The PHP file was subsequently accessible and interpreted by the server, demonstrating the security impact of insufficient upload validation in the configured Low security environment.
