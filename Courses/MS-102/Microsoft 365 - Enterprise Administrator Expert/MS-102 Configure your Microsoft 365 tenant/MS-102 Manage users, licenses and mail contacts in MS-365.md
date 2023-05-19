# Overview

An Enterprise Administrator is responsible for creating and managing all the companies MS 365 user accounts.

This process includes:
1.  Creating and managing user accounts;
2.  Assigning MS 365 licenses to users;
3.  Recovering deleted user accounts.

This process starts with identifying which user identity model is best suited for your organisation.  From there, user accounts can be added.

This module includes how to create accounts from the MS 365 admin centre and Windows PowerShell.

There are 3 different types of 'user identity model'.  These are:
1.  Cloud identities;
2.  Synchronised identities; and
3.  Federated identities.

## Cloud identities

A cloud identity is an identity that only exists in Azure AD.  Whilst organisation can create identities with the same name as on-premise accounts Active Directory Domain Services (AD DS) user account, there is no link between the two accounts.  

## Synchronised identities

A synchronised identity is a identitiy that exists in both on-premise AD DS and MS 365.  Changes made in the on-premise AD DS system are then synchronised with the MS 365 user account.  

Azure Active Directory Account (Azure AD Connect) undertakes the synchronisation once an organisation downloads and installs it in its on-premises environment.  Azure AD Connect filters the synchronised accounts and determines whether to synchronise passwords.

When organisations implements synchronised identities, the on-premise AD DS system is authoratitive.  As such, administrators must complete most administrative tasks on-premise.  The system then synchronises these changes to Azure AD.  Only a small set of attributes from MS 365 back to AD DS on-premise.

Authentication for synchronised identities occurs in MS 365.  MS 365 evaluates username and password without any reliance on the on-premise infrastrucuture.

## Federated identities

A federated identity is a synchronised user account that the LDAP (Lightweight Directory Access Protocol) on the AD DS authenticates.  The authentication process creates a local claims provider trust with the Active Directory Federated Services (ADFS). 

ADFS is deployed on an organisations on-premise network/infrastructure.  ADFS then communicates with AD DS on-premises.  As such, Azure AD authorises federated user accounts to access resources in MS 365 based on LDAP policy on AD DS (through AD FS).

In this model, authentication to MS 365 requires access to AD FS.  Consequently, service interruptions to the on-premises infrastructure can affect MS 365 authentication.

The main benefit of using federated identities is Single Sign-On.

Azure AD - Authorises federated user accounts to access resources in MS 365 based on LDAP policy located on AD DS (through AD FS). 

AD DS - 

Azure AD Connect - 

What is Azure AD Connect?

What is Active Directory Federated Services infrastructure?

## Determining the best model for your organisation

Todo - add table here

## Create user accounts in MS 365

Depending on organisational needs, provision of user accounts can be accomplished several ways:

1.  MS 365 admin centre;
2.  Import multiple users;
3.  Windows PowerShell; and
4. Directory synchronisation.

### Creating a user

1.  Select 'Users' - > 'Active users' - > "Add a user";
2.  Basics;
3.  Product licenses;
4.  Optional settings; and
5.  Finish.

## Manage user account settings in MS 365

Managing user accounts involves managing several account settings:

1.  Assigning adminstrator roles;
2.  Setting users sign-in status;
3.  Specifying user location settings; and
4. Assigning licenses.




