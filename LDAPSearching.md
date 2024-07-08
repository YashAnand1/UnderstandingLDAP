# LDAPSearching Practice Paper

The 20 questions mentioned within this document are strictly based on the [Sample-Directory](https://github.com/YashAnand1/UnderstandingLDAP/tree/main?tab=readme-ov-file#working-with-directories) that has been created by me for the main 'Understanding LDAP' document. For understanding the structure of the directory for which these questions have been framed, click on the above hyperlink.   

## 1. Find all rooms with more than 5 spinny chairs.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "dc=company,dc=com" "spinnyChairNo=4" spinnyChairNo -LLL

dn: cn=Indigo,ou=employees,dc=company,dc=com
spinnyChairNo: 4
```

## 2. Search for rooms that have a spinny chair color of blue.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "dc=company,dc=com" "(spinnyChairCol=blue)" spinnyChairCol -LLL
dn: cn=ShantiNiketan,ou=contractors,dc=company,dc=com
spinnyChairCol: blue

dn: cn=Nalanda,ou=interns,dc=company,dc=com
spinnyChairCol: blue
```

## 3. Find rooms that have both black wheelless chairs and tables of any color.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "(&(wheellessChairCol=BLack)(tableCol=*))" -LLL

dn: cn=Aryabhat,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Aryabhat
spinnyChairNo: 5
spinnyChairCol: black
wheellessChairNo: 7
wheellessChairCol: black
tableNo: 1
tableCol: light-brown
purchase: 20121014083000Z
secondHand: FALSE

dn: cn=Patliputra,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Patliputra
spinnyChairNo: 10
spinnyChairCol: black
wheellessChairNo: 25
wheellessChairCol: black
tableNo: 6
tableCol: dark-brown
purchase: 20060914211600Z
secondHand: TRUE

dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
spinnyChairCol: blue
wheellessChairNo: 9
wheellessChairCol: black
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE
```

## 4. Search for rooms where the purchase date is after January 1, 2015.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "dc=company,dc=com" "(purchase>=201501)" -LLL

dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
spinnyChairCol: blue
wheellessChairNo: 9
wheellessChairCol: black
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE

dn: cn=Kitchen,ou=common,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: kitchen
spinnyChairNo: 0
spinnyChairCol: N/A
wheellessChairNo: 30
wheellessChairCol: Red
tableNo: 4
tableCol: Dark-brown
purchase: 20231014153500Z
secondHand: TRUE
```

## 5. Find all rooms that are second-hand.
```
ldapsearch -H ldap://localhost:3389 -D 'cn=Directory Manager' -w [!REDACTED!] -b "dc=company,dc=com"
"(secondHand=TRUE)" -LLL

dn: cn=Patliputra,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Patliputra
spinnyChairNo: 10
spinnyChairCol: black
wheellessChairNo: 25
wheellessChairCol: black
tableNo: 6
tableCol: dark-brown
purchase: 20060914211600Z
secondHand: TRUE

dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
spinnyChairCol: blue
wheellessChairNo: 9
wheellessChairCol: black
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE

dn: cn=Kitchen,ou=common,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: kitchen
spinnyChairNo: 0
spinnyChairCol: N/A
wheellessChairNo: 30
wheellessChairCol: Red
tableNo: 4
tableCol: Dark-brown
purchase: 20231014153500Z
secondHand: TRUE
```

## 6. Search for rooms that belong to contractors and have more than 10 wheelless chairs.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "ou=contractors,dc=company,dc=com" "wheellessChairNo>=10" -LLL

dn: cn=Patliputra,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Patliputra
spinnyChairNo: 10
spinnyChairCol: black
wheellessChairNo: 25
wheellessChairCol: black
tableNo: 6
tableCol: dark-brown
purchase: 20060914211600Z
secondHand: TRUE
```

## 7. Find rooms that are assigned to interns and have a table color of light-brown.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "ou=interns,dc=company,dc=com" "tableCol=light-brown" -LLL

There was no output because a light-brown tableCol does not actually exist in the intern group 
```

## 8. Search for rooms with a specific common name (e.g., Indigo).
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "(cn=Indigo)" -LLL

dn: cn=Indigo,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Indigo
spinnyChairNo: 4
spinnyChairCol: black
wheellessChairNo: 10
tableNo: 20
tableCol: woodish-brown
purchase: 20121014083500Z
secondHand: FALSE
wheellessChairCol: Red
```

## 9. Find all common rooms with more than 20 chairs (both spinny and wheelless combined).
```
# Not done at first try

The 'answer' considers 2 cases where the spinnyCount is first more than 20 while wheellessCount is 0 and vice versa.

This answer appears to be wrong to me because there would likely be more cases to satisfy 'spinnyCount+wheellessCount>=20'.
```

## 10. Search for rooms that have been assigned to employees and have spinny chairs of any color except black.
```
# Not done at first try
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "(&(objectClass=roomInfo)(!(spinnyChairCol=black)))" -LLL

dn: cn=ShantiNiketan,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: ShantiNiketan
spinnyChairNo: 6
spinnyChairCol: blue
wheellessChairNo: 3
wheellessChairCol: blue
tableNo: 7
tableCol: light-brown
purchase: 20060914211200Z
secondHand: FALSE

dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
wheellessChairNo: 9
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE

dn: cn=Kitchen,ou=common,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: kitchen
spinnyChairNo: 0
spinnyChairCol: N/A
wheellessChairNo: 30
wheellessChairCol: Red
tableNo: 4
tableCol: Dark-brown
purchase: 20231014153500Z
secondHand: TRUE
```

## 11. Find rooms that have tables purchased after 2020 and are marked as second-hand.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "dc=company,dc=com" "(&(purchase>=2010)(secondHand=TRUE))" -LLL
dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
spinnyChairCol: blue
wheellessChairNo: 9
wheellessChairCol: black
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE

dn: cn=Kitchen,ou=common,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: kitchen
spinnyChairNo: 0
spinnyChairCol: N/A
wheellessChairNo: 30
wheellessChairCol: Red
tableNo: 4
tableCol: Dark-brown
purchase: 20231014153500Z
secondHand: TRUE
```

## 12. Search for rooms that belong to interns and have wheelless chairs with the color blue.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w [!REDACTED!] -b "ou=interns,dc=company,dc=com" "(wheellessChairCol=blue)" -LLL
No output because there are no wheel-less chairs in interns' room
```

## 13. Find all rooms with a purchase date in the year 2012.
```
ldapsearch -H "ldap://localhost:3389" -D "cn=Directory MANAGER" -w "[!REDACTED!]" -b "dc=company,dc=com" "purchase>=2012" -LLL
dn: cn=Indigo,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Indigo
spinnyChairNo: 4
spinnyChairCol: black
wheellessChairNo: 10
tableNo: 20
tableCol: woodish-brown
purchase: 20121014083500Z
secondHand: FALSE
wheellessChairCol: Red

dn: cn=Aryabhat,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Aryabhat
spinnyChairNo: 5
spinnyChairCol: black
wheellessChairNo: 7
wheellessChairCol: black
tableNo: 1
tableCol: light-brown
purchase: 20121014083000Z
secondHand: FALSE

dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
spinnyChairCol: blue
wheellessChairNo: 9
wheellessChairCol: black
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE

dn: cn=Kitchen,ou=common,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: kitchen
spinnyChairNo: 0
spinnyChairCol: N/A
wheellessChairNo: 30
wheellessChairCol: Red
tableNo: 4
tableCol: Dark-brown
purchase: 20231014153500Z
secondHand: TRUE
```

## 14. Search for rooms that have a table color containing the substring "brown".
```
# Not done at first try

ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "tableCol=*brown" -LLL

dn: cn=Indigo,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Indigo
spinnyChairNo: 4
spinnyChairCol: black
wheellessChairNo: 10
tableNo: 20
tableCol: woodish-brown
purchase: 20121014083500Z
secondHand: FALSE
wheellessChairCol: Red

dn: cn=Aryabhat,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Aryabhat
spinnyChairNo: 5
spinnyChairCol: black
wheellessChairNo: 7
wheellessChairCol: black
tableNo: 1
tableCol: light-brown
purchase: 20121014083000Z
secondHand: FALSE

dn: cn=Patliputra,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Patliputra
spinnyChairNo: 10
spinnyChairCol: black
wheellessChairNo: 25
wheellessChairCol: black
tableNo: 6
tableCol: dark-brown
purchase: 20060914211600Z
secondHand: TRUE

dn: cn=ShantiNiketan,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: ShantiNiketan
spinnyChairNo: 6
spinnyChairCol: blue
wheellessChairNo: 3
wheellessChairCol: blue
tableNo: 7
tableCol: light-brown
purchase: 20060914211200Z
secondHand: FALSE

dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
wheellessChairNo: 9
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE

dn: cn=Kitchen,ou=common,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: kitchen
spinnyChairNo: 0
spinnyChairCol: N/A
wheellessChairNo: 30
wheellessChairCol: Red
tableNo: 4
tableCol: Dark-brown
purchase: 20231014153500Z
secondHand: TRUE
```

## 15. Find rooms that are not second-hand and have spinny chairs with a count of 4.

```
ldapsearch -H "ldap://localhost:3389" -D "cn=Directory MANAGER" -w "[!REDACTED!]" -b "dc=company,dc=com" "(&(secondHand=FALSE)(spinnyChairNo=4))" -LLL

dn: cn=Indigo,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Indigo
spinnyChairNo: 4
spinnyChairCol: black
wheellessChairNo: 10
tableNo: 20
tableCol: woodish-brown
purchase: 20121014083500Z
secondHand: FALSE
wheellessChairCol: Red
```

## 16. Search for rooms belonging to common areas with tables of any color except dark-brown. 
```
*Could not attempt on the first try*

ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "(&(objectClass=roomInfo)(!(tableCol=Dark-brown)))" -LLL

dn: cn=Indigo,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Indigo
spinnyChairNo: 4
spinnyChairCol: black
wheellessChairNo: 10
tableNo: 20
tableCol: woodish-brown
purchase: 20121014083500Z
secondHand: FALSE
wheellessChairCol: Red

dn: cn=Aryabhat,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Aryabhat
spinnyChairNo: 5
spinnyChairCol: black
wheellessChairNo: 7
wheellessChairCol: black
tableNo: 1
tableCol: light-brown
purchase: 20121014083000Z
secondHand: FALSE

dn: cn=ShantiNiketan,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: ShantiNiketan
spinnyChairNo: 6
spinnyChairCol: blue
wheellessChairNo: 3
wheellessChairCol: blue
tableNo: 7
tableCol: light-brown
purchase: 20060914211200Z
secondHand: FALSE

dn: cn=Nalanda,ou=interns,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Nalanda
spinnyChairNo: 21
wheellessChairNo: 9
tableNo: 10
tableCol: chocholate-brown
purchase: 20241024143500Z
secondHand: TRUE
```

## 17.  Find rooms with more than 10 wheelless chairs and a purchase date before 2010.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "(&(wheellessChairNo>=10)(purchase<=2010))" -LLL
dn: cn=Patliputra,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Patliputra
spinnyChairNo: 10
spinnyChairCol: black
wheellessChairNo: 25
wheellessChairCol: black
tableNo: 6
tableCol: dark-brown
purchase: 20060914211600Z
secondHand: TRUE
```

## 18. Search for rooms assigned to employees that have both black spinny chairs and black wheelless chairs.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "(&(wheellessChairCol=black)(spinnyChairCol=black))" -LLL
dn: cn=Aryabhat,ou=employees,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Aryabhat
spinnyChairNo: 5
spinnyChairCol: black
wheellessChairNo: 7
wheellessChairCol: black
tableNo: 1
tableCol: light-brown
purchase: 20121014083000Z
secondHand: FALSE

dn: cn=Patliputra,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Patliputra
spinnyChairNo: 10
spinnyChairCol: black
wheellessChairNo: 25
wheellessChairCol: black
tableNo: 6
tableCol: dark-brown
purchase: 20060914211600Z
secondHand: TRUE
```

## 19.Find all rooms with spinny chairs but no wheelless chairs.
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "dc=company,dc=com" "(&(wheellessChairNo>=1)(spinnyChairNo=0))" -LLL

dn: cn=Kitchen,ou=common,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: kitchen
spinnyChairNo: 0
spinnyChairCol: N/A
wheellessChairNo: 30
wheellessChairCol: Red
tableNo: 4
tableCol: Dark-brown
purchase: 20231014153500Z
secondHand: TRUE
```

## 20. Search for rooms that belong to contractors and have tables with a specific color (e.g., dark-brown).
```
ldapsearch -H ldap://localhost:3389 -D "cn=Directory Manager" -w "[!REDACTED!]" -b "ou=contractors,dc=company,dc=com" "(tableCol=dark-brown)" -LLL

dn: cn=Patliputra,ou=contractors,dc=company,dc=com
objectClass: roomInfo
objectClass: top
cn: Patliputra
spinnyChairNo: 10
spinnyChairCol: black
wheellessChairNo: 25
wheellessChairCol: black
tableNo: 6
tableCol: dark-brown
purchase: 20060914211600Z
secondHand: TRUE
```
