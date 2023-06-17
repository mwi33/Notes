After an organisation creates its users it can then use groups for collaboration between users, both internal and external to the organisation.  

Within Exchange Online, groups enable organisations to distribute email to multiple users.  Within SharePoint Online, groups support cross-team collaboration.

With the correct permissions set, organisations can add users to groups from external organisations.

## Examine groups in Microsoft 365

M365 uses groups to manage and organise sets of users.  When assigning a team to a group, the group can facilitate permissions management on a SharePoint team site.  Additionally, the group enables the distribution of messages to all of its members.

|Group Type | Description | When to use | Where to create it|
|-------------|--------------|---------------|---------------------|
|MS 365 group | This is the recommended group.  Has it's own mailbox.  Users receive group emails.  Supports collaboration with shared workspace, conversations, files and calendar events.  |When you want to provide distribution list capabilities and other collaboration features.  Best for team work.  | -MS 365 admin centre; -MS 365 app; MS Entra; Exchange admin centre; Outlook|
|Distribution group | Also known as a distribution list.  Organisations often use this for email distribution purposes.  It allows emails to be sent to all group members by using a single email address associated with the group.  The organisations mail server distributes the email to individuals in the group.  |When you want to distribute messages using the group only. | - MS 365 admin centre; -MS 365 app; Exchange admin centre|
|Mail-enabled security group | A mail enabled security group has an email address associated with it that enables members to send and receive emails.  This group functions as a mailing or distribution list.  It can also be used as a security group and provide access to other resources like SharePoint.  Members will then have access to have access to sites, libraries, lists or other individual items within SharePoint. |When you want to use the group for permissions and mail distribution.| - MS 365 admin centre; -MS 365 app; Exchange admin centre |
|Security group | A security group provides a convenient way to manage and assign permissions to multiple users simultaneously.  A security group can grant access permissions to resources such as OneDrive and SharePoint.  |When you only require a group to provide permissions| - MS 365 admin centre; -MS 365 app; MS Entra admin centre |
|Dynamic distribution group | This group automatically manages its membership based on pre-defined criteria or filters.  Traditionally, members are added to groups manually, in a dynamic distribution group membership is updated based on rules.  This group is created and managed from the Exchange Admin Centre.  Rules can be based on department, location, job title or custom attributes.  |When you want a flexible distribution list that changes membership automatically.| - Exchange admin centre|

MS 365 groups contain objects.  These are:
* A shared outlook inbox;
* A shared calendar;
* A SharePoint teams site
* A SharePoint document library;
* Planner;
* PowerbI
* Yammer if you created the group from Yammer;
* A Team if you created the group from Teams; and
* A Roadmap if you have project for the web.

## Create and manage groups in MS 365

It is important that certain practices are applied consistently to ensure that groups and their members can securely and reliably access required services and resources.  The following are considered best practice with regard to the creation of groups:

* Keep naming conventions simple and applied consistently;
* Create policies and procedures for ongoing group maintenance;
* Add users to security groups and then add those security groups to default groups rather than adding individual users to the groups;
* Maintain a consistent and well-defined account provisioning process; and
* Assign at least two owners to a group for redundancy.

MS 365 groups can be created using PowerShell and MS Graph.

~~~ powershell

# Create a MS365 group with PowerShell and MS Graph

New-MgGroup -DisplayName 'Test Group' -MailEnabled:$False -MailNickName 'Test Group' -SecurityEnabled

~~~

The MS Admin Centre provides the 'Type' of groups available to the organisation.  

MS 365 supports nesting of groups.  That is the ability to add one group as a member of another group.  Completing this is essentially the same as adding a user to a group.  Select the relevant group instead of a user.  There are some limitations and some groups can't be added to certain group types.

TODO:  Add the groups matrix.

## Deleting and restoring groups

TODO: Add process

## Manage group-based licensing in Azure Active Directory

Most services and products in the Microsoft Cloud suite require a license of some type.  Typically, administrators use one of several admin centers to assign the required licenses to users.  Azure AD includes the facility to assign licenses to groups, which in turn assigns the license to the members of that group.  This function is only available through Microsoft Entra Admin Centre in Azure AD.

This eliminates a 'per-user' based approach to license management.

### Group-based licensing requirements

You must have one of the following licenses for every user who benefits from group-based licensing"

* Paid or trial subscription for Azure AD Premium P1 and above;
* Paid or trial edition of Microsoft 365 Business Premium or Microsoft 365 Enterprise E3 or Microsoft 365 A3 or Microsoft 365 GCC G3 or Microsoft 365 E3 for GCCH or Microsoft 365 E3 for DoD and above.

### Group-based licensing features

* Organisations can sync their on-premise security groups through Azure AD Connect.  Cloud only groups can also be created in Azure AD;
* Administrators can disable one or more service plans in the product.  For example, an organisation can assign MS 365 to a group and disable 'Yammer' until the organisation is ready to use it;
* Support all Microsoft Cloud Services  that require user level licensing;
* Group-based licensing is only available through the Azure Portal;
* Azure AD automatically manages license modifications that result from group membership changes;
* A user can be a member of multiple-groups with license policies specified.  A user can also have licenses assigned outside of group-based licenses.  The user then has the aggregate of the licenses assigned.  If the same license is applied more than once as a result of multiple group based assignments, the system consumes only one; and
* In some cases, you can't assign licenses to a user.  For example, there may not be enough license for all members of a group.  In this instance, administrators can access information about user which Azure AD couldn't fully process the license assignment.


