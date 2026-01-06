# Non-Promis Issued Invoice Edit & Report Actions

**Sequence:** 11  
**Source:** MVP Requirements / Non-Promis Issued Invoice Edit & Report Actions #ClientUser  
**ClickUp Page ID:** 8cp80ab-5735  
**Last Updated:** 2025-11-24  
**Tags:** #ClientUser #PromisIntegration #Invoices

---

# 1\. Issued Invoice Edit & Report Actions
### 1\. The creditor Client User may need to amend the Amount Due and/or Due Date associated with [file upload](../../requirements/client-user/01-non-promis-file-upload.md) (non-Promis) invoices
1. WHY:
    1. There are a range of events which may mean that the Amount Due and/or the Due Date need to be amended by the creditor Client User before an invoice should be included in a Clearing Cycle, and (unlike with Promis data) we will not automatically know about them:
        1. An expected payment (tracked via data extracted from invoice) has not been made, increasing the Amount Due
        2. An unexpected payment has been received, reducing the Amount Due
        3. A credit note has been associated with the invoice, reducing the Amount Due
        4. A debit note has been associated with the invoice, reducing the Amount Due
        5. Agreement to alter the payment terms, changing the Due Date
2. WHAT:
    1. The Client User who is the creditor of an invoice originating with non-Promis/[uploaded files](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-55dabc47-7af4-4e43-9d81-4ff1360bb68c) can edit the Amount Due:
        1. A reason for the change must be given:
            1. 'Expected (partial) payment not received'
            2. '(Partial) payment received'
            3. 'Credit note issued'
                1. Require a credit note number
            4. 'Debit note received'
                1. Require a debit note number (with a note to explain that this will need to be provided by the debtor)
        2. Constraints on changes to Amount Due:
            1. All reasons: Amount Due cannot be more than Total Amount
            2. Reason 1: Amount Due can only be revised upwards
            3. Reasons 2-4: Amount Due can only be revised downwards
    2. The Client User who is the creditor of an invoice originating with (non-Promis) [uploaded files](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-55dabc47-7af4-4e43-9d81-4ff1360bb68c) can edit the Due Date:
        1. A reason for the change must be given:
            1. 'Giving debtor more time to pay'
            2. 'Agreed with debtor that they will pay sooner'
        2. Constraints on changes to Due Date:
            1. Reason 1: Due Date can only be moved further into the future from the existing Due Date; Due Date cannot be moved to more than a year into the future
            2. Reason 2: Due Date can only be moved closer to the present date than the existing Due Date; Due Date cannot be moved before present date
                1. This reason is disabled if the Due Date is before the present date
        3. If the new Due Date is 'adverse' (i.e. sooner than the date of the next clearing cycle), the Submission Status (creditor) should be set to 'Excluded (auto)'.
    3. Any confirmed 'edit' action should modify the updated\_at field accordingly.
        1. As well as general traceability, this ensures that the invoice is auto-excluded if the edit is made during the Submission Window, as per Submission Status requirements.
### 2\. The creditor Client User may need to report [file upload](../../requirements/client-user/01-non-promis-file-upload.md) (non-Promis) invoices because one or more data fields have been incorrectly [extracted by AI](../../requirements/system-functions/04-ai-data-extraction-from-non-promis-files.md)
1. WHY: AI data extraction is not 100% reliable, and so we need to enable Client Users to report incorrect data and ensure that the associated invoices are not included in the upcoming clearing cycle
2. WHAT:
    1. The Client User who is the creditor of an invoice originating with non-Promis/[uploaded files](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-55dabc47-7af4-4e43-9d81-4ff1360bb68c) can report incorrectly extracted data:
        1. The affected field(s) must be selected:
            1. Invoice Debtor Organisation Name
            2. Amount Due
            3. Total Amount
            4. Invoice Number
            5. Issue Date
            6. Due Date
        2. The 'confirm' action should simultaneously remove the possibility of the invoice being submitted (by changing its [Submission Status](../../requirements/client-user/10-invoice-submission-status-actions.md) (creditor) to 'Submission not Possible'), and prompt the Client User to re-upload the file that it originated from.

### 10\. Post-MVP notes
1. Editing:
    1. Editing of fields other than Amount Due and Due Date?
    2. For Promis data, include a tooltip/advice to make any changes to Amount Due or Due Date directly in accounting platform.
    3. Review whether always safe for editing Amount Due to not affect Submission Status (noting that inclusion of sanity checks should make this safer), particularly for reason 1 ('Expected (partial) payment not received') whereby Amount Due is increased.
    4. If the new Due Date is not 'adverse' (whereas the original one was), and the Submission Status (creditor) is 'Excluded (auto)', then set the Submission Status (creditor) to 'Ready for Final Submission' (NB: need to ensure that this does not over-ride any other auto-exclusion logic, e.g. auto-exclusion due to the update being made during the Submission Window).
    5. What happens if AI extraction overestimates amount due and user tries to edit rather than report?
        1. Add 'other' reason to list?
2. Reporting:
    1. Although duplicate removal can handle duplicates of invoices with different values for Amount Due etc, in some scenarios (versions are <24 hours apart) this results in front office contacting Client User to confirm. Review this and ensure that not unduly asking Client User for info, perhaps by adding a flag to duplicates that captures when they have arisen because the Client User has reported incorrect data, and then followed the prompt to re-upload.
    2. Consider how to enable Client User to safely amend data for incorrectly extracted fields such that these invoices can be included in clearing without need to re-upload (reason for excluding/quarantining in MVP is to avoid complications arising from dishonest claims that extraction is incorrect).
3. Draft of deletion requirements (originally part of MVP):
    1. WHY:
        1. Although a Client User can also choose to exclude an invoice from clearing, this may not (depending on the design) permanently remove it from visibility in the interface. There is therefore a need for a distinct 'delete' action.
        2. Could instead remove it from the interface after it has been in 'excluded' state for a given time?
    2. WHAT:
        1. Client User can delete invoice entries originating with (non-Promis) [uploaded files](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-55dabc47-7af4-4e43-9d81-4ff1360bb68c)
            1. This action should either require confirmation, or be temporarily reversible (e.g. via an 'undo' button)
                1. UI/UX design-dependent
            2. Deleted invoice entries should be removed from all relevant [invoice entry tables](../../requirements/system-functions/07-unified-invoice-entries-tables-etl.md)
            3. Deleted invoice entries should be permanently hidden from the Client User's view
            4. This action should not delete the files themselves
            5. Deletion should be prompted if Due Date is a long time in the past? Instead of being overdue, these might have been paid and the Client User has not understood that only unpaid invoices should be shared and/or may not have reliably selected only unpaid invoices.

---

**Document Metadata:**
- **Created:** 2025-08-31
- **Sequence Number:** 11
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5735
