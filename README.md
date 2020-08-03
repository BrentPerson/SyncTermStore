Script: DocumentPinnedReusedTerms.ps1
.Synopsis        
        Script to output all the Reused and Pinned terms where the term is not a source term to csv file from SharePoint OnPrem.
	This will create a CSV file per Term Group for both pinned and reused terms

	**Change the following to fit your environment
		$SrcSiteUrl = "https://sp16.contoso.com"
		$outputFilePath = "C:\Scripts\TermStoreMigration\output\"
		$TermStoreName = "MMD_Restored"
    .Notes
        Name: DocumentPinnedReusedTerms.ps1
        Sources: 
        Author: Brent Person, Microsoft, brpers@microsoft.com
        Last Edit: 07/11/2019


Script: 
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


Script: FindMIssingTermsInTermSet.ps1
.Synopsis        
        Validation script to find missing/extra terms in specified Term Group/Term Set
        Change the variables to fit your environment
    .Notes
        Name: FindMissingTermsInTermSet.ps1
        Sources: 
        Author: Brent Person, Microsoft, brpers@microsoft.com
        Last Edit: 07/10/2019
