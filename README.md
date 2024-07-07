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

__________

02 July 2024
============

# Resources
- [ELI5 LDAP](https://www.reddit.com/r/explainlikeimfive/comments/jtzft/eli5_ldap/)
- [LDAP Basics](https://www.youtube.com/watch?v=Xp9kLn9vRmw)
- [LDAP Basic](https://www.reddit.com/r/devops/comments/e89spr/comment/fabjom2/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

-------------------------------------
LDAP: Lightweight Directory Access Protocol
- Open, secure & cross-platform
- Provides access for connecting w/ directory services
- Like a phonebook where details can be searched
- DATA STRUCTURE: Data stored in a hierarchical manner (like a tree structure)
- LIGHTWEIGHT: Simple, efficient and fast
- DIRECTORY: LDAP organises data in a tree-like structure, similar to file directory or phone directory
- ACCESS: Provides methods to access, search and modify directory's data, SECURELY only allows authorised users to access or modify
- PROTOCOL: Defines set of rules or how to interact with directory and how data will be communicated between clients and directory server (glorified db)

# Why LDAP?
## General Examples
- CASE 1: LIBRARY
	- Hard to search books from a large collection
	- What if searching is to be done based on certain criteria like genre? LDAP can be used to access this data from the directory service
	
- CASE 2: PHONEBOOK
	- LDAP is a giant phonebook that provides info about to anyone linked to use that phonebook
	- Computers can be linked to use that phonebook to look up details about you or someone else 
-----------------------------------------

## Practical Examples
- LDAP is a way to tell many computers about a set of tings at once
- Any changes made in LDAP will be shared with all computers when they ask about info

- CASE 1: Centralized Authentication: It allows organizations to have a central place to manage user credentials (like usernames and passwords). This way, users can use the same login information to access multiple services (email, computers, applications).

- CASE 2: Organizational Structure: It can store information about users, groups, devices, and other resources, making it easier to manage large amounts of data.

- CASE 3: Standardization: It provides a standard way for applications to interact with the directory service, ensuring compatibility and interoperability between different systems and applications.

----------------------------------
LDAP vs Active Directory
- LDAP is a way of talking to Active Directory
- AD = Directory service DB
- LDAP = Protocol used to talk to AD

--------------------------------------
How does LDAP work?
- We use an application or LDAP ready system (ApacheDirectoryStudio)
- Enter user/pass (or something else)
- LDAP calls LDAP server where internally LDAP database is also linked  
- LDAP DB sends response back to server whether your user/pass is invalid/valid

-----------------------------------------
How does LDAP Authenticate b/w Client & Server
- In an app, user will enter user/pass
- Internaly API/Services to be called 
- Connection made with LDAP/Active directory
- If invalid credentials entered/not found in LDAP, error message to be sent to application
- If valid credfentials entered, LDAP access will be granted

----------------------------------------------

# LDAP Structure
- LDAP follows a tree (root) structure
- ROOT --> DOMAIN COMPONENT (DC/TOP COMPONENT) --> ORGANISATION UNIT (OU/Container that holds object info) --> Common name  
- Example:
```
DIT - Directory info tree
|
KNA (o - organisation)
|---> DEVOPS (ou - organisation unit)
|	|---> VG (cn - common name)
|---> DEVELOPERS (ou)
|	|---> BACKEND (ou)
|	|	|--> amaresh (cn)
|	|		|--> address, phone, mailID (attributes)
|	|	|--> chandan (cn)
|	|		|--> address, phone, mailID (attributes)
|	|---> FRONTEND (ou)
|	|	|--> amaresh (cn)
|	|		|--> address, phone, mailID (attributes)
|---> ACCOUNTS (ou)
	| ---> Rajeev Sir (cn)

```
---------------------------------------------------

Important terms (object)
- dc: domain componentv vvvvvvvvvvvvvvvvvv
- o: organisation
- ou: organisation unit
- cn: common name
- sn: surname
- dn: distinguish name
- Object (when combined)
	- User: inetOrgPerson
	- User: groupsOfUniqueName
-------------------------
w----------------------------


========================================
[CN vs DN](https://www.reddit.com/r/explainlikeimfive/comments/jtzft/comment/c2f46v8/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

>Now, about the strange "cn this" and DN" that: I'm sure you've seen a phonebook. When you want to look for someone's number, you can only look them up if you know their last name. That works if you know their last name, but lets say you want to look up only girls in the phonebook?

You can ask ldap about anyone in the list based on certain criteria. those labels, like CN and DN are certain things you can ask ldap about.

CN stands for common name, and means what you'd expect; its' a common name, like Sally Harrison.

DN means distinguished name, and it's a more complicated name, and i'll get to that in a minute.

Remember above how I mentioned in the phonebook, you can only look up people by their name? What you can do in ldap is make containers to put people in. Let's say you have two containers, "Boys" and "girls"

You can ask ldap about only boys or girls if you want.

DN gives you information about which container the person is in, so CN=Sally Harrison might look like: DN: CN=George Harrison, DC=GIRLS

This way, you can ask ldap, "hey, I want all the girls' phone numbers!" so you can ask ldap to give you everyone that's DC=GIRLS.

===============================
===============================
===============================

# Using Apache DirectoryStudio
1. To use the Apache Directory Studio Browser plug-in open the LDAP perspective. Therefore go to Window → Open Perspective → Other... and select the LDAP perspective.

2. To create a new connection click the   New Connection button.

3.

## Structure I want to replicate
DIT - Directory info tree
|
movieListSite (o - organisation)
|---> comedy (ou - organisation unit)
|	|---> movie name (cn - common name)
|---> action (ou)
|	|---> gore (ou)
|	|	|--> movie name (cn)
|	|		|--> actorName, releaseDate, score (attributes)
|	|	|--> movie name (cn)
|	|		|--> actorName, releaseDate, score (attributes)=
|	|---> non gore (ou)
|	|	|--> movie name (cn)
|	|		|--> actorName, releaseDate, score (attributes)
|---> drama (ou)
	| ---> movie name (cn)

----------------------

touch finoptaplus.ldif
```
dn: dc=FinoPtaPlus,dc=com
objectClass: top
objectClass: domain
dc: FinoPtaPlus
description: FinoPtaPlus database
```
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
NOT ldapmodify -a -c -h localhost -p 3389 -D "cn=Directory Manager" -w redhat@123  -f <fileName.ldif>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

ldapmodify -a -c -H ldap://localhost:3389 -D "cn=Directory Manager" -w qwerty123 -f finoptaplus.ldif 

-a: to add
-c: to continue processing the ldif file even if faced with error
-H: specifying the LDAP URL to connect to
-D: defining the distinguished name
-w: for defining the password for the user
-f: filename of the LDIF file

To: create Object classes & attributes using the LDIF files

##################################################
--------------------------------------------------
##################################################

=========================================
July 03

## Recreating ApacheDS Connection
- Clicked 'Window -> Open Perspective -> Other -> LDAP (Default)'.
- Created a connection in the LDAP Browser using:
	- Name: originalConnection
	- Host: localhost
	- Port: 3389
	- bindDn: cn=Directory Manager

## Creating Suffix/Database
I first deleted the existing suffix while referring to this [document](https://docs.redhat.com/pt/documentation/red_hat_directory_server/12/html/configuring_directory_databases/assembly_deleting-a-database-of-a-suffix-that-is-no-longer-needed_configuring-directory-databases#proc_deleting-a-database-using-the-command-line_assembly_deleting-a-database-of-a-suffix-that-is-no-longer-needed):

1. Listing the existing databases:
```
32a3975e254a:/ # dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend suffix list

Enter password for cn=Directory Manager on ldap://localhost:3389: 
dc=finoptaplus,dc=com (finoptaplus)
dc=finoptaplus2,dc=com (finoptaplus2)
```

2. Deleting the databases:
```
32a3975e254a:/ # dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend delete "finoptaplus2" --do-it

Enter password for cn=Directory Manager on ldap://localhost:3389: 
Deleting Backend cn=finoptaplus2,cn=ldbm database,cn=plugins,cn=config :
Type 'Yes I am sure' to continue: Yes I am sure
The database, and any sub-suffixes, were successfully deleted

32a3975e254a:/ # dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend delete "finoptaplus" --do-it

Enter password for cn=Directory Manager on ldap://localhost:3389: 
Deleting Backend cn=finoptaplus,cn=ldbm database,cn=plugins,cn=config :
Type 'Yes I am sure' to continue: Yes I am sure
The database, and any sub-suffixes, were successfully deleted
```

3. Adding new database
```
# Creating the DB
32a3975e254a:/ # dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend create --suffix="dc=keenable,dc=com" --be-name="keenable-suffix01" --create-entries --create-suffix

Enter password for cn=Directory Manager on ldap://localhost:3389: 
The database was sucessfully created

# Verifying its creation
32a3975e254a:/ # dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend suffix list
Enter password for cn=Directory Manager on ldap://localhost:3389: 
dc=keenable,dc=com (keenable-suffix01)
```

## Modifying Database & Creating LDIF files
To push data to the DB, write an LDIF file:
```
dn: dc=keenable,dc=com
objectClass: top
objectClass: domain
dc: keenable
description: keenable database has been initialised with this 
```

To make the entry, run the following command:
```
ldapmodify -a -c -H ldap://localhost:3389 -D "cn=Directory Manager" -w qwerty123 -f keenableDB.ldif 

# -a: to add
# -c: to continue processing the ldif file even if faced with error
# -H: specifying the LDAP URL to connect to
# -D: defining the distinguished name
# -w: for defining the password for the user
# -f: filename of the LDIF file
```

### Adding organisationalUnits
In order to add the organisationalUnits, the following LDIF file was created within the context of our company for creating a directory of employees:
```
# An excerpt from newOrganisationalUnit.ldif
dn: ou=accounts,dc=keenable,dc=com
objectClass: organizationalClass
objectClass: top
description: For holding accountants
```

This ldif file was modified by running the following commands:
```
`ldapmodify -a -c -H ldap://localhost:3389 -D "cn=Directory Manager" -w "pass" -f newOrganisationalUnit.ldif`
```

### Adding commonNames
The ldif given below was modified by running:
`ldapmodify -a -c -H ldap://localhost:3389 -D "cn=Directory Manager" -w "pass" -f newCommonNames.ldif`
```
# Excerpts from newCommonNames.ldif
# dn: cn=Name,ou=backend,ou=dev,dc=keenable,dc=com
# objectClass: inetOrgPerson
# cn: Name
# sn: Surname
# l: Noida

dn: cn=Krish Kumar,ou=backend,ou=dev,dc=keenable,dc=com
objectClass: inetOrgPerson
cn: Krish Kumar
sn: Kumar
l: Kolkata
```

Similarly, the `ou` for devops and developers was created along with various sub-organizationalUnits & common-names within them to cater to the following tree-structure:
```
keenable
|
|-------> accounts
|		|-------> FinancialAccounting
|		|		|-------> Emp1 
|		|-------> TaxAccounting
|				|-------> Emp2
|-------> development
|		|-------> backend
|		|		|-------> Emp3 
|		|-------> frontend
|				|-------> Emp4
|-------> devops
		|-------> automation
		|		|-------> Emp5 
		|-------> security
				|-------> Emp6
```
### Adding Attributes for ObjectClasses
- 

### Understanding the terminologies

1. Directory Services
- Used to organise, store & present data in a key-value format
- Directories are optimised for lookups,searches, etc AKA data that is mostly read but not written often
- In a phonebook, info on each person is listed briefly like these directories

2. LDAP 
- Explains the rules based on which communication can be held with directory service and user/application

3. Attributes
- Key-Value pairs held within an ObjectClass
- Ex: mail:yash@fl.com but mail=yash@fl.com when refferencing in dn

4. Entries
- The statement blocks within an LDIF file
- Needed to associate the created attributes with something
- We can create an attribute "age=29" but can't tell whose age it is if this attribute is not associated with an entry
- Entries added using


=============================

Jul 04 

# Creating A New DB

## Setting up SUFFIX
### Creating suffix:
dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend create --suffix="dc=tablechair,dc=com" --be-name="tablechair":
```
Enter password for cn=Directory Manager on ldap://localhost:3389: 
The database was sucessfully created
```

- Verifying the creation: dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend suffix list:
```
Enter password for cn=Directory Manager on ldap://localhost:3389: 
dc=chairtable,o=keenable (tablechair)
dc=keenable,dc=com (keenable-suffix01)
```

What is directory?
Simply put, a directory is a repository of data, much like a database (but with significant differences) that is used to store huge amounts of data. Directories are optimised for fast search and retrieval. Directories are also fairly static — in the sense that the data in a directory is not updated very frequently.

======================================================

July 05

## CRUD Operations

### CREATE ENTRY
- We create LDIF files with the following format/rules:
```
# From the google document
First line of an entry is the dn  dn should be unique, consist the baseDn
Next few lines define objectClasses.
Next lines defines attributes values
All must attributes should be passed
There should not be any extra spaces in ldif file
```
- A sample LDIF file that I have created is as follows:
```
dn: cn=Rahul Shankar,ou=financialAccounting,ou=accounts,dc=keenable,dc=com
objectClass: inetOrgPerson
cn: Rahul Shankar
sn: Shankar
l: Noida
```

### MODIFY ENTRIES / ADD, DELETE OR REPLACE
- The rules for modifying an entry are:
```
First line is the dn of entity
Second line defines changetype modify
Changetype can be add / replace /  delete
For Replace change it is not necessary to attribute exist it will replace null.
```
- A sample Modify operation LDIF that I have made is as follows:
```
# To replace
DN: cn=Indigo,ou=employees,dc=company,dc=com
changetype: modify
replace: tableno
tableno: 20

# To delete a value
DN: cn=Indigo,ou=employees,dc=company,dc=com
changetype: modify
delete: wheellessChairCol
wheellessChairCol: blue

# TO add value to an existing attribtue within the objectClass
DN: cn=Indigo,ou=employees,dc=company,dc=com
changetype: modify
add: wheellessChairCol
wheellessChairCol: Red
```
- MAKE SURE that the attribute to which value is being added to already exists within the objectClass of the object 

### LDAP CRUD Commands

#### Changing Passwords
Changing own password can be done using:
```
ldappasswd -H ldap://localhost:3389 -x -D "cn=Directory Manager" -w qwerty123 -a qwerty123 -S

New password: 
Re-enter new password: 
Result: Confidentiality required (13)
Additional info: Operation requires a secure connection.
```

Changing other users' passwords can be done using ldapmodify:
```
# file.ldif
# userPassword is stored within the person objectClass
dn: uid=bjensen,ou=People,dc=example,dc=com
changetype: modify
replace: userPassword
userPassword: ChAnGeMe

ldapmodify -a -c -H ldap://localhost:3389 -D "cn=Directory Manager" -w qwerty123 -f file.ldif
```
