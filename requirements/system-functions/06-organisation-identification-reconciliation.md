# Organisation Identification & Reconciliation

**Sequence:** 06  
**Source:** MVP Requirements / Organisation Identification & Reconciliation #SystemFunction  
**ClickUp Page ID:** 8cp80ab-6175  
**Last Updated:** 2025-11-26  
**Tags:** #SystemFunction

---

# 1\. Organisation Identification & Reconciliation

1. WHAT:
    1. [Super-MVP workflow for debtor organisations](about:blank)
    2. Client User variant:
        1. Realised that organizations table has very different schema to org\_customers - need to discuss with [@Abrar Chowdhury](#user_mention#188527999) asap.
            1. Discussed and agreed that would add to organizations schema on an as-needed basis, starting with Admin User requirements.

### 9\. Other testing notes
*   Data sources:
    *   Pilot & v1.1/1.2 orgs
    *   LCR councils' suppliers
*   Notes:
    *   Some instances observed for Blaze Media where they had used multiple Invoice Debtor Organisation Names for what appear to be the same entities (e.g. 'Gala PR' and 'Alex Sutton PR'). Although not immediately obvious that these were related, they were flagged as duplicates by Grace & Mohammed. After some discussion, realised that the best thing to do would be to flag/capture in the Debtors Report, and ask Client User how best to handle (they might have a good reason, e.g. VAT, for having multiple contacts/names for the same entity). Will also need some kind of merging rules.
*   Send results of early testing to Geoff

**Board clean-up notes**
*   Tickets that can be closed as obsolete:
    *   986; 825

### 10\. Post-MVP notes
*   Fallback process for periodic syncronisation - in Yani's experience triggers have a relatively high failure rate, so should always have back-ups.
*   Combining org\_customers and organizations into single table of LLM-platform originating orgs?
*   Removing client users from organizations\_public
*   Renaming tables to be more semantic
*   Debtors
    *   Review v1 workflow to see if any possible improvements to v2 that weren't included
    *   Client user search during initial automated workflow
    *   Building out entire workflow/scenarios
    *   Re-naming organisation tables, other rework
    *   Introduce staging table for debtor organisations?
    *   Bring organizations table/client users search into initial workflow in order to do as much of this as possible automatically. Wouldn't be necessary if have a combined version of org\_customers and organizations (which would have other advantages)
    *   Performing a postcode/catchment area check before searching in org\_customers or IDM?
    *   B2B determination process still needs to be defined. Anything other profiling we can do that makes it likely that invitations (from us or Client Users via the app) will have a high success rate?
        *   NB that might need to update Eligibility Status assignment logic at ETL stage if a 'not sure' value is introduced for this field - see ETL documentation.
    *   Population of org\_customers table using existing data?
    *   Better use of close matches (from searches)/false positives
    *   Periodic automated checks/clean-ups of org\_customers database to catch any that were not successfully found and matched to previous entries, and then merge/consolidate them - minimise need for manual review.
    *   Automatic updates to latest IDM data
    *   Promis capacity
    *   Open Banking as another data source
    *   CRM as another data source. Also Endole platform?
    *   Sometimes can work out who a business' accountants are by looking at upload accounts documents on CH. Larger firms may be big enough to be audited and can be looked up on [auditregister.org.uk](http://auditregister.org.uk/) (e.g. found Penketh Holdings). NB also that Alexander Myerson are audit accountants, and might intro us to the auditors of Penketh
    *   Notes from IDM 30th Oct:
        *   Use banking info from invoices
        *   Reporting on subsidiaries
            *   Reconciliation/merging affected by whether or not companies are subsidiaries?
        *   QA on collected location data: sometimes obviously wrong
        *   Standardisation of (Promis) contacts data, regular expression check on postcodes at point of collection, always pay attention to last 3 bits of postcode
        *   Use pre-@ part of email address, as this is sometimes useful (e.g. [a.mutualcreditservices@gmail.com](mailto:a.mutualcreditservices@gmail.com)), particularly for identifying sole traders. Can also download names lists
        *   Scrape Facebook as well as LinkedIn
        *   Avoid web scraping if at all possible - slow and painful, increasingly regulated
        *   Create large synthetic datasets to test even small-scale processes
        *   Avoid ending up with any self-referential checks
        *   Postcode → name → exact address/geometry in new IDM datasets (geoposition rather than postcode)
        *   Local authority boundaries: ONS Geoportal for geoshapes, can already check boundaries using IDM dataset. GSS codes
*   New workflow/decision tree for Client Users on registration:
    *   Variant of debtor workflow. [@Paul Maker](#user_mention#100554191) noted that might be able to have a centralised service for identification, and that this can be factored into post-MVP iterations.
    *   Is a separate ticket needed to collect data on the Client User, as well as their Contacts/Customers?
*   Org identity maintenance:
    *   Profile/Account management functionality:
        *   What happens if a Client User deletes their account?
            *   Need to specify how to update 'Membership Status' from 'Member (current)' to 'Member (former)'
                *   Update: note that Membership Status is now a boolean ('true' or 'false'), and that another way to track 'current' or 'former' status needs to be implemented
            *   NB that this should probably be tracked in the CRM, rather than the app - in order to establish Eligibility Status, all the app needs to do is know whether or not an organisation is currently a Member. Any other things that would be best in the CRM?
        *   What happens if Client User changes App Org Name (or another editable name)?
    *   What happens when a Xero/QuickBooks user updates their own name?
        *   Depends on whether coupling functionality from v1.1/1.2 is implemented for MVP - need to confirm with Yani
    *   What happens when a non-Promis user updates their own name?
        *   Might appear as mismatch between Invoice Creditor Org Name and Creditor Canonical Org Name - feed into 'received invoices' updates
    *   Checking Companies House for registered name changes?
    *   What happens when a Xero/QuickBooks user updates a contact name?
        *   Presumably previously-issued invoices don't change, but invoices issued from then on will use the new name.
        *   We need to ensure we are tracking Contact name changes and keeping in sync with our org identity and reconciliation management.
        *   We're already getting updates on Contacts every 5 minutes, so in principle can do this near-continuously.
        *   Effect on duplicate analysis etc?
        *   QB: if user updates Company Name, then (for v1.1): newly-created invoices are captured with new Company Name, but previously-captured invoices do not update
*   Keep Tomaž up to date on org and invoice matching, avoid reproducing Informal's work

---

**Document Metadata:**
- **Created:** 2025-11-24
- **Sequence Number:** 06
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-6175
