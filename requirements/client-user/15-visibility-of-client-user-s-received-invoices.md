# Visibility of Client User's Received Invoices

**Sequence:** 15  
**Source:** MVP Requirements / Visibility of Client User's Received Invoices #ClientUser  
**ClickUp Page ID:** 8cp80ab-5755  
**Last Updated:** 2025-09-07  
**Tags:** #ClientUser #Invoices

---

# 1\. Visibility of Client User's Received Invoices
### 1\. Based on the [Aggregated Invoice Entries Table](../../requirements/system-functions/07-unified-invoice-entries-tables-etl.md?block=block-0c64c21a-72b4-46e1-a564-fe637842b8ba), present the Client User's received invoices data to them as a 'single source of truth'
1. WHY: Client Users should have a single location to see their received invoices, i.e. invoices that other Client Users have shared with Local Loop and which reference them as the debtor, and be able to verify that they accurately represent the current state of the invoices they expect to pay.
2. WHAT:
    1. The Client User should only be able to see data from invoices for which other Client Users have named them as the debtor.
    2. Only invoices with an [Eligibility Status](../../requirements/client-user/08-invoice-eligibility-status-actions.md) of 'eligible' should be displayed.
    3. Required invoice data fields:
        1. Supplier
            1. The Display Name of the Client User who imported the invoice
                1. If this has not been set in the Account/Profile page, then default to the App Organisation Name.
        2. Total Amount (£)
        3. Amount Due (£)
        4. Due Date
        5. It may be desirable to show additional fields (e.g. Description, Invoice Number) via user actions, e.g. clicking on tooltips.
    4. Invoice data should be displayed in reverse chronological order (by Issue Date or Due Date?).
### 2\. Target sprint (Yani & Paul)

### 3\. Increment to existing implementation
#### Existing implementation
*   None.
#### Increment the BRD is intended to deliver
### 4\. Acceptance criteria

### 5\. Candidate solution material
*   The origin for the data could be either the tables that separately contain each Client User's data after it has been [cleaned and de-duplicated](../../requirements/system-functions/07-unified-invoice-entries-tables-etl.md?block=block-a82588df-bb8a-4e8a-9c6a-2259913c450a), or it could be the table containing invoices [aggregated across all Client Users](../../requirements/system-functions/07-unified-invoice-entries-tables-etl.md?block=block-0c64c21a-72b4-46e1-a564-fe637842b8ba), with a filter applied such that the Client User can only see data that names them as the debtor.
    *   This choice will depend on whether the app-based version of the invoice data processing workflow maintains separate tables for each Client User, security considerations etc.
### 6\. Other background/reference material
*   Note that the requirements may be altered in light of ongoing UI/UX work.
    *   Might be integrated with the [Client User's view of their own (issued) invoice data](../../requirements/client-user/09-invoices-visibility.md)? Previous designs have had separate tabs for 'Issued' and 'Received' invoices, suggesting not integrated.
### 7\. Ready to create ClickUp task? (Requirement Owner \[Tom/Dil\])

### 8\. Linked ClickUp task ID (Jimmy)

### 9\. Test scenarios
#### Cases
#### Regression testing (if increment)

---

**Document Metadata:**
- **Created:** 2025-08-31
- **Sequence Number:** 15
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5755
