# VulnBankLab — Threat Model

## 1. Methodology

The VulnBankLab threat model uses the STRIDE methodology to identify security threats affecting the application's architecture.

The analysis focuses on:

* Web application
* Mobile application
* REST API
* Database
* Authentication
* Authorization
* Banking transactions
* Administrative functionality

The identified threats will later be converted into security requirements and security tests.

---

# 2. Data Flow

The primary data flow is:

```text
Web Client ────────┐
                   │
                   ▼
                REST API
                   │
Mobile Client ─────┘
                   │
                   ▼
               PostgreSQL
```

The API represents the main trust boundary between client-controlled input and backend resources.

---

# 3. Trust Boundaries

## TB-01 — Client / API

Data received from the web or mobile client must be considered untrusted.

Security controls must therefore be enforced server-side.

## TB-02 — API / Database

The API is responsible for controlling access to database resources.

The client must never have direct database access.

## TB-03 — User / Administrator

Administrative functions must be protected by server-side authorization checks.

---

# 4. STRIDE Analysis

## 4.1 Spoofing

### Threat

An attacker may attempt to impersonate a legitimate user.

### Potential targets

* Login
* Authentication tokens
* Session management
* Password reset
* Mobile authentication

### Security requirements

* Secure authentication
* Strong password storage
* Secure session/token handling
* Authentication failure controls
* Secure password reset mechanisms

### Future tests

* Authentication testing
* Session testing
* Token validation
* Password reset testing

---

## 4.2 Tampering

### Threat

An attacker may attempt to modify application data or business operations.

### Potential targets

* Transaction amount
* Sender account
* Receiver account
* User role
* Beneficiary information
* Account information

### Security requirements

* Server-side validation
* Authorization checks
* Business-rule validation
* Integrity controls
* Database constraints

### Future tests

* Parameter manipulation
* Request modification
* Business logic testing
* Authorization testing

---

## 4.3 Repudiation

### Threat

A user may deny having performed a security-sensitive action.

### Potential targets

* Transfers
* Account modifications
* Beneficiary creation
* Administrative operations

### Security requirements

* Security logging
* Transaction identifiers
* Timestamps
* User identification
* Administrative audit trails

### Future tests

* Log generation verification
* Log integrity verification
* Security event coverage

---

## 4.4 Information Disclosure

### Threat

An unauthorized user may access sensitive information.

### Potential targets

* User profiles
* Account balances
* Account numbers
* Transactions
* Beneficiaries
* API responses
* Mobile local storage

### Security requirements

* Object-level authorization
* Data minimization
* Secure API responses
* Secure storage
* Access control

### Future tests

* BOLA/IDOR testing
* API response analysis
* Authorization testing
* Mobile storage analysis

---

## 4.5 Denial of Service

### Threat

An attacker may consume excessive application resources.

### Potential targets

* Authentication endpoints
* Search endpoints
* Transaction endpoints
* File upload functionality
* API resources

### Security requirements

* Rate limiting
* Request size limits
* Input validation
* Resource controls
* Appropriate timeouts

### Future tests

Testing will be performed only in the controlled local laboratory environment.

---

## 4.6 Elevation of Privilege

### Threat

A normal user may attempt to obtain privileges reserved for administrators.

### Potential targets

* Administrative API endpoints
* User role
* Administrative dashboard
* User management
* Transaction management

### Security requirements

* Server-side role validation
* Function-level authorization
* Object-level authorization
* Least privilege

### Future tests

* Horizontal privilege testing
* Vertical privilege testing
* Administrative endpoint authorization testing

---

# 5. High-Priority Threat Scenarios

The following scenarios are considered high priority for the project.

## TH-01 — Unauthorized Account Access

An authenticated user attempts to access another user's account.

Potential security category:

* BOLA
* Broken Access Control

---

## TH-02 — Unauthorized Transaction Access

A user attempts to access transaction records belonging to another user.

Potential security category:

* BOLA
* Broken Access Control

---

## TH-03 — Unauthorized Transfer

A user attempts to initiate a transfer using an account that does not belong to them.

Potential security category:

* Broken Access Control
* Business Logic vulnerability

---

## TH-04 — Privilege Escalation

A standard user attempts to access administrative functionality.

Potential security category:

* Broken Function Level Authorization
* Broken Access Control

---

## TH-05 — Sensitive Data Exposure

An API endpoint returns more information than the client requires.

Potential security category:

* Broken Object Property Level Authorization
* Sensitive data exposure

---

## TH-06 — Authentication Compromise

An attacker attempts to bypass or abuse authentication mechanisms.

Potential security category:

* Authentication failures
* Broken Authentication

---

## TH-07 — Mobile Data Exposure

Sensitive information is improperly stored or exposed on the mobile device.

Potential security category:

* Insecure Data Storage
* Inadequate Privacy Controls

---

# 6. Security Requirements

The following security requirements are derived from the threat model.

| ID    | Requirement                                                           |
| ----- | --------------------------------------------------------------------- |
| SR-01 | All protected API endpoints require authentication.                   |
| SR-02 | Authorization must be enforced server-side.                           |
| SR-03 | Users may only access resources they are authorized to access.        |
| SR-04 | Administrative functions require appropriate privileges.              |
| SR-05 | Sensitive data must not be unnecessarily returned by APIs.            |
| SR-06 | Financial operations must enforce server-side business rules.         |
| SR-07 | Authentication tokens must be securely handled.                       |
| SR-08 | Sensitive mobile data must be securely stored.                        |
| SR-09 | Security-sensitive operations must generate appropriate logs.         |
| SR-10 | API resources must have appropriate rate and resource controls.       |
| SR-11 | Client-provided input must be validated server-side.                  |
| SR-12 | Database access must remain restricted to trusted backend components. |

---

# 7. Security Framework Mapping

VulnBankLab will use multiple OWASP references because the project contains web, mobile and API components.

### Web

OWASP Top 10:2025.

### API

OWASP API Security Top 10:2023.

### Mobile

OWASP Mobile Top 10:2024.

These frameworks will be used as references during security testing and reporting.

---

# 8. Threat Model Status

**Status:** Initial threat model

**Completed:**

* Assets identified
* Trust boundaries identified
* STRIDE analysis performed
* High-priority threats identified
* Security requirements defined
* OWASP mappings established

**Next phase:**

Security requirements and application design.
