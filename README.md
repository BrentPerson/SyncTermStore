# SyncTermStore
scripts used to sync your Term Store to SharePoint Online or On-Premises


As far as in what order we should utilize the scripts it will vary but the general idea is this:

1.	Document your Term Store to see what groups are reusing/pinning terms and get an initial Term count from the On-premises term store. 

    a.	The documentation will be done with Validation script ‘DocumentPinnedReusedTerms.ps1’

    b.	Analyze the document and make sure we start syncing the larger groups first like ‘Enterprise Metadata’ as the other term groups will be pinning and reusing terms from these larger groups.

    i.	Or sync the groups that are not listed in the csv outputs as they are all source terms not reused or pinned anywhere else

    c.	Run the Validation Script ‘OnPremSourceTermCount.ps1’   

    d.	We also can’t reuse deprecated terms so we should either remove deprecated terms from the OnPrem Termstore, or Enable those terms and then disable after sync’s have completed.
    
2.	Once we have an idea of where to start we will run the script ‘AllTermSetsAtOnce.ps1’ so we can get as many term sets and terms sync’d to SPO during the first run.

3.	After each Term Group gets sync’d we will need to validate what terms, if any, didn’t get sync’d by first performing a Term Count on the SharePoint Online Term store and compare the out put with the output from the OnPrem count from step 1
    
    a.	This will be done using the validation script ‘SPOSourceTermCount.ps1’
    
4.	Once we have the OnPrem vs Online term count we will need to see what terms didn’t get created and investigate why (term is a pinned term but source doesn’t exist yet)
    
    a.	For this we will use the Validation Script ‘FindMissingTermsInTermSet.ps1’
    
5.	When we find what wasn’t sync’d the first run around we can use either of the next two sync scripts to do specific termset/term syncs
    
    a.	If the whole term set needs to be sync’d again in a term group but the whole term group does not need to be sync’d again we can use sync script ‘SyncSpecificTermSet.ps1’
    
    b.	If a specific root term and it’s child terms need to be sync’d but the whole term set does not need to be sync’d we can use sync script ‘SyncSpecificRootTerm.ps1’
    
6.	After each sync run the ‘SPOSourceTermCount.ps1’ script again to get an updated term count.
