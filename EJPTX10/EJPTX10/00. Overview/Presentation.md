

---

# 1. Explain the architecture of your Active Directory environment.

### 

Our environment consists of:

- One Windows Server named **NCAI-DC01**
    
- The server is the **Domain Controller** and also runs **DNS**.
    
- The domain is **ncai.local**.
    
- One Windows client named **NCAI-WS01** joined to the domain.
    
- Users, Groups, and Organizational Units are managed from the Domain Controller.
    

### Whiteboard Diagram

```
             NCAI.local

          NCAI-DC01
      (AD DS + DNS Server)
              |
        ----------------
        |
     NCAI-WS01
    (Domain Client)
```

---

# 2. Why is DNS essential in Active Directory?



DNS is responsible for helping computers locate the Domain Controller.

When a user logs in:

1. The client asks DNS where the Domain Controller is.
    
2. DNS returns the Domain Controller's IP address.
    
3. The client contacts the Domain Controller.
    
4. Authentication occurs using Kerberos.
    

If DNS is not working:

- Users cannot log in.
    
- Computers cannot join the domain.
    
- Active Directory services fail.
    

---

# 3. Show one user and one security group you created.



User:

```
Ahmed Khan
```

OU:

```
SOC
```

Security Group:

```
GG-SOC-Analysts
```

### Why?

Ahmed works in the Security Operations Center.

Instead of assigning permissions directly to Ahmed, we assign him to the SOC group.

Then permissions are assigned to the group.

This makes management easier.

---

# 4. Demonstrate how Windows joined the domain.

### Steps

1. Install Windows.
    
2. Rename the computer to:
    

```
NCAI-WS01
```

3. Configure Preferred DNS to point to the Domain Controller.
    
4. Open System Properties.
    
5. Click Change.
    
6. Join:
    

```
ncai.local
```

7. Enter Domain Administrator credentials.
    
8. Restart.
    
9. Log in using a domain account.
    

### Verification

Run:

```
whoami
```

or

```
systeminfo
```

The computer should display:

```
Domain: ncai.local
```

---

# 5. Why do organizations use Organizational Units (OUs)?

### Expected Answer

OUs help organize users and computers by department.

Benefits:

- Easier management
    
- Apply Group Policies
    
- Delegate administration
    
- Better organization
    

Example:

```
NCAI

├── SOC
├── HR
├── Finance
├── Red Team
├── Blue Team
```

Instead of keeping hundreds of users in one folder, departments remain organized.

---

# 6. Explain the CompanyData permissions.

### Configuration

```
GG-IT-Admins
Full Control

GG-SOC-Analysts
Read

Everyone
Removed
```

### Why?

IT Administrators manage the files.

SOC only needs to read logs and reports.

Everyone is removed to prevent unauthorized access.

This follows the Principle of Least Privilege.

---

# 7. A new SOC employee joins tomorrow.

### What would you do?

Create the user.

Example:

```
Ali Ahmed
```

Place the account inside:

```
SOC OU
```

Add the user to:

```
GG-SOC-Analysts
```

Now the user automatically receives the same permissions as every other SOC analyst.

No additional permission configuration is required.

---

# 8. Why is Active Directory targeted by attackers?

### Expected Answer

Because Active Directory controls the entire organization's authentication and authorization.

If an attacker compromises Active Directory, they may gain control over:

- User accounts
    
- Computers
    
- Passwords
    
- File servers
    
- Group Policies
    
- Domain Controllers
    

Common attacks include:

- Password Spraying
    
- Kerberoasting
    
- Pass-the-Hash
    
- BloodHound Enumeration
    
- AS-REP Roasting
    
- DCSync
    

The Domain Controller is targeted because it stores Active Directory data and authenticates every domain user.

---

# Bonus Question

Suppose NCAI grows from 20 employees to 2,000 employees with offices in Lahore, Islamabad, and Karachi.

### Expected Answer

I would redesign the environment to improve scalability and management.

Possible improvements include:

- Create separate Organizational Units for each office.
    
- Organize users by department within each office.
    
- Deploy additional Domain Controllers in each city for redundancy and faster authentication.
    
- Use Active Directory Sites and Services to manage replication between locations.
    
- Apply Group Policies specific to each department or office.
    
- Delegate administrative control to local IT staff instead of giving everyone Domain Admin privileges.
    
- Maintain consistent naming conventions for users, computers, and groups.
    

Example structure:

```
NCAI.local

├── Lahore
│   ├── SOC
│   ├── HR
│   └── Finance
│
├── Islamabad
│   ├── SOC
│   ├── Red Team
│   └── IT Support
│
└── Karachi
    ├── Blue Team
    ├── Digital Forensics
    └── Threat Intelligence
```

This design keeps the environment organized, improves performance, simplifies administration, and supports future growth.

---


Absolutely. Since this is a cybersecurity course, I would ask a mix of **practical**, **theoretical**, and **conceptual** questions. That way you can tell whether students actually understand Active Directory or simply followed a YouTube video.

Here are 10 excellent conceptual/theoretical questions.

---

## 1. What is the difference between Active Directory and Active Directory Domain Services (AD DS)?

**Expected Answer:**

- Active Directory is Microsoft's directory service for managing users, computers, groups, and other network resources.
    
- AD DS is the server role that provides Active Directory functionality. Without installing AD DS, a Windows Server cannot function as a Domain Controller.
    

---

## 2. What is the difference between a Workgroup and a Domain?

**Expected Answer:**

- A Workgroup is a peer-to-peer network where each computer manages its own users.
    
- A Domain is centrally managed by one or more Domain Controllers.
    
- Users can log into any domain-joined computer using their domain account.
    

---

## 3. Why do organizations use a Domain Controller instead of creating local users on every computer?

**Expected Answer:**  
Because the Domain Controller provides:

- Centralized authentication
    
- Centralized user management
    
- Centralized security policies
    
- Easier administration
    
- Better security
    

---

## 4. Explain the difference between Authentication and Authorization.

**Expected Answer:**

- Authentication verifies who you are (username and password).
    
- Authorization determines what you are allowed to access after you've been authenticated.
    

**Example:**

- Logging into Windows = Authentication
    
- Accessing the CompanyData folder = Authorization
    

---

## 5. What is the difference between a User Account and a Security Group?

**Expected Answer:**

- A User Account represents an individual person.
    
- A Security Group is a collection of users used to simplify permission management.
    

Instead of assigning permissions to 100 users, assign permissions to one group.

---

## 6. Why is Kerberos more secure than NTLM?

**Expected Answer:**  
Kerberos:

- Uses tickets
    
- Doesn't repeatedly send passwords across the network
    
- Supports mutual authentication
    
- Faster and more secure
    

NTLM:

- Older protocol
    
- Less secure
    
- Used mainly for compatibility with legacy systems
    

---

## 7. Why should permissions be assigned to groups instead of individual users?

**Expected Answer:**  
Because it:

- Simplifies management
    
- Reduces mistakes
    
- Makes onboarding/offboarding easier
    
- Follows enterprise best practices
    

---

## 8. What happens when you type your username and password on a domain-joined computer?

**Expected Answer:**

1. User enters credentials.
    
2. Client contacts DNS.
    
3. DNS locates the Domain Controller.
    
4. Domain Controller authenticates the user (typically using Kerberos).
    
5. If successful, the user receives access according to their group memberships.
    

---

## 9. What is the purpose of Group Policy (GPO)?

**Expected Answer:**  
Group Policy allows administrators to centrally configure and enforce settings across users and computers.

Examples:

- Password policies
    
- USB restrictions
    
- Desktop wallpaper
    
- Software installation
    
- Windows Update settings
    

---

## 10. Why is the Principle of Least Privilege important?

**Expected Answer:**  
Users should receive only the permissions they need to perform their jobs.

Benefits:

- Reduces insider threats
    
- Limits damage if an account is compromised
    
- Improves overall security
    
- Helps prevent accidental changes
    

---

# One "thinking" question (my favorite)

> Suppose an attacker compromises a regular employee account in the Finance department. Does that mean they immediately control the entire Active Directory? Why or why not?

**Expected Answer:**  
No.

Compromising a standard user account does not automatically give an attacker control of the domain. The attacker's access is limited to the permissions of that user. To take over the domain, they would typically need to escalate privileges, steal administrator credentials, exploit misconfigurations, or compromise the Domain Controller.

This question is excellent because it distinguishes students who understand Active Directory security concepts from those who only know the setup steps.

### Suggested viva breakdown

- **4 Practical Questions:** Based on the lab they built.
    
- **4 Theoretical Questions:** AD, DNS, Kerberos, GPOs, etc.
    
- **2 Scenario-Based Questions:** "What would happen if...?" or "How would you...?"
    

This combination gives you a well-rounded assessment of both their hands-on skills and conceptual understanding.


1. Explain the architecture of the Active Directory environment you built.
    
2. What is the difference between Active Directory (AD) and Active Directory Domain Services (AD DS)?
    
3. What is the role of a Domain Controller (DC) in an Active Directory environment?
    
4. Why is DNS essential for Active Directory? What would happen if DNS stopped working?
    
5. Explain the difference between a Workgroup and a Domain.
    
6. Why did you create Organizational Units (OUs)? Why not place all users directly under the domain?
    
7. What is the difference between a User Account and a Security Group?
    
8. Why should permissions be assigned to Security Groups instead of individual users?
    
9. Explain the difference between Authentication and Authorization.
    
10. What happens when a user logs into a domain-joined computer?
    
11. Explain how you joined your Windows client to the domain.
    
12. How can you verify that a computer has successfully joined the domain?
    
13. What is the purpose of Group Policy (GPO)?
    
14. What are LDAP, Kerberos, and NTLM, and what role do they play in Active Directory?
    
15. Why is Kerberos considered more secure than NTLM?
    
16. Explain the permissions you configured for the CompanyData shared folder.
    
17. Why was the "Everyone" group removed from the shared folder permissions?
    
18. If a new employee joins the SOC department, what steps would you follow to create and configure their account?
    
19. Why is Active Directory one of the most targeted technologies in cybersecurity?
    
20. Name and briefly explain three attacks that target Active Directory.
    
21. What is the Principle of Least Privilege, and why is it important?
     
22. If a Domain Controller fails, what impact would it have on the organization?
    
23. Why do enterprises use Security Groups, OUs, and Group Policies instead of managing each computer individually?
    
24. Suppose NCAI expands to three offices with 2,000 employees. How would you redesign your Active Directory structure to support the organization's growth?.
    
    
    
    
    Rauf   10/10  presentaiton questions   10/7
Fizzah 10/8   questions 10/7

hassan preseanton 10/7 quesitons 10/9

minahil shezadi  10/9 10/10


Ayyan  10/9  quesitons 10/9


minhail 10/8 quesiton 10/7

ahmad 10/9 quesiton 10/10


rohail tariq presanton 10/9 quesiton 10/7







