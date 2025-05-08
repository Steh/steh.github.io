---
title: "ldapsearch"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "ldapsearch is a command-line tool for querying and retrieving data from LDAP (Ligthweight Directory Access Protocol) directories. It supports search filters, authentication, and displays results in LDIF format." 
toc: true
--- 

´´´bash
# -x   -> simple authentication
# -LLL -> supresses printing of version number and comments
# -b   -> base DN
ldap -x -LLL -b "C=DE" "(serialNumber=*)" -H ldap://server.example

# example search that only returns the specified attributes
ldap -x -LLL -H ldap://ldap.example.com -b "dc=example,dc=com" "(mail=*)" cn mail uid
´´´

## source

* [ldapsearch manpage][def]

[def]: https://www.man7.org/linux/man-pages/man1/ldapsearch.1.html
