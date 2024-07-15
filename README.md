<div align=center>

![img](https://i.imgur.com/lkhw80m.png)
# Understanding LDAP: An Introduction
</div>

## Table of Contents
- [Understanding LDAP And Its Components](#understanding-ldap-and-its-components)
  - [Protocol](#protocol)
  - [Directory](#directory)
- [Topics Related To Directory](#topics-related-to-directory)
  - [Directory Information Tree (DIT)](#directory-information-tree-dit)
  - [Suffix & Distinguished Name (dn)](#suffix--distinguished-name-dn)
- [Working With Directories](#working-with-directories)
  - [Creating A Directory](#creating-a-directory)
  - [Modifying A Directory](#modifying-a-directory)
- [Searching Using LDAPSearch](#searching-using-ldapsearch)
- [LDAP Installation](#ldap-installation)
- [Resources](#resources)

## Understanding LDAP And Its Components
LDAP (Lightweight Directory Access Protocol) is a **protocol** or a way of talking to and possibly modifying **directories**.  

An analogical explanation of the same is as follows:
> It works like a phonebook where details can be searched and data is stored in a hierarchical manner / like a tree structure.

Provided below is a slightly more detailed explanation of LDAP - which consists of LDAP Client for Users & LDAP Server for data storage.
#### Protocol

The word protocol is equated with guidelines or rules that govern actions or behaviours. Similarly in networking, a protocol is a set of instructions or rules that computers within a network follow to talk to eachother. 

Within the context of LDAP, one such rule from the established rules that are expected to be followed, defines how the Client-Server interaction will handle authentication and authorisation and how client will talk to directory server. It should be noted that interaction can also be held anonymously without authentication, if allowed by server admins. 

Simply speaking, this Protocol or rule explains how communication will be held for accessing the data from the Directory Server or content belonging within the LDAP directory. 

#### Directory

A directory is a structured way of organising information for easy access like a [catalogue](https://www.visme.co/templates/catalogs/), employee directory, phone book, library card, emergency contact list, etc.

LDAP's directory is similar to the **traditional** 'ContactList' from cellphones that contain contacts with their phone-numbers and additional attributes in the form of a directory. However, it should be noted that [LDAP's directory is Hierarchical and not Flat type](https://stackoverflow.com/questions/40558806/best-directory-structure-for-static-files-hierarchical-vs-flat), like the 'ContactList', in which, there would be no groupings or categories and all entries of contacts will be independent of eachother but still be on the same level. There would also be some disadvantages of this flat format:
- If contact list became too long, navigating would be difficult
- There will be no clear organisation for saving contacts and forming groups

These disadvantages are solved by Hierarchical directories - Some of the real life examples of a hierarchical directory that I have come up with are:
- The [output](https://unix.stackexchange.com/questions/127063/tree-command-output-with-pure-7-bit-ascii-output) of the 'tree' command
- A [detailed-plan for a pyramid scheme](https://cpb.iphy.ac.cn/article/2019/1992/cpb_28_7_078901/cpb_28_7_078901_f1.jpg)
- Table of content
  
Within the context of LDAP, a directory is a database whose speciality is fast filtered searching from a huge hierarchical data. Accessing LDAP's directory is secure as it provides User:
- **Authentication**: Verifying the identity of a user or system - Is the User/Pass correct?
- **Authorisation**: Defines what a user is allowed and not allowed to do - Example: Role Based Access Control, users not allowed to open admin-marked files.

### Topics Related To Directory 
#### Directory Information Tree (DIT)
In LDAP, DIT is used to structure and access directory entries based on their hierarchical relationships. 

As explained before, LDAP connects to hierarchical directories which have tree-like structures. The suffix and other objects with **Distinguished Names (DNs)** belong within this very tree.

#### Suffix & Distinguished Name (dn)
This is the starting point of the directory, its the very foundation within which data will be added. For simplicity, the name of the site like "wikipedia.com/" is the suffix and the pages created further within it are like entries/objects. As an example, "wiki/" & "wiki/someArticle" in "wikipedia.org/wiki/someArticle" will represent how entries (pages) are organised under the suffix (wikipedia.org). Similarly in filesystem, "/" will be the suffix and the files stored under it will be the entries.

Distinguished Names (dn) on the other hand, are a unique name to specify the pin-pointed location of an entry within the directory. If this is not unique, then querying specific attributes within a directory would be difficult. This is similar to how files with same name cannot be added within the same folder. If the previous example was to be represented hierarchically in LDAP, its `dn` could be `cn=someArticle, ou=wiki, dc=wikipedia, dc=org`.

## Working With Directories

### Creating A Directory
The actions in this section were performed after going through this document [this DigitalOcean Guide](https://www.digitalocean.com/community/tutorials/understanding-the-ldap-protocol-data-hierarchy-and-entry-components#defining-ldap-data-components). The sample database that I created for my own understanding followed the scenario of storing information related to the Table-Chairs within a company's rooms that will be divided into different groups. The following structure was formed before getting started:
```
Company
|
|----> Common Rooms
|       |-------> Kitchen
|                   |-------> Table-Chair details (their Number, their Colour, Type of chair, etc.)  
|
|----> Employee Rooms
|       |-------> Indigo
|       |           |-------> Table-Chair details (their Number, their Colour, Type of chair, etc.) 
|       |
|       |-------> Aryabhat
|                   |-------> Table-Chair details (their Number, their Colour, Type of chair, etc.) 
|
|----> Contractor Rooms
|       |-------> Patliputra
|       |           |-------> Table-Chair details (their Number, their Colour, Type of chair, etc.) 
|       |
|       |-------> ShantiNiketan
|                   |-------> Table-Chair details (their Number, their Colour, Type of chair, etc.) 
|
|----> Intern Rooms
        |-------> Nalanda
                    |-------> Table-Chair details (their Number, their Colour, Type of chair, etc.) 
```

Provided below are the steps that I utilised for creating a directory for the above structure within LDAP by strictly writing LDAP Data Interchange Format (LDIF) files:

**1. Creating Suffix**
- Entered the LDAP container using `podman exec -it ldap-v1 bash` where ldap-v1 is my container's name
- Created suffix using `dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend create --suffix="dc=chairtables, dc=com" --be-name="company""`
	- *`dsconf`*: CLI-Tool for managing directories - Have not studied this tool in detail
	- *`-D="cn=Directory Manager"`*: To define the bindDN used while connecting - Directory Manager is Admin
	- *`ldap://localhost:3389`*: To specify the LDAP Host server
	- *`backend create`*: To create a database in backend
	- *`--suffix="dc=company,dc=com"`*: For specifying the Suffix or the Root-Distinguished-Name
	- *`--be-name`*: To specify the name of the suffix
- Ran `dsconf -D "cn=Directory Manager" ldap://localhost:3389 backend suffix list` to verify the creation of the suffix
   
**2. Writing LDIF To creation Entries of Attributes, ObjectClass and Objects**		
I wrote the '[roomInfo.ldif](https://github.com/YashAnand1/UnderstandingLDAP/blob/main/roomInfo.ldif)' LDIF file for creating these entries, with the following sequence:
- Attribute definitions
- ObjectClass definition
- Object creation of the 4 categories as organizationalUnit & various rooms belong within these categories as a commonName

The terminologies being used in the above ldif file are being explained below in a tabular form to explain these 3 entry-blocks. Please have a look at hyperlinked LDIF FIle first and then refer to the following tables for a better understanding:

2.1. Attribute Definitions

<div align=center>
	
| LDIF Term |  Explanation |			
|----|-----------------------------------------------------------------|			
| `attributetypes` | Defining attribute to be added and its features   |			
| `NAME`       | Attribute Names		| 
| `EQUALITY`| For equality matching operations on the attribute values - "Ignore case match entered by user when searching" |			
| `SYNTAX`    | In LDAP SYNTAX = DataType like string, integer, etc. but with a [unique code](https://ldap.com/attribute-syntaxes/) |		
| `SINGLE-VALUE`| Some attributes can only have one value but some may have many |		
</div>

2.2. ObjectClass Definitions

<div align=center>
	
| LDIF Term    | Explanation    |			
|---|--------------------------------------|			
| `objectClasses` | Defines the objectClass to be added in the directory     |		
| `NAME`          | Object class name                                                |			
| `SUP`           | AKA Superclass - "This is a parent class that the objectClass being created is a child of and so inherits its attributes" |		
| `MUST`          | Mandatory attributes - cannot be left empty    |		
| `MAY`           | Optional attributes - can be left empty |		
| `X-ORIGIN`      | Marking origin of the objectClass definition - like metadata  |		
</div>

2.3 Object Definition

<div align=center>
	
| LDIF Term |  Explanation       |		
|------|---------------------------------------------------------------------------------------------------------|		
| `dn` | Distinguished Name or specific entry name in the LDAP directory |		
| `dc`| Domain Component - Like `dc=wikipedia,dc=org` from previous example  |		
| `cn`  | Common Name or the name of an object |		
| `ou`| Organisational Unit - basically objects used for organisational sub-groups |		
| `objectClass`  | assigning the type of object (that was created in previous step) to the objects |		
</div>

**3. Adding Entries of LDIF Files To Directory**
- Sequentially, ran the `ldapmodify -a -c -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!rEDACTED!]" -f <name>.ldif` command to create entries
	- *`-a`*: To add entries from the ldif file
	- *`-c`*: To continue processing the ldif file instead of stopping even if faced with error - [like `ignore_errors: yes` in Ansible-Playbooks](https://stackoverflow.com/questions/38876487/ansible-ignore-errors-in-tasks-and-fail-at-end-of-the-playbook-if-any-tasks-had)
	- *`-H`*: Specifying the LDAP URL of the LDAP server to connect to
	- *`-D`*: Defining the BindDN (explained before)
	- *`-w`*: For defining the password for the BindDN
	- *`-f`*: Filename of the LDIF file 

The verification of the addition of the entries was done by visiting the ApacheDS - which could have also been done using LDAPSearch by running a command like `ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" -LLL` - More on this in the coming section but `-b` refers to base/suffix/root of the DIT, essentially searching the entire DIT to match the condition.

<div align=center>

![img](https://i.imgur.com/5Dcy0oX.png)
</div>

### Modifying A Directory
Given that the entries from my LDIF File had been added to the directory, I modify these entries by creating another LDIF File called **[`modify.ldif`](https://github.com/YashAnand1/UnderstandingLDAP/blob/main/modify.ldif)**, whose explanation is given below:

<div align=center>

| LDIF Modifying Term | Explanation |			
|---|--------------|		
| `changetype`   | The type of modification operation: add / replace / delete |			
| `add` | To add new atribute-values |			
| `replace` | To replace existing values of an attribute |		
| `delete` | To delete value or its attribute |		
</div>

After the above file had been created, I ran the `ldapmodify -a -c -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!rEDACTED!]" -f modify.ldif` command to add the entries into my existing directory

The delete operation can be performed by writing an LDIF file - like my [`modify.ldif`](https://github.com/YashAnand1/UnderstandingLDAP/blob/main/modify.ldif) - or by using the `ldapdelete` or `ldapmodify` tools:
- Using `ldapdelete`:
```
ldapdelete -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" specificAttribute=specificValue,ou=organisationalUnit,dc=company,dc=com
```
- Using `ldapmodify`:
```
Ldapmodify -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" specificAttribute=specificValue,ou=organisationalUnit,dc=company,dc=com Changetype:delete
```

## Searching Using LDAPSearch
As discussed before, directories are optimised to provide a fast search result even with multiple-filters. In order to do so, the `ldapsearch` tool is brought to use for being able to filter in the following scenarios:
- Within Object: "Display all rooms assigned under the employees group (organisationalUnit)"
	- Done using base-searching:
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "ou=employees,dc=company,dc=com"
```
- Equality: "Display all rooms where the number of chairs (attribute) is exactly 5"
	- Done using base-searching:
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "ou=employees,dc=company,dc=com" "(chairs=5)"
```
- Exception: "Display every room where the tableColour (attribute) is not brown (is not equal to value)"
	- Done using base-searching:
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "dc=company,dc=com" "(&(objectClass=roomInfo)(!(tableColour=brown)))"
```
- Null: "Display all those rooms where the value of the chairColour attribute is empty/null"
	- Done using base-searching:
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "dc=company,dc=com" "(&(objectClass=roomInfo)(!(chairColour=*)))"
```
- Substring Search: "Display the rooms whose chairColour (attribute) starts with the letter "D" (Value substring)"
	- Done using base-searching:
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "dc=company,dc=com" "(chairColour=D*)"
```

For being able to get better at filtering searches while utilising the `ldapsearch` tool, [I practised 20 Questions/Situations](https://github.com/YashAnand1/UnderstandingLDAP/blob/main/LDAPSearching.md) based on the `roomInfo.ldif` that I had created earlier. 

## LDAP Installation
The following installations or setups were performed on my end for being able to work with LDAP:

**1. Containerising LDAP**
   - Creating Container: `podman run -d --name ldap-v1 -e DS_DM_PASSWORD=[!REDACTED!] -v /home/user/Desktop/ldap:/data --security-opt label=disable -p 3389:3389 docker.io/389ds/dirsrv:latest`
      - '-d' = detatched
      - '-e' = extras
      - '-v' = volume (for mounting)
      - '-p' = changeable outer port:default inner port

**2. Installing ldap-utils**
   - [LDAP-Utilities](https://wiki.debian.org/LDAP/LDAPUtils)
   	- Contains tools like `ldapsearch`, `ldapmodify`, `ldapdelete`, etc. that are used to interact with the LDAP Directories
   - Installation command: `sudo apt install ldap-utils`

**3. Setting-up Apache DirectoryStudio (ApacheDS)**
   - Downloaded tar file from the [ApacheDS website](https://directory.apache.org/studio/download/download-linux.html), untarred it & ran './ApacheDirectoryStudio'
   - Clicked 'Window -> Open Perspective -> Other -> LDAP (Default)'
   - Created a connection in the LDAP Browser using:
      - Name: originalConnection
      - Host: localhost
      - Port: 3389
      - bindDn: cn=Directory Manager (admin)
      	- This is the identity of LDAP Client that is given to LDAP Server for authentication - Kind of like a username.

## Resources
	
- [StackOverflow Post: What does LDAP solve?](https://stackoverflow.com/questions/884604/what-does-ldap-solve)	
	- For understanding the purpose of LDAP & use-cases
- [Hierarchical VS Flat Directories](https://stackoverflow.com/questions/40558806/best-directory-structure-for-static-files-hierarchical-vs-flat)	
	- Good for understanding through computer related examples
- [Hierarchical vs. Flat Organisational Structure](https://pingboard.com/blog/hierarchical-vs-flat-organizational-structure-and-benefits-of-each/) 	
	- Extremely great for general understanding with real life examples
- [DigitalOcean: How To Use LDIF Files to Make Changes to an OpenLDAP System](https://www.digitalocean.com/community/tutorials/how-to-use-ldif-files-to-make-changes-to-an-openldap-system)	
	- Explains Create, Update and Delete process using LDIFs really well
- [DigitialOcean: Understanding the LDAP Protocol, Data Hierarchy, and Entry Components](https://www.digitalocean.com/community/tutorials/understanding-the-ldap-protocol-data-hierarchy-and-entry-components#defining-ldap-data-components)	
	- Clears the fundamentals/basics to the terminologies such as Attributes, ObjectClasses, etc.
- [ServerFault Post: What is the difference between an RDN, a DN, and a CN in LDAP?](https://serverfault.com/questions/790108/what-is-the-difference-between-an-rdn-a-dn-and-a-cn-in-ldap)	
	- Helped clear my understanding of RDN, DN and CN through a simple language 
- [LDAP Official Document: Attribute Syntaxes](https://ldap.com/attribute-syntaxes/)	
	- For learning about the various data types of attributes 
- [Reddit Post: What are internet protocols?](https://www.reddit.com/r/learnprogramming/comments/3jjezp/what_are_internet_protocols/)	
	- Great for getting a basic idea of internet protocols through analogies
- [DevConnected Article: How To Search LDAP using ldapsearch](https://devconnected.com/how-to-search-ldap-using-ldapsearch-examples/)	
	- For understanding use-cases and scenarios in which ldapsearching can be made possible 
