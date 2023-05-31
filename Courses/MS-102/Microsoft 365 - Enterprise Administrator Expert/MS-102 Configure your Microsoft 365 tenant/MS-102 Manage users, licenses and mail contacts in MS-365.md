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

## Manage user licenses in MS 365

License provide access to MS 365 services (products), like Outlook and SharePoint online.  When an Administrator assigns a licese, MS 365 sets up the required services for the user.  For example, when an administrator assigns a license for SharePoint Online sets up 'edit' permissions.

Only members of the 'MS 365 Global Admin' and 'User Management' can assign or remove licenses from users.

**Warning** 
When and administrator removes a license from a user, the system deletes any service data that is associated with that user.  You then have a 30 day grace period to recover that data.  After this grace period the data is unrecoverable.

### Viewing user license information

The MS 365 admin centre provides acces to license and user information.  Admins can view this information through both the billiing and users drop downs.  Various filters can be used to refine the displayed information, for example to show unlicensed users.

### Assigning licenses

Administrators can use either the MS 365 admin centre or PowerShell to assign a license to a user.  Administrators can undertake bulk user maintenance using the MS 365 admin centre.

From within the MS 365 admin centre select:

Users -> Active User -> (select the relevant user) -> from the menu (ellipses) select Manage product licenses.

Administrators can assign licenses through either the MS 365 admin centre or through PowerShell. 

## Using Microsoft graph PowerShell to manage user licenes

Administrators must assign a location to user accounts.  The system requires a location when you create a new user in MS 365 admin centre.  By default, accounts syncronised from and organistion's on-premise Active Directory Domain Services don't have any location data.  Consequently, location data can be created from either:

1.  The MS 365 admin centre;
2.  Microsoft Graph PowerShell; and
3. The Azure Portal  (Active Directory > Users > user Account > Profile > Contact info > Country or region).

###  Finding unlicesed accounts using Microsoft graph PowerShell

Assigning and removing licenses for a user requires User.ReadWrite.All permission scope or one of the other permissions listed in the ['Assign license' Microsoft Graph API Reference page]()

PowerShell requires the Organization.Read.App permission scope to read the licenses available in the tenant.

~~~ powershell
Connect-MgGraph -Scopes User.ReadWrite.All, Organization.Read.All

# The 'Get-MgSubscribedSku' command shows the available licenses in each plan
Get-MgSubscribedSku

# To find the unlicensed accounts in your organisation, run the following command

Get-MgUser -Filter 'assignedLicense/$count eq 0' -ConsistencyLevel eventual -CountVariable unlicensedUserCount -All
~~~

Todo - there are heaps more PowerShell commands to add here.

### Assigning licenses to user accounts

To assign a license to a user, use the following command:

``` powershell

Set-MgUserLicense -UserId $userUPN -AddLicense @(SkuId = "<SkuId>") -RemoveLicense@()

```

## Recover deleted user accounts in Microsoft 365

When an employee leaves an organisation, it is good practice to delete the corresponding user account.  This also results in recovering all of the licenses that were being used by that user.

### Deleting a user account

User accounts can be deleted from within the MS 365 admin centre.  

Users -> Active users -> (select the relevant user) Delete user -> (from the delete users pane) Delete user -> close

Users can also be deleted using MS Graph PowerShell using the 'Remove-MgUser' with the -UserIdstring parameter

``` powershell

Remove-MgUser -UserId '5c442efb-5e66-484a-936a-91b6810bed14'

```

### Restoring a deleted user account

When a user is deleted, it initially becomes inactive so that the user can no loger sign in.  MS 365 provides a 30 day grace period, during which deleted accounts can be recoered.  After this 30 day period the account can no longer be recovered.

1.  To restore a user account select the Users -> Active Users -> Deleted users ;
2.   Select the deleted user that you want to recover and then select the Restore user option; and
3. You will also need to select how a password is assigned.

Accounts can also be recovered using the MS Graph PowerShell using the Restore-MgDirectoryDeletedItem.

``` powershell

Restore_MgDirectoryDeletedItem -DirectoryObjectId '5c442efb-5e66-484a-936a-91b6810bed14'

```

## Perform bulk user maintenace in Azure Active Directory

Azure AD enables organisations to undertake bulk user maintenance including creating and deleting users as well as restoring deleted users.  

### Create users in bulk

Buld user operations require the use of CSV files.  The format for the CSV file for each of the create, delete and restore functions.  

The first 2 rows of the CSV are reserved for the version number and the column headings.  Initially, the third row has an example, however, this row is replaced by the first row of users to be uploaded. 

1.  Row one contains the version number;
2.  Row two contains the column headings in the format  - item name [propertyName] Required or blank e.g. Name[displayName] Required; and
3.  Examples.

In order to bulk create new users, administrators must have wither Global Admin or User Admin.

#### Check status of your bulk operations

The status of bulk administration processes can be checked in the Azure AD admin portal.

#### Verify the users were created

Verification can be undertaken either through the Azure AD admin portal of PowerShell.  Either Global Admin or User Admin permissions are required.

#### Delete users in bulk

Just as adding users in bulk, users can also be deleted in bulk.  The processes is basically the same as adding users in bulk.

#### Restore users in bulk

This is the same process as creating and deleting users in bulk.

#### Creating users in bulk using PowerShell

See Additional Learning for details on how to connect and configure Microsoft Graph PowerShell.

### Create and manage guest users

MS 365 has the facility to add guest users, which permits collaboration with users external to the tenant.  In order to provide external access, administrators must have either Global Admin, Guest Inviter or User Admin.

Administrators can add guest users to either Azure AD, Groups of Applications.  Guest users are added to Azure AD with type 'Guest'.  The guest user much redeem their invitation before they can begin collaborating with organisational users.

Once the end user has been added to the host organisations Azure Active Directory , the guest user can select either:

1.  A direct link to a shared application; or
2. The redemption URL in the invitation email they received.

Note - Guest invitations do not expire.

By default, guest access is enabled by default in MS 365 and the MS 365 Administrator controls whether or not a guest has access to all groups, a subset of groups or the entire organisation.

In addtion to MS 365 other apps also have the capacity to provide guest access.  These include:

1.  Power Apps;
2. Lists;
3. OneDrive;
4. Planner;
5. MS 365 Groups; and
6. Yammer.

#### Restrict guest access permissions in Azure AD

There are three different permissions models for guest access.  These are:

1.  Same as member users;
2. Limited access (default); and
3. Restricted access.

When guest users have restricted access, they can only view their own profile.  They don't have permission to view other users, even if the guest searches by User Principal Name or object Id.  Restricted access also restricts guest users from seeing the membership of groups they're in.  

External collaboration settings let an organisation specify what roles it can invite external users for B2B collaboration.  These settings also include options for allowing or blocking specific domains and options for restricting what external guests can see in your Azure AD directory.   The following options:

1.  Determine guest user access;
2. Specify who can invite guests;
3. Enable guest self-service sign-up via user flows; and
4. Allow or block domains.

Cross-tennant access settings provide the capacity to configure access to other Azure AD Organisations.  This ensure both inbound and outbound collaboration and specifies access to user, groups and applications.  

Guest access permissions are set in Azure AD.

Microsoft 365 admin centre ->  Admin centres -> Azure AD -> User settings -> Manage External collaboration settings

#### Add guests in (Active Directory, a group and an application)

Todo --> add processes here

### Create and manage mail contacts

In Exchange Online Organizations, mail contacts are mail enabled objects that contain information about people that exist outside of your organization.  

#### Permissions needed to create mail contacts

The required permissions for creating mail contacts can come from either:

1.  Recipient Management role group;
2. Organization Management role group; and
3. Mail recipient role.

#### Use the new EAC to create mail contacts

Use the following steps to create mail contacts in the new Exchange Admin Centre (EAC):

1.  

#### Use the new EAC to modify mail contacts

#### Use the new EAC to remove mail contacts

#### Use Exchange Online PowerShell to modify mail contacts

#### Use Exchange Online PowerShell to modify mail contacts

#### Use Exchange Online PowerShell to remove mail contacts

















