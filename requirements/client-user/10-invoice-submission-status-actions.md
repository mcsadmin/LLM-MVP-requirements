# Invoice Submission Status Actions

**Sequence:** 10  
**Source:** MVP Requirements / Invoice Submission Status Actions #ClientUser  
**ClickUp Page ID:** 8cp80ab-5775  
**Last Updated:** 2025-12-07  
**Tags:** #ClientUser #Invoices

---

# 1\. Submission Status & Associated Actions
### 1\. Submission Status determines whether or not an invoice will be included in the current clearing cycle, and so needs to be actionable.
1. WHY: Deliberate submission of invoices is a legal requirement for them to be included in clearing. Client Users must therefore be able to understand the Submission Status of their own eligible issued and received invoices, perform associated desirable actions, and understand their implications.
2. WHAT:
    1. Submission Status is managed via two fields: Submission Status (creditor) and Submission Status (debtor)
    2. Submission Status (creditor) values:
        1. 'Submission not Possible'
            1. Description: this invoice cannot be submitted because either:
                1. It has an [Eligibility Status](../../requirements/client-user/08-invoice-eligibility-status-actions.md) other than 'eligible' (i.e. 'potentially eligible' or 'ineligible'), or
                2. It is a Promis invoice for which the Total Due has been revised upwards at any point after the invoice was first collected
                    1. Necessary because Xero (and possibly other platforms) allows creditors to amend data (including Total Due) after the invoice has been approved, enabling deliberate corruption of clearing results
                3. It is a non-Promis/file upload invoice which has been [reported as having incorrectly extracted data](../../requirements/client-user/11-non-promis-issued-invoice-edit-report-actions.md?block=block-2efdb50f-3823-4e90-a551-ed010dc9621b)
            2. [Visibility](../../requirements/client-user/09-invoices-visibility.md?block=block-f83ffe3c-ec75-427d-8a3a-83ab15e0e945) to creditor Client user: not visible
            3. Actions available to creditor Client User: none
            4. Visibility to debtor Client user: not visible
            5. Actions available to debtor Client User: none
        2. 'Ready for Final Submission'
            1. Description: due to 'opt-out' design, this is the default value of Submission Status (creditor) for invoices with an Eligibility Status of 'eligible'
            2. Visibility to creditor Client User: visible within their 'clearing set'
            3. Actions available to creditor Client User: 'exclude'
                1. Changes Submission Status (creditor) to 'Excluded (manual)'
            4. Visibility to debtor Client User: visible within their 'clearing set'
            5. Actions available to debtor Client User: 'exclude'
                1. Changes Submission Status (debtor) to 'Excluded (manual)'
        3. 'Excluded (manual/auto)'
            1. Description:
                1. Manually excluded by creditor Client User from their 'clearing set' ('manual' variant), or
                2. Automatically excluded ('auto' variant) because:
                    1. The Due Date is 'adverse' (i.e. the invoice Due Date is on or after the present date, but sooner than the end of the Submission Window of the [current Cycle](../../requirements/system-functions/12-clearing-cycle.md) (i.e. the time of the next clearing process), and we assume that the creditor Client User would rather just be paid on time)
                    2. The collected\_on or updated\_at timestamps are within the Submission Window of the current Clearing Cycle
                    3. The debtor Client User registered on the platform (changing the Eligibility Status of the invoice to 'eligible') during the Submission Window of the current Clearing Cycle
            2. Visibility to creditor Client User: visible within their 'excluded' list
            3. Actions available to creditor Client User:
                1. During Data Acceptance/Review Window: 'undo' (temporary option after manual exclusion only); 'restore' (standing option): changes Submission Status (creditor) to 'Ready for Final Submission'
                    1. If Due Date is 'adverse', warn creditor Client User that this may encourage their debtor to pay late.
                2. During Submission Window: 'undo' (temporary option after manual exclusion only): changes Submission Status (creditor) back to 'Final Submitted'
                    1. If Due Date is 'adverse', warn creditor Client User that this may encourage their debtor to pay late.
            4. Visibility to debtor Client User: no longer visible (within either 'clearing set' or 'excluded' list)
                1. Needs to disappear almost immediately - if not possible, may need to introduce 'Excluded (by both)' status, or find some other way to ensure that a lag does not introduce bugs/errors.
            5. Actions available to debtor Client Users: none.
        4. 'Final Submitted'
            1. Description: the creditor of this invoice has performed the final submission confirmations for their 'clearing set', which included this invoice (i.e. this invoice had a Submission Status (creditor) of 'Ready for Final Submission')
                1. 'Final submission confirmation' action is only available during the Submission Window of the current Cycle
            2. Visibility to creditor Client User: visible within their 'clearing set'
            3. Actions available to creditor Client User: 'exclude'
                1. As with exclusion from 'Ready for Final Submission' state, this changes the Submission Status (creditor) value to 'Excluded (manual)'
            4. Visibility to debtor Client User: visible within their 'clearing set'
            5. Actions available to debtor Client User: 'exclude'
                1. As with exclusion from 'Ready for Final Submission' state, this changes the Submission Status (debtor) value to 'Excluded (manual)'
    3. Submission Status (debtor) values:
        1. 'Submission not Possible'
            1. Description: this invoice cannot be submitted because either:
                1. It has an [Eligibility Status](../../requirements/client-user/08-invoice-eligibility-status-actions.md) other than 'eligible' (i.e. 'potentially eligible' or 'ineligible'), or
                2. It is a Promis invoice for which the Total Due has been revised upwards at any point after the invoice was first collected
                    1. Necessary because Xero (and possibly other platforms) allows creditors to amend data (including Total Due) after the invoice has been approved, enabling deliberate corruption of clearing results
            2. [Visibility](../../requirements/client-user/09-invoices-visibility.md?block=block-f83ffe3c-ec75-427d-8a3a-83ab15e0e945) to creditor Client user: not visible
            3. Actions available to creditor Client User: none
            4. Visibility to debtor Client user: not visible
            5. Actions available to debtor Client User: none
        2. 'Ready for Final Submission'
            1. Description: due to 'opt-out' design, this is the default value of Submission Status (debtor) for invoices with an Eligibility Status of 'eligible'
            2. Visibility to creditor Client User: visible within their 'clearing set'
            3. Actions available to creditor Client User: 'exclude'
                1. Changes Submission Status (creditor) to 'Excluded (manual)'
            4. Visibility to debtor Client User: visible within their 'clearing set'
            5. Actions available to debtor Client User: 'exclude'
                1. Changes Submission Status (debtor) to 'Excluded (manual)'
        3. 'Excluded (manual)'
            1. Description: manually excluded by debtor Client User from their 'clearing set'
            2. Visibility to creditor Client User: no longer visible (within either 'clearing set' or 'excluded' list)
                1. Needs to disappear almost immediately - if not possible, may need to introduce 'Excluded (by both)' status, or find some other way to ensure that a lag does not introduce bugs/errors.
            3. Actions available to creditor Client User: none.
            4. Visibility to debtor Client User: visible within their 'excluded' list
            5. Actions available to debtor Client Users:
                1. During Data Acceptance/Review Window: 'undo' (temporary option after manual exclusion only); 'restore' (standing option): changes Submission Status (debtor) to 'Ready for Final Submission'
                    1. If Due Date is 'adverse', warn debtor Client User that this may send a signal that intending to pay their creditor late.
                2. During Submission Window: 'undo' (temporary option after manual exclusion only): changes Submission Status (debtor) back to 'Final Submitted'
                    1. If Due Date is 'adverse', warn debtor Client User that this may send a signal that intending to pay their creditor late.
        4. 'Final Submitted'
            1. Description: the debtor of this invoice has performed the final submission confirmations for their 'clearing set', which includes this invoice (i.e. this invoice had a Submission Status (debtor) of 'Ready for Final Submission')
                1. 'Final submission confirmation' action is only available during the Submission Window
            2. Visibility to creditor Client User: visible within their 'clearing set'
            3. Actions available to creditor Client User: 'exclude'
                1. As with exclusion from 'Ready for Final Submission' state, this changes the Submission Status (creditor) value to 'Excluded (manual)'
            4. Visibility to debtor Client User: visible within their 'clearing set'
            5. Actions available to debtor Client User: 'exclude'
                1. As with exclusion from 'Ready for Final Submission' state, this changes the Submission Status (debtor) value to 'Excluded (manual)'

### 9\. Additional testing notes
*   If a creditor excludes an invoice, it should disappear for the debtor. To test this properly we'll have to set up multiple client user accounts and 'connect' them via invoices (which is something we'll want to do in any case in order to simulate wider 'network' behaviour/affordances).
*   Timestamp and auto-exclusion note: if an invoice is created during the Submission Window, then it should be auto-excluded as per the requirements. However, to implement this, only need to look at updated\_at timestamp (rather than created\_at), since created\_at will be identical to updated\_at for new invoices.
*   

### 10\. Post-MVP notes
1. Better handling of upwards revision of Promis invoice Total Due field by creditors, or better/more granular handling of updated\_at, e.g. only rejecting if field that has changed is amount\_due or debtor\_name, depending on which version of requirements was ultimately implemented
2. Better handling of exclusion due to editing? Since editing can only be done by creditors, then it should only be possible to revise amounts due downwards (via adding payments)?
3. Include area where invoices excluded by counterparty are visible to Client User (particularly important for when they were auto-excluded due to debtor joining during Submission Window, as this might have been by invitation of the creditor), alongside 'prompt to undo exclusion' functionality.
    1. If this is implemented, a new Submission Status - 'Excluded (by both)' - may become relevant, but not necessary for MVP since invoices should immediately disappear for counterparty after being excluded by the other.
4. Include indication to Client User that their counterparty has performed final submission action, e.g. if status is 'Final Submitted (creditor)', then include indication to debtor that their creditor for this invoice has performed final submission on it, and if status is 'Final Submitted (both)', then include indication to debtor that their creditor for this invoice has performed final submission on it, and vice versa.
5. Option to remember/save choices/preferences with respect to counterparties:
    1. For each customer?
        1. Invoices for trading partners which have standing orders or direct debits associated with them?
    2. UI design: include controls (trading partner specific and global) on Account/Profile page?
6. More sophisticated handling of invoices with 'adverse' Due Dates. Several possibilities:
    1. Dedicated status(es) and associated visibility so that creditor and debtor can coordinate
    2. Remove auto-exclude-by-creditor functionality - will people even notice invoices with adverse Due Dates in their clearing sets, or draw the inferences around signalling about late payment that we anticipate they will? Removing this functionality might improve results due to clearing of invoices that were always going to be paid late/after the clearing cycle. Subject for user testing.

---

**Document Metadata:**
- **Created:** 2025-09-07
- **Sequence Number:** 10
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5775
