### 📌 **FTP Server Return Codes Overview**

FTP return codes are **three-digit** responses where:

#### **First Digit – Response Type**

| Range | Meaning                                                               |
| ----- | --------------------------------------------------------------------- |
| `1xx` | **Positive Preliminary** – Action starting; expect another reply.     |
| `2xx` | **Positive Completion** – Action completed, ready for next command.   |
| `3xx` | **Positive Intermediate** – Awaiting further info to complete action. |
| `4xx` | **Transient Negative** – Temporary failure; retry same command later. |
| `5xx` | **Permanent Negative** – Command failed; retry discouraged.           |
| `6xx` | **Protected Reply** – Secured (Base64) messages per RFC 2228.         |

#### **Second Digit – Functional Group**

|Range|Category|
|---|---|
|`x0x`|**Syntax** errors or unrecognized commands.|
|`x1x`|**Information** or help replies.|
|`x2x`|**Connections** (data/control).|
|`x3x`|**Authentication/accounting**.|
|`x4x`|_Unspecified in RFC 959_.|
|`x5x`|**File system** operations.|

---

### ✅ **Full List of FTP Status Codes**

#### **1xx – Preliminary**

- `110`: Restart marker reply.
    
- `120`: Service ready in `nnn` minutes.
    
- `125`: Data connection open; transfer starting.
    
- `150`: File status okay; opening data connection.
    

#### **2xx – Completion**

- `202`: Command not implemented.
    
- `211`: System status.
    
- `212`: Directory status.
    
- `213`: File status.
    
- `214`: Help message.
    
- `215`: System type (e.g., UNIX).
    
- `220`: Service ready for new user.
    
- `221`: Control connection closing.
    
- `225`: Data connection open; no transfer.
    
- `226`: Closing data connection; action completed.
    
- `227`: Entering Passive Mode.
    
- `228`: Entering Long Passive Mode.
    
- `229`: Entering Extended Passive Mode.
    
- `230`: User logged in.
    
- `232`: User logged in (secure).
    
- `234`: Security mechanism accepted (no data needed).
    
- `235`: Security data accepted (no further data needed).
    
- `250`: Requested action completed.
    

#### **3xx – Intermediate**

- `331`: Username OK, need password.
    
- `332`: Need account for login.
    
- `334`: Security mechanism accepted; data required.
    
- `336`: Username/password OK; challenge follows.
    

#### **4xx – Transient Errors**

- `421`: Service not available; closing connection.
    
- `425`: Can't open data connection.
    
- `426`: Connection closed; transfer aborted.
    
- `430`: Invalid credentials.
    
- `431`: Missing resource for security processing.
    
- `434`: Host unavailable.
    
- `450`: File action not taken.
    
- `451`: Action aborted (local error).
    
- `452`: Insufficient storage; file unavailable.
    

#### **5xx – Permanent Errors**

- `500`: Syntax error, command unrecognized.
    
- `501`: Syntax error in parameters.
    
- `502`: Command not implemented.
    
- `503`: Bad command sequence.
    
- `504`: Command not implemented for parameter.
    
- `530`: Not logged in.
    
- `532`: Need account for storing files.
    
- `533–537`: Security or policy-related denials.
    
- `550`: File unavailable.
    
- `551`: Page type unknown.
    
- `552`: Exceeded storage allocation.
    
- `553`: Invalid file name.
    

#### **6xx – Protected Replies**

- `631`: Integrity protected.
    
- `632`: Confidentiality + Integrity protected.
    
- `633`: Confidentiality protected only.
    

---
