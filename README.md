Note: This is a rough-draft - This document is still a work in progress.
_______________________________
# LDAP: Lightweight Directory Access Protocol

LDAP (Lightweight Directory Access Protocol) is an open, secure, and cross-platform protocol used for connecting with directory services. It works like a phonebook where details can be searched, and data is stored in a hierarchical manner (like a tree structure). LDAP is known for being lightweight, efficient, and fast.

## Key Features of LDAP

- **Lightweight**: Simple, efficient, and fast.
- **Directory**: Organizes data in a tree-like structure, similar to a file directory or phone directory.
- **Access**: Provides methods to securely access, search, and modify directory data, allowing only authorized users.
- **Protocol**: Defines a set of rules for interacting with the directory and communicating data between clients and the directory server.

## Why Use LDAP?

### General Examples

#### CASE 1: LIBRARY
- Hard to search for books from a large collection.
- LDAP can be used to access data from the directory service based on criteria like genre.

#### CASE 2: PHONEBOOK
- LDAP acts like a giant phonebook providing information to anyone linked to use it.
- Computers can use LDAP to look up details about users.

## Practical Examples

### CASE 1: Centralized Authentication
- Manages user credentials (like usernames and passwords) centrally, allowing users to use the same login information across multiple services (email, computers, applications).

### CASE 2: Organizational Structure
- Stores information about users, groups, devices, and other resources, making it easier to manage large amounts of data.

### CASE 3: Standardization
- Provides a standard way for applications to interact with the directory service, ensuring compatibility and interoperability between different systems and applications.

## LDAP vs Active Directory

- **LDAP**: Protocol used to talk to directory services.
- **Active Directory (AD)**: A directory service database that uses LDAP as a protocol.

## How Does LDAP Work?

1. Use an LDAP-ready system (e.g., ApacheDirectoryStudio).
2. Enter user credentials (username/password).
3. LDAP server checks the LDAP database for credentials.
4. LDAP database responds with validation (valid/invalid credentials).

## How Does LDAP Authenticate Between Client & Server?

1. User enters credentials in an application.
2. Application calls internal API/services.
3. Connection is made with LDAP/Active Directory.
4. If credentials are invalid, an error message is sent to the application.
5. If credentials are valid, LDAP access is granted.

## LDAP Structure

LDAP follows a hierarchical tree structure:
- **ROOT**
  - **DOMAIN COMPONENT (DC/TOP COMPONENT)**
    - **ORGANISATION UNIT (OU/Container that holds object info)**
      - **Common name (cn)**

### Example Structure
```
DIT - Directory info tree
|
KNA (o - organisation)
|---> DEVOPS (ou - organisation unit)
| |---> VG (cn - common name)
|---> DEVELOPERS (ou)
| |---> BACKEND (ou)
| | |--> amaresh (cn)
| | | |--> address, phone, mailID (attributes)
| | |--> chandan (cn)
| | | |--> address, phone, mailID (attributes)
| |---> FRONTEND (ou)
| | |--> amaresh (cn)
| | | |--> address, phone, mailID (attributes)
|---> ACCOUNTS (ou)
| ---> Rajeev Sir (cn)
```

## Important Terms (Object Classes)

- **dc**: Domain component
- **o**: Organisation
- **ou**: Organisation unit
- **cn**: Common name
- **sn**: Surname
- **dn**: Distinguished name

### Object Classes

- **User**: inetOrgPerson
- **User**: groupsOfUniqueName

## Resources
- [ELI5 LDAP](https://www.reddit.com/r/explainlikeimfive/comments/jtzft/eli5_ldap/)
- [LDAP Basics](https://www.youtube.com/watch?v=Xp9kLn9vRmw)
- [LDAP Basic](https://www.reddit.com/r/devops/comments/e89spr/comment/fabjom2/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
