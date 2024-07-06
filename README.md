<div align=center>
Note: This is a rough draft - This document is still a work in progress.
</div>

_______________________________
# LDAP: Lightweight Directory Access Protocol

LDAP (Lightweight Directory Access Protocol) is an open, secure, and cross-platform protocol used for connecting with directory services. It works like a phonebook where details can be searched, and data is stored in a hierarchical manner (like a tree structure). LDAP is known for being lightweight, efficient, and fast.

## Key Features of LDAP

- **Lightweight**: Simple, efficient, and fast.
- **Directory**: Organises data in a tree-like structure, similar to a file directory or phone directory.
- **Access**: Provides methods to securely access, search, and modify directory data, allowing only authorised users.
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

### CASE 1: Centralised Authentication
- Manages user credentials (like usernames and passwords) centrally, allowing users to use the same login information across multiple services (email, computers, applications).

### CASE 2: Organisational Structure
- Stores information about users, groups, devices, and other resources, making it easier to manage large amounts of data.

### CASE 3: Standardisation
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

# Verifying The Basics

## Table of Content

## Resources
- [Hierarchical VS Flat Directories](https://stackoverflow.com/questions/40558806/best-directory-structure-for-static-files-hierarchical-vs-flat)
	- Good for understanding through computer related examples
- [Hierarchical vs. Flat Organisational Structure](https://pingboard.com/blog/hierarchical-vs-flat-organizational-structure-and-benefits-of-each/) 
	- Extremely great for general understanding with real life examples

## Understanding LDAP And Its Components
LDAP (Lightweight Directory Access Protocol) is a **protocol** or a way of talking to and possibly modifying **directories**.  

An analogical explanation of the same is as follows:
> It works like a phonebook where details can be searched and data is stored in a hierarchical manner / like a tree structure.

### Protocol

The word protocol is equated with guidelines or rules that govern actions or behaviours. For example, "Do not break the army protocol" can be equated with "Follow the established rules within the army", essentially saying that the army personnels should follow orders. Very similarly in networking, a protocol is a set of instructions/rules that computers or the personnel within a network or army, follow to talk to eachother. 

Within the context of LDAP, some of the established protocol or rule or guideline that is expected to be followed for accessing directories is as follows. One such rule defines how the Client-Server interaction will handle authentication and authorisation and how client will talk to directory server. It should be noted that interaction can also be held anonymously without authentication, if allowed by server admins. 

Simply speaking, this Protocol or rule explains how communication will be held for accessing the data or content belonging within the LDAP directory. 

### Directory

Generally speaking, a directory is a structured way of organising information for easy access like a catalogue, employee directory, phone book, library card, emergency contact list, traditional mobile phonebook/contact list, etc.

LDAP's directory is similar to the traditional 'ContactList' from cellphones contains contacts with their phone-numbers and additional information in the form of directory. However, it should be noted that [LDAP's directory is Hierarchical and not Flat type](https://stackoverflow.com/questions/40558806/best-directory-structure-for-static-files-hierarchical-vs-flat), like the 'ContactList'. In this application, there would be no groupings or categories and all entries of contacts will independent of eachother but still on the same level. There would also be some disadvantages of this flat format:
- If contact list becomes too long, navigating would be difficult
- There will be no organisation for saving contacts 

LDAP's directory uses hierarchical  
Real life examples of a hierarchical directory can be table of content, the output of the 'tree' command, a detailed-plan for a pyramid scheme, etc.

Within the context of LDAP, a directory is a database whose speciality is fast filtered searching from a huge hierarchical data. LDAP's directory is designed to store information like user authentication, authorisation and other information:
- **Authentication**: Verifying the identity of a user or system - Is the User/Pass correct?
- **Authorisation**: Defines what a user is allowed and not allowed to do - Example: Role Based Access Control, users not allowed to open admin-marked files.
- **Other Information**: Can contain any piece of information as attribute-values in the form of key-value pairs

### Topics Related To Directory 
#### Directory Information Tree (DIT)
In applications like Apache Directory Studio, DIT is used to structure and access directory entries based on their hierarchical relationships. 

As explained before, LDAP connects to hierarchical directories which have tree-like structures. The suffix and other objects with **Distinguished Names (DNs)** belong within this very tree.

#### Suffix & Distinguished Name (DN)
This is the starting point of the directory, its very base or foundation upon which data will be added. If a comparison was to be made between the such Directories and the filesystem, the "/" or the root will be the suffix, under which further files/folders can be added. 

Distinguished Names on the other hand, are a unique name to specify the pin-pointed location of an entry within the directory. If this is not unique, then querying specific attributes within a directory would be difficult. This is similar to how files with same name cannot be added within the same folder. 

## Resources
- [ELI5 LDAP](https://www.reddit.com/r/explainlikeimfive/comments/jtzft/eli5_ldap/)
- [LDAP Basics](https://www.youtube.com/watch?v=Xp9kLn9vRmw)
- [LDAP Basic](https://www.reddit.com/r/devops/comments/e89spr/comment/fabjom2/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
