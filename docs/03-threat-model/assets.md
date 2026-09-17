# VulnBankLab — Assets

## 1. Purpose

This document identifies the assets that require protection within VulnBankLab.

An asset is considered sensitive when unauthorized access, modification, disclosure or destruction could negatively affect users, the application or the integrity of banking operations.

---

## 2. Asset Inventory

| ID   | Asset                    | Description                                         | Sensitivity |
| ---- | ------------------------ | --------------------------------------------------- | ----------- |
| A-01 | User credentials         | Authentication credentials and password hashes      | Critical    |
| A-02 | Authentication tokens    | Tokens used to maintain authenticated sessions      | Critical    |
| A-03 | Personal information     | Name, email, phone number and profile information   | High        |
| A-04 | Bank accounts            | Account identifiers, account ownership and balances | Critical    |
| A-05 | Transactions             | Financial transaction records                       | Critical    |
| A-06 | Beneficiaries            | Information about transfer recipients               | High        |
| A-07 | Authorization data       | Roles and permissions                               | Critical    |
| A-08 | Administrative functions | Functions available to administrators               | Critical    |
| A-09 | Security logs            | Records of security-relevant events                 | High        |
| A-10 | API configuration        | Backend configuration and security settings         | High        |
| A-11 | Mobile application data  | Data stored or processed by the mobile application  | High        |
| A-12 | Database                 | Persistent application data                         | Critical    |

---

## 3. Critical Assets

The following assets are considered critical:

### User credentials

Compromise could allow unauthorized access to user accounts.

### Authentication tokens

Compromise could allow unauthorized use of an authenticated session.

### Bank accounts

Unauthorized access or modification could expose financial information or affect banking operations.

### Transactions

Transactions represent high-value business operations.

Unauthorized creation, modification or deletion could have significant consequences.

### Authorization data

Roles and permissions determine which functions users can access.

Compromise of authorization information could result in privilege escalation.

### Database

The database contains multiple sensitive application assets and therefore represents a high-value target.

---

## 4. Security Properties

Each asset should be protected according to three fundamental security properties:

### Confidentiality

Sensitive information must only be accessible to authorized users and services.

### Integrity

Sensitive information and transactions must not be modified by unauthorized parties.

### Availability

The application and its critical functions should remain available to legitimate users.

---

## 5. Asset Security Priorities

The initial security priorities are:

1. Protect authentication credentials.
2. Protect authentication tokens.
3. Protect account information.
4. Protect transaction integrity.
5. Enforce authorization.
6. Prevent unauthorized access to personal information.
7. Protect administrative functions.
8. Maintain reliable security logs.
9. Protect the database.
10. Secure mobile application data.

---

## 6. Security Assessment Focus

The following assets will receive particular attention during the security assessment:

* Authentication credentials
* Authentication tokens
* Account information
* Transaction information
* Authorization data
* Administrative functions
* API data
* Mobile application data
