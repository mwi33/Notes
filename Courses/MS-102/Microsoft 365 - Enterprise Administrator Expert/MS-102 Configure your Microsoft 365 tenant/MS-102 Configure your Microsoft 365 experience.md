A M365 subscription is a paid plan that provides access to various M365 cloud services (exchange, sharepoint, onedrive e.t.c).  With a subscription, an organisation can create users accounds, assign licenses to these accounds and manage subscription settings.
A tenant is a dedicated instance of the Microsoft cloud environment.  The tenant is used to manage its subscriptions and associated resources.  When an organisation signs up for M365 subscription Microsoft automatically creates a tenancy for the company.  This tenant becomes the central hub for the organisation to manage all of its subscription's resources including users, domains and settings.

The tenant domain is based on the domain name provided during signup and typically looks like:

https://contoso.onmicrosoft.com

An organisations M365 tenant includes Azure AD tenant.  The Azure AD tenant is a dedicated instance of Azure AD for storing the company's M365 user accounts, groups, and other objects.  Each Azure AD tenant is distinct, unique and separate from all othe Azure AD tenants.  

Whilst an organisation can have more than one Azure AD tenant a M365 tenant can only use a single Azure AD tenant.  That Azure AD tenant must be the one that Microsoft created when it create the M365 tenant.  

## A properly configured tenant

A properly configured tenant considers/implements:

1. The correct set of products (subscriptions) and licenses;
2.  For networking,  it configured the correct DNS domain names, network traffic is optimised for on-premise workers, and VPN traffic for off-site workers
3. If it has on-premise AD Domain Service, it synchronised accounts, groups, and other objects.  It mapped Azure AD tenant accounts to Exchange on-line mailboxes with correct  DNS domains for email addresses.  I assigned its user accounts the correct licenses from the correct purchased products (E3, E5 e.t.c.);
4. Configured strong identity and access management.  It requires sign-in with passwordless or MFA.  It created conditional access policies that enforce sign-in requirements and restrictions for higher levels security.
5.  It performs device management with Intune or Basic Mobility and security built into M365.

A [[Tenant Configuration Checklist]] of the core components required to configure a tenant is a useful resource for the initial build.

## Microsoft 365 Conceptual Architecture

When an organisation signs up for a subscription, Microsoft 365 creates the tenant.  Each tenant is distinct.  Each tenant has it's own instance of Azure Active DIrectory (AD).  

Additional subscritptions can be added to the tenant as required.  Within an organisation, individual employees require a license to use products or services included in a subscription.

todo - add architecture
Tenant - organisation domain and geographic location
Subscription - Microsoft 365 Business Premium
License - E3

## Enterprise deployment lifecycle

Planning --> Purchasing --> Deployment --> Operations --> Support --> Upgrade and retire

## Planning

1.  Computer strategy;
2.  Computer selection;
3.  Deployment methods;
4.  Demand forecasting; and
5.  Design configuration

## Purchasing
1.  Hardware;
2.  Software;
3.  Accessories;
4. Deployment process; and
5. Hardware staging.
## Deployment
1.  Build;
2.  Deployment;
3.  Enrollment; and
4.  Data Migration.
	1. Known Folder Move

Enterprise State Roaming 
User State Migration tool (10.0)
	USMT migrates user accounts, user files, operating system settings and application settings to a new windows.  You can use USMT for both PC replacement and PC refresh migrations.

Planning an application deployment consists of 3 phases: managing application inventory and compatability; packaging applications; and providing life-cycle support.

Microsoft Intune Suite is used to take an application inventory.  

## Operations

## Support

## Upgrade

## Retire

Windows Autopilot - Windows autopilot joins the device to AD and enrols in intune.

Azure active directory - 

Intune -  Intune automatically applies users' email, apps, files, preferences, and security settings without the need for a custom OS image

MS intelligent security graph

Microsoft 365 Configuration Process

1.  Setting up your organisational profile
2. Managing your tenant subscriptions
3. 