# 🔐 Brute Force Authentication

## 📌 Overview

A brute-force authentication attack involves repeatedly submitting different credential combinations to an authentication endpoint in an attempt to discover valid credentials.

This test was performed against the intentionally vulnerable DVWA application running locally.

---

## 🎯 Target

* **Application:** Damn Vulnerable Web Application (DVWA)
* **Vulnerability:** Brute Force
* **Security Level:** Low
* **Environment:** Local Windows XAMPP Lab
* **Target URL:** `http://127.0.0.1/DVWA/`

---

## 🎯 Objective

The objective was to determine whether the login functionality allowed repeated authentication attempts without effective protections such as rate limiting, account lockout, or other brute-force defenses.

---

## 🧪 Step 1: Valid Login

The known DVWA credentials were submitted:

```text
Username: admin
Password: password
```

The application returned:

```text
Welcome to the password protected area admin
```

### 📸 Screenshot

---

## 🧪 Step 2: Invalid Login

An incorrect password was submitted:

```text
Username: admin
Password: wrongpassword
```

The application returned:

```text
Username and/or password incorrect.
```

### 📸 Screenshot

---

## 🕵️ Step 3: Burp Suite Request

Burp Suite was used to inspect the authentication request.

The request contained the username and password parameters:

```text
username=admin&password=wrongpassword
```

### 📸 Screenshot

---

## 🧪 Step 4: Intruder Test

The password parameter was selected as the Intruder payload position.

A small controlled password list was used:

```text
123456
admin
password
wrongpassword
```

The Intruder results showed that the `password` payload produced a different response length:

```text
password → Length: 4907
```

while the other tested passwords returned:

```text
4864
```

The different response corresponded with the known valid DVWA credential:

```text
admin:password
```

### 📸 Screenshot

---

## ✅ Vulnerability Observation

The DVWA login functionality accepted repeated authentication attempts during the controlled test.

No effective rate limiting or account lockout was observed during this small lab test.

The response difference also provided a way to distinguish the successful authentication response from unsuccessful attempts.

---

## ⚠️ Impact

Insufficient protection against repeated authentication attempts can allow attackers to systematically test password guesses.

Potential impact includes:

* Unauthorized account access
* Credential compromise
* Account takeover
* Increased risk from weak or reused passwords

---

## 🛡️ Remediation

Recommended protections include:

* Implement rate limiting for authentication attempts.
* Apply progressive delays after repeated failures.
* Consider account lockout or temporary authentication throttling where appropriate.
* Implement multi-factor authentication (MFA).
* Monitor and alert on repeated failed authentication attempts.
* Use strong password policies.
* Avoid revealing detailed differences between successful and unsuccessful authentication responses.

---

## 📌 Conclusion

The DVWA brute-force functionality was successfully tested using a controlled password list.

Burp Suite Intruder demonstrated that repeated authentication attempts could be submitted and that the successful credential produced a distinguishable response.
