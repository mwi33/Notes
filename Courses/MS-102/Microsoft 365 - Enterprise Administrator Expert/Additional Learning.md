## Microsoft Graph PowerShell

PowerShell can be used for many administrative function.  Microsoft Graph PowerShell must be installed, import the Microsoft.Graph.Identity.DirectoryManagement module and connect to MgGraph with the correct permissions.  

``` powershell

Install-Module Microsoft.Graph -Scope CurrentUser
Import-Module Microsoft.Graph.Identity.DirectoryManagement
Connect-MgGraph -Scopes 'User.ReadWrite.All'

```

With this done, the New-MgUser cmdlet can be used to create a user account.  The bulk upload process with PowerShell still requires that the required user data is cotained in a csv file.

``` powershell

Import-Csv -Path <Input CSV File Path and Name> | foreach {New-MgUser -DisplayName $_.DisplayName -GivenName $_.FirstName -Surname $_.LastName -UserPrincipalName $_.UserPrincipalName -UsageLocation $_.UsageLocation -LicenseAssignmentStates $_.AccountSkuId -PasswordProfile $_.Password} | Export-Csv -Path <Output CSV File Path and Name>

```

The above command can also include writing the results of the upload to a csv file for future reference.

``` powershell

# the following parameter is appended to the bulk upload command to write
# the results of the upload

Export-Csv -Path "C:\My Documents\NewAccountResults.csv"

```

## Microsoft Graph API

## Connect to Microsoft 365 with PowerShell

[PowerShell for MS 365](https://learn.microsoft.com/en-us/microsoft-365/enterprise/connect-to-microsoft-365-powershell?view=o365-worldwide) enables you to manage your MS 365 settings from the command line.

There are two versions of PowerShell which can be used to connect to MS 365.  These are:

1.  Azure Active Directory PowerShell for Graph, whose cmdlets include AzureAD in their name; and
2. Microsoft Azure AD module for Windows PowerShell, whose cmdlets include Msol in their name.

## Microsoft Azure Cloud Shell

You will need an active Azure subscription for your subscription that is tied to your MS365 to access [Azure Cloud Shell](https://learn.microsoft.com/en-us/microsoft-365/enterprise/connect-to-microsoft-365-powershell?view=o365-worldwide#connect-with-the-azure-cloud-shell) 