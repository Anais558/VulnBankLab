# VulnBankLab — Application Architecture

## 1. Overview

VulnBankLab consists of three primary application components:

* Web application
* Mobile application
* REST API

Both the web and mobile applications communicate with the backend through the REST API.

The backend communicates with a PostgreSQL database.

```text
Web Application ──────┐
                      │
                      ▼
                  REST API
                      │
Mobile Application ───┘
                      │
                      ▼
                  PostgreSQL
```

---

## 2. Application Components

### 2.1 Web Application

Technology:

* React
* TypeScript
* Tailwind CSS

The web application provides the customer and administrator interfaces.

Main functionalities:

* Registration
* Authentication
* Profile management
* Account consultation
* Balance consultation
* Transaction history
* Beneficiary management
* Transfers
* Administration

---

### 2.2 Mobile Application

Technology:

* Flutter

The mobile application provides banking functionality through a mobile interface.

Main functionalities:

* Authentication
* Account consultation
* Balance consultation
* Transaction history
* Beneficiary management
* Transfers
* Profile management

---

### 2.3 REST API

Technology:

* Node.js
* Express.js
* TypeScript

The API is responsible for:

* Authentication
* Authorization
* User management
* Account management
* Transaction processing
* Beneficiary management
* Administrative operations
* Business logic

The API represents the primary trust boundary between the client applications and backend resources.

---

### 2.4 Database

Technology:

* PostgreSQL

Main entities:

```text
Users
Accounts
Transactions
Beneficiaries
```

---

## 3. User Roles

VulnBankLab defines two application roles:

### USER

Standard banking customer.

Permissions include:

* Access own profile
* Access own accounts
* View own transactions
* Manage own beneficiaries
* Initiate authorized transfers

### ADMIN

Administrative user.

Permissions include:

* User management
* Account management
* Transaction monitoring
* Security log access
* Administrative operations

Authorization must be enforced server-side.

---

## 4. Main Data Entities

### Users

```text
id
email
password_hash
first_name
last_name
phone
role
created_at
```

### Accounts

```text
id
user_id
account_number
account_type
balance
currency
created_at
```

### Transactions

```text
id
sender_account_id
receiver_account_id
amount
currency
type
status
created_at
```

### Beneficiaries

```text
id
user_id
name
account_number
bank_name
created_at
```

---

## 5. Sensitive Data

The following information is considered sensitive:

* Password hashes
* Authentication tokens
* Personal information
* Phone numbers
* Account numbers
* Account balances
* Transaction history
* Beneficiary information

The application must prevent unauthorized disclosure or modification of this information.

---

## 6. Authentication Flow

```text
Client
  |
  | POST /api/auth/login
  |
  v
API
  |
  | Authentication
  |
  v
Database
  |
  | Authentication result
  |
  v
API
  |
  | Authentication token/session
  |
  v
Client
```

---

## 7. Account Access Flow

```text
Client
  |
  | GET /api/accounts/:id
  v
API
  |
  | Authentication
  | Authorization
  v
Database
  |
  v
API
  |
  v
Client
```

The API must verify that the authenticated user is authorized to access the requested account.

This control will be tested during the security assessment for potential Broken Object Level Authorization (BOLA/IDOR).

---

## 8. Transfer Flow

```text
Client
  |
  | POST /api/transfers
  v
API
  |
  ├── Authentication
  ├── Authorization
  ├── Input validation
  ├── Business rules
  └── Transaction processing
  |
  v
Database
  |
  ├── Debit sender
  ├── Credit receiver
  └── Create transaction record
```

The transfer functionality represents a high-value security area because it can affect financial data and account balances.

---

## 9. Trust Boundaries

The architecture contains several trust boundaries.

```text
User Device
    |
    | Untrusted input
    v
REST API
    |
    | Trusted backend communication
    v
Database
```

All data received from clients must be treated as untrusted.

Security controls such as authentication, authorization, input validation and business-rule validation must be enforced on the server side.

---

## 10. Attack Surface

The main attack surfaces identified during the initial architecture review are:

### Web

* Authentication
* Authorization
* Session management
* Input handling
* XSS
* CSRF
* File uploads
* Business logic

### Mobile

* Local storage
* Authentication
* Tokens
* Network communication
* Application configuration
* API communication

### API

* Authentication
* Authorization
* Object-level access control
* Function-level access control
* Input validation
* Data exposure
* Business logic
* Rate limiting
* CORS
* Token handling

---

## 11. Security Assessment Focus

The security assessment will focus on the interaction between:

```text
Web
 ↓
API
 ↓
Database

Mobile
 ↓
API
 ↓
Database
```

The assessment will evaluate both technical vulnerabilities and business-logic weaknesses.

---

## 12. Current Status

**Phase:** Architecture definition

**Completed:**

* Application components identified
* User roles defined
* Main data entities defined
* Authentication flow defined
* Transfer flow defined
* Trust boundaries identified
* Initial attack surface identified

**Next phase:**

Threat modeling and security requirements.
