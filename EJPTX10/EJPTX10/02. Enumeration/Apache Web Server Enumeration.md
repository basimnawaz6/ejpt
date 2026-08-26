
# 🧪 Apache Enumeration using Metasploit Framework

This lab demonstrates how to perform **Apache enumeration** on a target machine using multiple **Metasploit auxiliary scanner modules**.

---

## **Step 1 — Access the Kali Machine**

- Open the lab link to access the **Kali machine**.
    

---

## **Step 2 — Check Target Reachability**

**Command:**

```bash
ping -c 5 victim-1
```

✅ The target `victim-1` is reachable.

---

## **Step 3 — Start the Metasploit Framework Console**

**Command:**

```bash
msfconsole -q
```

---

## **Step 4 — Run Metasploit Auxiliary HTTP Scanner Modules**

---

### 🔹 Module 1: HTTP Version Scanner

**Path:** `auxiliary/scanner/http/http_version`

**Commands:**

```bash
use auxiliary/scanner/http/http_version
set RHOSTS victim-1
run
```

---

### 🔹 Module 2: robots.txt Scanner

**Path:** `auxiliary/scanner/http/robots_txt`

**Commands:**

```bash
use auxiliary/scanner/http/robots_txt
set RHOSTS victim-1
run
```

---

### 🔹 Module 3: HTTP Header Scanner

**Path:** `auxiliary/scanner/http/http_header`

**Commands:**

```bash
use auxiliary/scanner/http/http_header
set RHOSTS victim-1
run
```

**Optional (Scan a specific path):**

```bash
use auxiliary/scanner/http/http_header
set RHOSTS victim-1
set TARGETURI /secure
run
```

---

### 🔹 Module 4: Directory Brute Force Scanner

**Path:** `auxiliary/scanner/http/brute_dirs`

**Commands:**

```bash
use auxiliary/scanner/http/brute_dirs
set RHOSTS victim-1
run
```

---

### 🔹 Module 5: Directory Scanner

**Path:** `auxiliary/scanner/http/dir_scanner`

**Commands:**

```bash
use auxiliary/scanner/http/dir_scanner
set RHOSTS victim-1
set DICTIONARY /usr/share/metasploit-framework/data/wordlists/directory.txt
run
```

---

### 🔹 Module 6: Directory Listing Scanner

**Path:** `auxiliary/scanner/http/dir_listing`

**Commands:**

```bash
use auxiliary/scanner/http/dir_listing
set RHOSTS victim-1
set PATH /data
run
```

---

### 🔹 Module 7: Files Directory Scanner

**Path:** `auxiliary/scanner/http/files_dir`

**Commands:**

```bash
use auxiliary/scanner/http/files_dir
set RHOSTS victim-1
set VERBOSE false
run
```

---

### 🔹 Module 8: HTTP PUT Method Scanner

**Path:** `auxiliary/scanner/http/http_put`

**Upload a file to target:**

```bash
use auxiliary/scanner/http/http_put
set RHOSTS victim-1
set PATH /data
set FILENAME test.txt
set FILEDATA "Welcome To AttackDefense"
run
```

**Verify uploaded file:**

```bash
wget http://victim-1:80/data/test.txt
cat test.txt
```

**Delete the uploaded file:**

```bash
use auxiliary/scanner/http/http_put
set RHOSTS victim-1
set PATH /data
set FILENAME test.txt
set ACTION DELETE
run
```

**Verify deletion (should return 404):**

```bash
wget http://victim-1:80/data/test.txt
```

---

### 🔹 Module 9: HTTP Login Scanner

**Path:** `auxiliary/scanner/http/http_login`

**Commands:**

```bash
use auxiliary/scanner/http/http_login
set RHOSTS victim-1
set AUTH_URI /secure/
set VERBOSE false
run
```

---

### 🔹 Module 10: Apache User Directory Enumeration

**Path:** `auxiliary/scanner/http/apache_userdir_enum`

**Commands:**

```bash
use auxiliary/scanner/http/apache_userdir_enum
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set RHOSTS victim-1
set VERBOSE false
run
```

---

