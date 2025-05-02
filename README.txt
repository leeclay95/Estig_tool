##The excel spreadsheet is CASE SENSITIVE.

The following columns are included in the excel sheet

#Vuln ID	ExpectedStatus	ValidTrueStatus	ValidTrueComment AnswerKey Name

You can use AnswerKey Name if you have particular hosts where you want specific comments and statuses to be applied.
I.E you can insert the Hostname of the workstation that a specific v-key needs its status changed with a particular comment.

Vuln ID is the V-Key number I.E. V-221594 #the V is capital

ExpectedStatus is the status found during the original scan. The following are expected statuses
# "Not_Reviewed", "Open", "NotAFinding", and "Not_Applicable" # Case sensitive

ValidTrueStatus is what the new status should be #Reference the statuses above

ValidTrueComment is what comments you have to say about the STIG #Not case sensitive

The tabs represent each individual stig by its short name listed in Evaluate-STIG. If the STIG you are looking for is not present, run evaluate stig with the -ListSupportedProducts switch to find the short name and make a new tab for it.

This excel sheet will be processed by a python script to generate anwser files for STIG automation.

####ENSURE TO CLOSE WORKBOOK AFTER CHANGES HAVE BEEN APPLIED####
##THE PYTHON PROGRAM also allows mass answering of Manual STIGs with a comment that will apply to all of them. If this is a more feasible option please let me know###

#Created by Lee Clayton##

