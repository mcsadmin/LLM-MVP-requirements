# Admin User Interface

**Sequence:** 18  
**Source:** MVP Requirements / Admin User Interface #AdminUser  
**ClickUp Page ID:** 8cp80ab-5915  
**Last Updated:** 2025-11-25  
**Tags:** #AdminUser

---

# 1\. Admin User
### 1.
1. WHAT:
    1. Access: tbc
        1. Refer to v1.1/1.2 requirements
        2. Note from previous discussion with Ops: logins should only be available to second-line (i.e. Grace, Dil, Yani, Paul).
    2. Client Users list (organizations table):
        1. For each Client User, display:
            1. Canonical Name (not currently in organizations schema), should be able to sort by this
            2. App Organisation Name (the name they used to register - might be display\_name?)
            3. Account/Organisation Email (email address used to register - presumably email)
            4. Organisation Tier Level (org\_tier\_level), should be able to sort by this
            5. Outstanding tasks? ('yes' or 'no'), should be able to sort by this
                1. 'yes' if Client User has associated tasks in 'Reporting and tasks' page
            6. List searchable by Canonical Name and App Organisation Name
    3. Detailed Client User view:
        1. Basic info:
            1. uuid (id)
            2. Canonical Name
            3. App Organisation Name
            4. Display Name (optional field on Account page - might be display\_name? (although this may also be App Organisation Name))
            5. Address (if only postcode is available, this is fine for MVP, although this is not currently in the schema)
            6. Account/Organisation Email
            7. Contact Email (optional field on Account page - not currently in schema)
            8. Registration Date (presumably created\_at)
            9. Organisation Tier Level
            10. Promis connection status
                1. Not connected
                2. Connected to Xero
                3. Connected to QuickBooks
                4. Xero connection broken
                5. QuickBooks connection broken
        2. 'Delete org' functionality
            1. Various v1.1/1.2 tickets can be used as sources for testing script
        3. Summary of issued and received invoices (count and total amounts from invoices\_final)
        4. View and manage file uploads
            1. Search files
            2. View basic info (files table):
                1. file uuid (id)
                2. file type
                3. file name (original\_file\_name)
                4. upload date (date part of uploaded\_at)
            3. View detailed extracted info (invoices\_staging table?):
                1. tbc - reference [Non-Promis Data Extraction & Pre-Processing](https://hackmd.io/O9Spdn2ET0u5TjSgPasI9Q)
            4. Actions:
                1. View pdf file directly (optional/post-MVP?)
                2. Download pdf file
                3. Delete pdf file
                    1. This should only delete the file itself, not any of the invoices associated with/extracted from it.
            5. Flag/highlight if file has been reported as having incorrect data, direct to 'Reporting and tasks' page
        5. View invoices\_final table filtered by this Client User as creditor or debtor
            1. Table view: entire schema (can refine post-MVP)
            2. Highlight each row with associated critical ETL or de-duplication issues that require action from the 'Reporting and tasks' page
                1. Ensure that these are always displayed at the top of the table, so that they are immediately visible
        6. If Promis connection is active or broken: view 'raw' Promis table filtered by this Client User as creditor
        7. 'Sync now' button to refresh current view
        8. 'Download' button to download current view in .csv format
            1. See ticket [#1096](https://github.com/CredComSoc/cofi-app-llm/issues/1096) for testing script (might need updating)
    4. Debtor organisations list (org\_customers table):
        1. For each debtor organisation, display:
            1. Canonical Name (canonical\_name), should be able to sort by this
            2. Invoice Aliases (invoice\_aliases)
            3. Outstanding tasks? ('yes' or 'no'), should be able to sort by this
                1. 'yes' if debtor organisation has associated tasks in 'Reporting and tasks' page
            4. List searchable by Canonical Name and all Invoice Aliases
    5. Detailed debtor organisation view
        1. Basic info:
            1. uuid (customer\_id)
            2. Canonical Name (canonical\_name)
            3. List of associated Invoice Debtor Organisation Names (invoice aliases)
        2. 'Delete org' functionality
            1. Various v1.1/1.2 tickets can be used as sources for testing script
        3. View invoices\_final table filtered by this debtor organisation as debtor
            1. Table view: entire schema (can refine post-MVP)
            2. 'Sync now' button
            3. 'Download' button to download current view in .csv format
                1. See ticket [#1096](https://github.com/CredComSoc/cofi-app-llm/issues/1096) for testing script (might need updating)
    6. Network (invoices\_final table):
        1. View invoices\_final table (entire schema) with no filtering
        2. View invoices\_final table (entire schema) as Clearing Set
            1. Data:
                1. Four fields from the invoices\_final table:
                    1. An obligation uuid
                        1. Could be final\_id or another value - for review with reference to the final\_invoices schema
                    2. Debtor organisation uuid
                    3. Creditor organisation uuid
                        1. NB that this order is reverse of that used in example file in Telegram chat - confirm final format with Tomaž!
                    4. Amount Due
                        1. Cycles algorithm requires integer values for this: need to convert from £ into pence.
                2. Only rows with [Submission Status values](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-42353422-e770-405f-8ee5-b165aa5c8025) of 'Final Submitted' for both creditor and debtor should be included.
                3. Only rows with a clearing cycle number/identifier corresponding to the current [Clearing Cycle](../../requirements/system-functions/12-clearing-cycle.md) should be included.
        3. 'Sync now' button to refresh current view
        4. 'Download' button to download current view in .csv format
    7. Reporting & tasks
        1. Client Users:
            1. Critical data ingestion issues:
                1. Broken Promis connections
                2. Non-Promis data extraction:
                    1. Obligation types other than invoices
                    2. Invoices are received rather than issued
                        1. Reporting on this might not be strictly necessary for MVP, so long as can confirm that they are being reliably filtered out
                    3. Anything else flagged by the AI?
                3. Client User reports of incorrectly extracted non-Promis data
            2. Critical ETL issues:
                1. More than one unique value of creditor\_name\_raw associated with this Client User in any invoices table
                2. One or more invoices with mandatory fields missing
                3. One or more invoices flagged as 'invalid'
                4. _Multiple unique values of creditor\_name\_raw associated with any single Client User in any invoices table_
                5. One or more invoices with Due Date missing
            3. Critical duplicates issues:
                1. List all instances of the following [scenarios](https://hackmd.io/jcOtMR7gTsGOt-R5_mckPA), alongside associated Client User: 1bi, 1c, 2bi, 2bii1, 2ci, 2cii, 2di, 3bi, 3bii, 3c, 3d, 1z, 2z, 3z
        2. Debtor organisations ID & reconciliation
            1. As per [super-MVP admin user workflows](https://www.figma.com/board/Vs5nknyzzlazVWNiFH8c5f/MVP-Debtor-Org-ID---Reconcilation?node-id=361-1374&t=B66b0Ua6MIPPRvxk-0)
                1. Each workflow to be performed one at a time across all organisations, i.e. do reconciliation/merging for all rows in org\_customers, then do all matching to client users (organizations) for all rows

### 2\. Other background/reference material (optional)
*   Service performance monitoring:
    *   Uptime monitoring
###   

### 10\. Post-MVP notes
*   Tables other than invoices\_final and 'raw' Promis data?
    *   Discussed with [@Abrar Chowdhury](#user_mention#188527999), agreed that no need for staging and core, as tech team have direct access to Supabase for bug fixing
*   Client Users list:
    *   Membership Status
    *   Issued invoices in current cycle? ('yes' or 'no')
        *   'yes' if invoices\_final has issued invoices for this Client User for current cycle
            *   tbc
    *   Received invoices in current cycle? ('yes' or 'no')
        *   'yes' if invoices\_final has received invoices for this Client User for current cycle
            *   tbc
*   Detailed Client User view:
    *   Basic info:
        *   Membership Status
        *   Identity confirmed? (not in current schema)
        *   In catchment area? (not in current schema)
        *   Show 'App Display Name'
        *   Linked with debtor organisation, associated details (not in current schema)
        *   Linked with IDM, associated details (not in current schema)
        *   Most Recent Invoice Data Timestamp (table and field tbc)
            *   See ticket [#1362](https://github.com/CredComSoc/cofi-app-llm/issues/1362) for testing script (might need updating)
            *   Most Recent Sign In Date (not sure which field this is)
        *   Promis connection status: generate report on connect, disconnect, and connection broken history. See detailed syncing status
        1. Generate & download analysis & visualisation
            1. Day 1 analysis & visualisations (specifications tbc)
                *   NB that for MVP agreed with [@Abrar Chowdhury](#user_mention#188527999) to just use raw/unfiltered invoics\_final .csv from Network view, since Mohammed's visualisation Python script can do the filtering by client user itself
    *   Summary of issued and received invoices
        *   Filters by Eligibility, Submission Status, current cycle only?
    *   Invoices:
        *   View archived Promis data (from most recent connection?)
        *   Eligibility Status filters
        *   Submission Status filters
        *   Cycle number filter
        1. Grouped view:
            1. month → debtor/customer → individual invoices
            2. individual invoices view:
                1. Issued or Received
                2. Eligibility Status
                3. Submission Status
                4. Other data from invoices\_final schema tbc
    *   Contacts
        *   tbc (depends on available Promis and non-Promis contacts data)
        *   If 'Download' button included, see ticket [#1367](https://github.com/CredComSoc/cofi-app-llm/issues/1367)
    *   'Delete org' functionality
        *   More sophisticated account deletion - option for us to keep analysing data and inform when results are better
*   Debtor organisations list:
    *   Additional fields:
        *   Potential member? (catchment area, B2B, not already a member)
        *   B2B? (b2b)
*   Detailed debtor organisation view
    *   Summary of received invoices (count and total amounts)
    *   Invoices (invoices\_final table filtered by this debtor organisation as debtor) possibly also includes invoices for which this debtor org is the creditor if they are also linked to a Client User?
    1. Identity confirmed? (not in current schema)
    2. In catchment area? (in\_catchment\_area)
    3. Linked with IDM (confirmed match boolean not in current schema, but could be inferred from presence or absence of idm\_link), associated details?
    4. Linked with Client User (not in current schema), associated details?
*   Network
    *   Reintroduce checkboxes/selection to enable download of custom-filtered .csv
*   Reporting & tasks
    1. Client Users
        1. New registrations in last day/week. Might be better to have something that indicates some time of processing status?
        2. See v1.1/1.2 requirements for full details of possibly desirable/non-critical reports (search for 'report' in documentation)
        3. Review of all Client User 'edit' actions on non-Promis data
            1. Monitoring plus support of any supplementary out-of-app interactions with Client Users (e.g. 'can you confirm the Amount Due?').
        4. [@Abrar Chowdhury](#user_mention#188527999) suggested including a report on removal of invoices based on 'is\_current' in invoices\_core - this will tell us that a new row has arrived in staging, and this is an update on an earlier existing row.
        5. Client User org ID & reconciliation tasks?
            1. (all below tbc once Client User version of org ID & reconciliation workflow finalised):
                1. Identity confirmed = 'false' or 'true (web)'
                2. In catchment area = 'false' or 'not sure'
                3. B2B = 'false' or 'not sure'
                4. Confirmed match in org\_customers = ‘false’ and Other match(es) in org\_customers = ‘close’
                    1. Necessary?
                5. Confirmed match in IDM = ‘false’ and Other match(es) in IDM = ‘close’
        6. View all Contact Us submissions (auth version)? Might be covered by email and/or Odoo ticketing
    *   
*   Edit functionality for Client Users and debtor organisations?
*   Look at client journey for other useful notifications/reports to admin users (in addition to new client users)
*   Add a way for Admin User to know whether initial data sync has finished/how many invoices are still to be loaded
*   Re-instate 'create new Client User' functionality (and add sending an email to new client user after admin user has created their account). Any need for 'create new non-Client User org' functionality?
*   Investigate and consider re-instating ‘Remove Promis Data’ button - appeared in v1.1, purpose and function currently unknown.
*   Ensure that Client Users always have full address
    *   Should be automatic as a result of identity confirmation workflow, but will need to confirm this
*   Different permissions (e.g. edit and view) for different admin users.
*   Analytics of recurring problems, as indicated by Odoo tickets.
*   Clearing cycle management
    *   Set length of [Submission Window](../../requirements/system-functions/12-clearing-cycle.md)
*   Pseudo-client dashboard

---

**Document Metadata:**
- **Created:** 2025-11-14
- **Sequence Number:** 18
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5915
