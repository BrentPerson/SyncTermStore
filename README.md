.Synopsis        
        Script to migrate an OnPrem term store to SharePoint Online
        This Script Assumes you've installed SharePoint in the default location
        This Script currently does not support user mapping to SPO user
        This Script currently only supports a single TermStore associated with the OnPrem web application and it must be the default TermStore
        
        **Change the location of the sharepoint client .dll files to fit your environment**

    .Prerequisites
       SharePoint Online Client SDK version 16.0.7018.1200 or higher
       TermStore Administrator Rights
    
    .Example
        '.\MigrateOnPremTermStoreToSPO.ps1' -SrcSiteUrl https://www.contoso.com -SrcUsername contoso\admin -SrcPassword **** -SPOSiteUrl https://contoso.sharepoint.com -SPOUsername Admin@contoso.onmicrosoft.com -SPOPassword **** -GroupList ("Group1","Group2","Group3","Group4")
    
    .Notes
        Name: MigrateOnPremTermStoreToSPO.ps1
        Author: Brent Person, Microsoft, brpers@microsoft.com
        Created: 7/10/2020
        Last Edit: 07/22/2020
