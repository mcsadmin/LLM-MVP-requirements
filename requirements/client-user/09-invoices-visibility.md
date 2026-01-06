# Invoices Visibility

**Sequence:** 09  
**Source:** MVP Requirements / Invoices Visibility #ClientUser  
**ClickUp Page ID:** 8cp80ab-4495  
**Last Updated:** 2025-11-24  
**Tags:** #ClientUser #Invoices

---

# 1\. Visibility of Client User's Issued Invoices
### 1\. Based on the [Aggregated Invoice Entries Table](../../requirements/system-functions/07-unified-invoice-entries-tables-etl.md?block=block-0c64c21a-72b4-46e1-a564-fe637842b8ba), present the Client User's relevant issued invoice data to them
1. WHY: Client Users should be able to see their relevant issued invoices, i.e. the ones that they have imported into Local Loop, and be able to verify that they accurately represent the current state of the invoices for which they expect to be paid by other Local Loop members.
2. WHAT:
    1. The Client User should be able to clearly see their own issued invoice data.
    2. Only invoices with an [Eligibility Status](../../requirements/client-user/08-invoice-eligibility-status-actions.md) of 'eligible' should be displayed in the 'submit for clearing' functionality.
        1. Required invoice data fields:
            1. Customer
                1. The Invoice Debtor Organisation Name that they use to refer to their customer on their invoices
            2. Amount Due (£)
            3. Due Date
            4. Show additional fields (Total Amount (£), Description, Invoice Number) via user actions, e.g. clicking on tooltips.
        2. Default ordering of invoices is by Due Date in reverse chronological order.
        3. It should be possible to sort invoices by Due Date, or by counterparty name, and by Amount Due.
    3. Invoices with 'potentially eligible' status should be used to populate a list of debtors who could be invited to Local Loop (this should be clearly separated from the 'submit for clearing' functionality).
    4. Invoices with 'ineligible' status should not be displayed at all.

# 2\. Visibility of Client User's Received Invoices
### 1\. Based on the [Aggregated Invoice Entries Table](../../requirements/system-functions/07-unified-invoice-entries-tables-etl.md?block=block-0c64c21a-72b4-46e1-a564-fe637842b8ba), present the Client User's relevant received invoices data to them
1. WHY: Client Users should be able to see their relevant received invoices, i.e. invoices that other Client Users have shared with Local Loop and which reference them as the debtor, and be able to verify that they accurately represent the current state of the invoices they expect to pay to other Local Loop members.
2. WHAT:
    1. The Client User should be able to clearly see data from invoices for which other Client Users have named them as the debtor.
    2. Only invoices with an [Eligibility Status](../../requirements/client-user/08-invoice-eligibility-status-actions.md) of 'eligible' should be displayed in the 'submit for clearing' functionality.
        1. Required invoice data fields:
            1. Supplier
                1. The Display Name of the Client User who imported the invoice
                    1. If this has not been set in the Account/Profile page, then default to the App Organisation Name.
            2. Amount Due (£)
            3. Due Date
            4. Show additional fields (Total Amount (£), Description, Invoice Number) via user actions, e.g. clicking on tooltips.
        2. Default ordering of invoices is by Due Date in reverse chronological order.
        3. It should be possible to sort invoices by Due Date, or by counterparty name, and by Amount Due.
    3. Invoices with 'ineligible' status should not be displayed at all.
###

---

**Document Metadata:**
- **Created:** 2025-06-25
- **Sequence Number:** 09
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-4495
