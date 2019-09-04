Prerequisites:
	• Account running the scripts must be term store administrator in both source and destination Term stores
	• In the three main sync scripts AllTermSetsAtOnce.PS1, SyncSpecificRootTerm.PS1, SyncSpecificTermSet.PS1 we are dot sourcing the helper scripts so they all must be in the same directory


Secure Store Configuration Process:
	• Create Secure Store Service Application
	• Create Two Secure Store Apps for your Source and Destination sites and then set credentials. 
		○ Make note of the Target Application ID as we'll use it in the sync scripts
			§ Target Application Type: Group
			§ Field Name: User Name
				□ Field Type: User Name
			§ Field Name: Password
				□ Field Type: Password


Main Script Changes:

AllTermSetsAtOnce.PS1, SyncSpecificRootTerm.PS1, SyncSpecificTermSet.PS1
	• Set ALL Global Variables to match your environment
	• Lines 31, 32 make sure the UPN suffix with the '@' and Domain with the '\' are correct
		○ In order to migrate Group Managers, Group Contributors, and term set stake holders the account UPN must exist in Azure Active Directory
	• Lines 36-38 make sure the assembly path is correct for the 'Add-Type'

 CSOMHelper.PS1
	• Lines 14,15 make sure the assembly path is correct for the 'Add-Type'

PSJobHelper.PS1
	• Lines 14,15 make sure the assembly path is correct for the 'Add-Type'

SecureStoreServiceHelper.PS1
	• Lines 17,18 make sure the assembly path is correct for the 'Add-Type'


Validation Script Changes:

DocumentPinnedReusedterms.PS1
Lines 13-15 set the variables to fit your environment
Lines 17-19 make sure the assembly path is correct for the 'Add-Type

FindMissingTermsInTermSet.PS1
Lines 18-20 make sure the assembly path is correct for the 'Add-Type
Line 23 - 35 Change the variables to fit your environment
Uncomment lines 111 and 121 to find the missing terms in Destination term store
Uncomment lines 126 and 136 to find missing terms in Source term store

OnPremSourceTermCount.PS1
Lines 19-23 Change the variables to fit your environment
Lines 25-27 make sure the assembly path is correct for the 'Add-Type

SPOSourceTermCount.PS1
Lines 19-22 Change the variables to fit your environment
Lines 24-26 make sure the assembly path is correct for the 'Add-Type



As far as in what order we should utilize the scripts it will vary but the general idea is this
 
	1. Document your Term Store to see what groups are reusing/pinning terms and get an initial Term count from the On-premises term store.
			a. The documentation will be done with Validation script ‘DocumentPinnedReusedTerms.ps1’
			b. Analyze the document and make sure we start syncing the larger groups first like ‘Enterprise Metadata’ as the other term groups will be pinning and reusing terms from these larger groups.
		i. Or sync the groups that are not listed in the csv outputs as they are all source terms not reused or pinned anywhere else
			a. Run the Validation Script ‘OnPremSourceTermCount.ps1’
			b. We also can’t reuse deprecated terms so we should either remove deprecated terms from the OnPrem Termstore, or Enable those terms and then disable after sync’s have completed.
	2. Once we have an idea of where to start we will run the script ‘AllTermSetsAtOnce.ps1’ so we can get as many term sets and terms sync’d to SPO during the first run.
	3. After each Term Group gets sync’d we will need to validate what terms, if any, didn’t get sync’d by first performing a Term Count on the SharePoint Online Term store and compare the output with the output from the OnPrem count from step 1
			a. This will be done using the validation script ‘SPOSourceTermCount.ps1’
	4. Once we have the OnPrem vs Online term count we will need to see what terms didn’t get created and investigate why (term is a pinned term but source doesn’t exist yet)
			a. For this we will use the Validation Script ‘FindMissingTermsInTermSet.ps1’
	5. When we find what wasn’t sync’d the first run around we can use either of the next two sync scripts to do specific termset/term syncs
			a. If the whole term set needs to be sync’d again in a term group but the whole term group does not need to be sync’d again we can use sync script ‘SyncSpecificTermSet.ps1’
			b. If a specific root term and it’s child terms need to be sync’d but the whole term set does not need to be sync’d we can use sync script ‘SyncSpecificRootTerm.ps1’
	6. After each sync run the ‘SPOSourceTermCount.ps1’ script again to get an updated term count.
