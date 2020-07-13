# SyncTermStore
scripts used to sync your Term Store to SharePoint Online or On-Premises


<#
    .Synopsis        
        Script to migrate an OnPrem term store to SharePoint Online
        This Script Assumes you've installed SharePoint in the default location
        This Script currently does not support multilingual termstores
        This Script currently does not support user mapping to SPO user
        This Script currently only supports a single TermStore associated with the OnPrem/Source web application and it must be the default TermStore

        .Example:
        	.\MigrateOnPremTermStoreToSPO.ps1 -SrcSiteUrl https://www.contoso.com -SrcUsername contoso\admin -SrcPassword P@ssword -SPOSiteUrl https://contoso.sharepoint.com -SPOUsername admin@Contoso.onmicrosoft.com -SPOPassword P@ssword
	
	.Notes
        	Name: MigrateOnPremTermStoreToSPO.ps1
        	Sources: 
        	Author: Brent Person, Microsoft, brpers@microsoft.com
        	Last Edit: 07/10/2020
#>
