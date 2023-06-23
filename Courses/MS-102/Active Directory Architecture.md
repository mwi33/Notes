Trying to understand how all the various AD/IM components fit together:

* Azure AD;
* Azure AD Connect;
* Local AD
* Active Directory Domain Services*

Azure AD - In a nutshell, this is your cloud-native identity platform.

Local AD - This is your on-premise (runs on a server on-site) identity platform and directory service. It handles identity by keeping records of user accounts and devices.

Azure AD Connect - This is a component that sync's your local AD directory into Azure AD. This is effectively the component that allows identity to exist in a hybrid state (on-prem and cloud).

Active Directory Domain Services* - This a component of Active Directory that focuses on managing the user accounts and devices. AD DS lets you control access to the network and resource control (who and what can access what resources through various permission levels).
