# 💉 SQL Injection

## 📌 Overview

SQL Injection (SQLi) is a web application vulnerability that occurs when
user-controlled input is incorporated into SQL queries without proper
validation or parameterization.

## 🎯 Target

* Application: Damn Vulnerable Web Application (DVWA)
* Module: SQL Injection
* Security Level: Low
* Testing Environment: Local Windows Lab

## 🎯 Objective

To determine whether the DVWA SQL Injection module is vulnerable to
user-controlled SQL query manipulation.

## 🧪 Testing Methodology

A normal numeric User ID was first submitted to establish baseline
application behavior.

The input was then modified with a SQL Injection test payload to determine
whether the application's SQL query could be altered.

## 🧪 Test 1 — Baseline

### 📥 Input

```text
1
```

### 📤 Result

The application returned a single user record:

```text
ID: 1
First name: admin
Surname: admin
```

### 📸 Evidence

`01-sqli-normal-request.png`

---

## 🧪 Test 2 — SQL Injection

### 💉 Payload

```text
1' OR '1'='1
```

### 📤 Result

The application returned multiple user records, including:

```text
admin admin
Gordon Brown
Hack Me
Pablo Picasso
Bob Smith
```

This behavior indicates that the supplied input affected the SQL query

logic and bypassed the intended record filtering.

### 📸 Evidence

`02-sqli-basic-payload.png`

---

## 🕵️ Burp Suite Evidence

The SQL Injection request was captured using Burp Suite HTTP history.

The request showed the user-controlled `id` parameter being sent to the

DVWA SQL Injection endpoint.

### 📸 Evidence

`03-sqli-burp-request.png`

---

## ⚠️ Impact

SQL Injection can allow an attacker to manipulate database queries.

Depending on the application's database privileges and implementation,

this can potentially expose, modify, or delete unauthorized data.

## 🛡️ Remediation

* Use prepared statements / parameterized queries.
* Avoid constructing SQL queries through direct string concatenation.
* Validate and constrain user input.
* Apply least-privilege permissions to database accounts.
* Use appropriate server-side input handling.

## 📌 Conclusion

The DVWA SQL Injection module was successfully demonstrated to be

vulnerable at the Low security level. A crafted input caused the

application to return multiple database records instead of only the
requested record.
