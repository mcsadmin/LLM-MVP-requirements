# Promis Data Collection #SystemFunction

**Source:** MVP Requirements / Promis Data Collection #SystemFunction  
**ClickUp Page ID:** 8cp80ab-4435  
**Last Updated:** 2025-01-03  
**Tags:** #SystemFunction #PromisIntegration #DataCollection #Xero #QuickBooks

---

## 1. Connect, Disconnect, Reconnect

### 1. Integrations should support easy connect, disconnect and reconnect client user actions.

1. **WHY:** Invoice data is the basis for service delivery.
2. **WHAT:**
    1. **Xero:**
        1. Client user interactions: as per [v1.1 requirements](https://hackmd.io/x7b95YKQQs2ApC9PGFHVSQ?both) 4.1.1, 4.1.2, 4.1.3, 4.1.7, 4.2.1, 4.2.2, 4.3.2 & 4.3.3.
            1. 4.1.3 may not have been included in MVP - need to confirm with Yani.
        2. Xero app launcher integration (see ticket [#966](https://github.com/CredComSoc/cofi-app-llm/issues/966)).
            1. Might be post-MVP.
        3. LLM registration via Xero app.
            1. Might be post-MVP.
    2. **QuickBooks:**
        1. Client user interactions as per [v1.1 requirement](https://hackmd.io/x7b95YKQQs2ApC9PGFHVSQ?both) 5.3.
        2. QuickBooks app launcher integration
            1. Might be post-MVP.
        3. LLM registration via QuickBooks app.
            1. Might be post-MVP.
    3. Collected invoice data can be subjected to [further processing](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-5635).

### 9. Additional testing notes

*   Tickets with relevant testing scripts/requirements:
    *   1315:
        *   Xero:
            *   'Xero connection & invoice import':
                *   _'Basic connection'_
                *   _'Collection of invoices from before connection is established'_
                *   _'Check that it is not possible to connect to a Xero organisation with an existing connection...'_
            *   'Xero disconnection': all sections
            *   'Xero reconnection': all sections
        *   QuickBooks:
            *   tbc - need to modify testing scripts in 1315
*   If deliberate disconnect by Client User from Local Loop platform side, wipe data from all downstream tables:
    *   Delete data from staging
    *   Ensure that propagation logic from core to final is per client user and not for the whole set

**Board clean-up notes**

*   Tickets that can be closed because their testing scripts are relevant, but captured by #1315:
    *   849; 923; 1080; 961; 889
*   Tickets that can be closed as obsolete:
    *   

### 10. Post-MVP notes

*   Xero partner certification
    *   [Application form](https://docs.google.com/forms/d/e/1FAIpQLSdnauYFf3yCaZF3lzAKXlQBIgI2QRZCWojZ87aJfUj5RWrXgw/viewform)
    *   Notes
        *   [https://developer.xero.com/xero-developer-platform-terms-conditions](https://developer.xero.com/xero-developer-platform-terms-conditions)
        *   'Your terms should also clearly describe how and why you collect, store, use and share any user data.'
        *   14\. Collaborators: Sometimes, you might want to use a third party (like a subcontractor or a third party development company) to help you connect to the developer platform - we call them collaborators.
            *   Review with respect to Promis
        *   15\. Security
            *   Ask Paul to review
        *   Might need to deploy Sign Up with Xero functionality to demo. Otherwise share dev instance?
    *   See also emails
*   Connect/disconnect/reconnect:
    *   May ask client user to confirm from app side after they have deliberately removed a connection from the accounting platform side.
    *   More sophisticated restoration/re-syncing of data reconnection (see [here](https://app.clickup.com/9015918923/v/dc/8cp80ab-3915/8cp80ab-4215?block=block-c56f5adb-c3a0-4069-ac08-09e83c3d2f29) for MVP notes).
        *   NB: MVP implementation seems to be that invoices from previous connections are retained in invoices\_core - review whether this diverges from notes linked to above, consider implications if so. Also seems uncertain whether file upload invoices are retained through connect/disconnect cycles - initial impression is that they are also deleted on disconnect - for further investigation.
*   Monitoring changes to accounting platforms:
    *   Developments to Xero affordances for partial payments, as improvements seem to be in high demand.
    *   Most efficient way to monitor and respond to API changes?
        *   Set up mcsdevs to subscribe to platforms and forward to Yani & Paul personal emails?
*   Top candidates for further platforms:
    1. FreeAgent
    2. Invoice2Go
    3. Sage:
        1. Previously ruled out on Hugh T-F's advice, but may be staging a come-back:
            1. [https://www.accountingweb.co.uk/tech/accounting-software/sage-ceo-ai-is-the-future-but-well-always-need-accountants?cm-uuid=76ed1e59-e82d-4752-90cf-e267bd8bcdcf](https://www.accountingweb.co.uk/tech/accounting-software/sage-ceo-ai-is-the-future-but-well-always-need-accountants?cm-uuid=76ed1e59-e82d-4752-90cf-e267bd8bcdcf)
    4. Could also specify with respect to target market share:
        1. Market guides:
            1. [https://www.gartner.com/en](https://www.gartner.com/en)
            2. [https://accountinginsights.org/gartner-magic-quadrant-insights-for-accounting-software/](https://accountinginsights.org/gartner-magic-quadrant-insights-for-accounting-software/)

---

## 2. Collect invoice data

### 1. Collected invoice data accurately reflects the current state of those of the client user's issued invoices that are suitable for clearing, as captured by their accounting platform, from 01/01/2024 to the present.

1. **WHY:** Invoice data is the basis for service delivery.
2. **WHAT:**
    1. **Xero**
        1. Invoice data collection as per:
            1. [v1.1 requirements](https://hackmd.io/x7b95YKQQs2ApC9PGFHVSQ?both) 4.1.4 and 4.1.6
            2. [late-June changes to v1.1](https://docs.google.com/document/d/1te7A3OHt029ztpIlxA5qx55-wJc-p_3lQTpbf7bhmQc/edit?tab=t.0#heading=h.6vsswlj6g8cq)
            3. v1.2 increments
            4. MVP additions:
                1. Include Xero invoice IDs in Admin User view & downloadable Promis .csv as per [ticket #1371](https://github.com/CredComSoc/cofi-app-llm/issues/1371).
                2. Pro forma invoices:
                    1. Start collecting 'Description' field as per [ticket #1479](https://github.com/CredComSoc/cofi-app-llm/issues/1479).
                        1. NB: unlikely this will help much, but research indicates that some users will use this to indicate pro forma status, and so can use to identify and filter out post-collection.
                3. CIS invoices:
                    1. Start collecting the 'Account' field as per [ticket #1481](https://github.com/CredComSoc/cofi-app-llm/issues/1481).
                        1. See [this article](https://central.xero.com/s/article/Enable-CIS-in-your-organisation#AbouttheCISsystemaccounts) for explanation as to why collecting this field and then filtering during post-collection will work.
                4. Include currency field in schema and display field to Admin User
                    1. We believe that this field is already being collected, but need to confirm.
                    2. Need to look at Xero API for specific field name etc.
        2. 'Status' field
            1. Mapping of Xero user actions to 'Status' field as per [ticket #1373](https://github.com/CredComSoc/cofi-app-llm/issues/1373).
                1. See also [ticket #1223](https://github.com/orgs/CredComSoc/projects/6/views/8?pane=issue&itemId=116746026&issue=CredComSoc%7Ccofi-app-llm%7C1223) for mapping of Xero (and QuickBooks) statuses to Promis 'Status' field, and onward mapping to Issuance Status, Payment Status, and Voided Status (although NB that onward mappings are now being done at ETL stage - only Xero & QuickBooks statuses to Promis 'Status' is relevant here).
            2. Invoices with a Status of 'AUTHORISED' should be loaded before invoices with a Status of 'PAID' as per [ticket #1478](https://github.com/CredComSoc/cofi-app-llm/issues/1478).
    2. **QuickBooks**
        1. Invoice data collection as per:
            1. [v1.1 requirement 5.3](https://hackmd.io/x7b95YKQQs2ApC9PGFHVSQ?both)
            2. [late-June changes to v1.1](https://docs.google.com/document/d/1te7A3OHt029ztpIlxA5qx55-wJc-p_3lQTpbf7bhmQc/edit?tab=t.0#heading=h.6vsswlj6g8cq)
            3. v1.2 increments
            4. MVP additions:
                1. Include QuickBooks invoice IDs in Admin User view & downloadable Promis .csv as per [ticket #1372](https://github.com/CredComSoc/cofi-app-llm/issues/1372).
                2. Pro forma invoices:
                    1. Start collecting 'Description' field as per [ticket #1482](https://github.com/CredComSoc/cofi-app-llm/issues/1482).
                        1. NB: unlikely this will help much, but research indicates that some users will use this to indicate pro forma status, and so can use to identify and filter out post-collection.
                3. CIS invoices:
                    1. Start collecting the 'Product Code' field (appears as 'Product/Service' in the QuickBooks interface) as per [ticket #1483](https://github.com/CredComSoc/cofi-app-llm/issues/1483) and 'VAT' field as per [ticket #1484](https://github.com/CredComSoc/cofi-app-llm/issues/1484)
                        1. See [this source](https://www.youtube.com/watch?v=Qbba4IsUM2I) for explanation as to why this will work.
                        2. NB: further investigation of QuickBooks API may be needed to confirm correct fields.
                    2. Include currency field in schema and display field to Admin User
                        1. We believe that this field is already being collected, but need to confirm
                        2. Need to look at QuickBooks API for specific field name etc.
        2. 'Status' field
            1. Mapping of QuickBooks user actions to 'Status' field as per [ticket #1373](https://github.com/CredComSoc/cofi-app-llm/issues/1373) and [ticket #1304](https://github.com/CredComSoc/cofi-app-llm/issues/1304).
                1. See also [ticket #1223](https://github.com/orgs/CredComSoc/projects/6/views/8?pane=issue&itemId=116746026&issue=CredComSoc%7Ccofi-app-llm%7C1223) for mapping of QuickBooks (and Xero) statuses to Promis 'Status' field, and onward mapping to Issuance Status, Payment Status, and Voided Status (although NB that onward mappings are now being done at ETL stage - only Xero & QuickBooks statuses to Promis 'Status' is relevant here).
            2. Invoices with a Status of 'AUTHORISED' should be loaded before invoices with a Status of 'PAID' as per [ticket #1478](https://github.com/CredComSoc/cofi-app-llm/issues/1478).

### 9. Additional testing notes

*   Tickets with relevant testing scripts/requirements:
    *   1315:
        *   Xero:
            *   'Xero connection & invoice import':
                *   _'Basic connection'_
                *   _'Invoice Promis statuses'_
                    *   Check that no modifications needed from #1223
                *   _'Correctly getting updates resulting from payments'_
                *   '_Correctly getting updates resulting from changes other than payments_'
        *   QuickBooks:
            *   tbc - need to modify testing scripts in 1315
*   Check 'Collected On' and 'Updated At' timestamps:
    *   'Collected On' should correspond to time of invoice creation in Xero/QB
    *   'Updated At' should correspond to time of most recent invoice edit in Xero/QB
    *   See also ticket #1344 for testing script (may need to be modified)
*   Ensure not collecting received invoices
*   Test whether a change in one client user's Promis data also triggers Promis calls for all other client users. Current implementation seems to have been sensibly done, but needs rigorous testing.
*   Review and confirm QuickBooks invoice deletion behaviour and corresponding value of 'Status'.
*   v1.1/1.2 observations:
    *   All Amounts Due are £0.00? (Observed after connecting to QB)
        *   Check this with respect to Payment Status implementation on [ticket #1373](https://github.com/CredComSoc/cofi-app-llm/issues/1373) (including comment about full payments from 29/09)
    *   Invoices with Statuses that are updated post-collection from e.g. 'AUTHORISED' to 'VOIDED' are disappearing (whereas should be kept - see notes on [ticket #1373](https://github.com/CredComSoc/cofi-app-llm/issues/1373)) - discussed with Paul on 7/10, but confirm that addressed.
    *   Bug observed with Paul on 7/10 that - during demo of initial Xero connection testing script - invoice issued after connection was not collected. Confirm that addressed.
    *   

**Board clean-up notes**

*   Tickets that can be closed because their testing scripts are relevant, but captured by #1315:
    *   940; 1117; 1230
*   Tickets that can be closed as obsolete:

### 10. Post-MVP notes

*   Invoice data collection:
    *   Direct debits: [ticket #1258](https://github.com/CredComSoc/cofi-app-llm/issues/1258) has a comment that includes a 'DirectDebitEnabled' Xero field that we might be able to collect and filter on?
    *   Investigate other types of invoices using [this source](https://www.invoicesoftwarefinder.com/Invoices-Types/Self-Billing-Invoice)
    *   Line items
        *   These do not affect amount due, or any other field that it is necessary for clearing, but may offer an improvement to analytics.
    *   Xero invoice histories/lifecycle tracing & reporting, timestamp collection - see ticket #977.
    *   Collecting received invoices
        *   Search [Invoice Data Processing MVP](https://app.clickup.com/9015918923/v/dc/8cp80ab-3915/8cp80ab-4215) and v1.1/1.2 requirements docs for relevant notes.
    *   Start accepting invoices with associated direct debits?
    *   Accepting CIS invoices?
*   'Status' field:
    *   May be desirable to have a 'PART PAID' value of Status for Xero (as per QuickBooks), although the benefit will be marginal as we don't need to explicitly track this (Amount Due suffices).
    *   QuickBooks: work out if can use 'Save and share link' and 'Save & Share (WhatsApp)' actions to update Status from 'DRAFT' to 'AUTHORISED'
        *   At the moment, only the 'Save and send' (via email) action does this, and not safe to collect invoices unless this has happened, as QuickBooks does not clearly distinguish these as drafts - see [these notes](https://app.clickup.com/9015918923/v/dc/8cp80ab-3915/8cp80ab-4215?block=block-85c5826e-6e93-4a49-b247-4176cbf43760) and [this comment](https://github.com/CredComSoc/cofi-app-llm/issues/1304#issuecomment-3348152064) on ticket #1304 for more detail.
*   Collecting credit/debit notes?
    *   Search [Invoice Data Processing MVP doc](https://app.clickup.com/9015918923/v/dc/8cp80ab-3915/8cp80ab-4215) for notes
    *   Handling of unallocated credit/debit notes?

---

## 3. Collect contacts data

### 1. 'Contact'/'Customer' data to inform debtor Organisation Identification

1. **WHY:**
    1. [Organisation identification and reconciliation](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-5675) is a requirement for service delivery, and it may or may not be easy to identify a client user's debtors just from the Contact 'name' field included with collected invoice data. It will also be useful to collect client users' creditors so that we can enable them to invite their suppliers.
2. **WHAT:**
    1. Xero:
        1. See tickets [#1258](https://github.com/CredComSoc/cofi-app-llm/issues/1258), [#1364](https://github.com/CredComSoc/cofi-app-llm/issues/1364).
    2. QuickBooks:
        1. See tickets [#1365](https://github.com/CredComSoc/cofi-app-llm/issues/1365).

---

## 4. Number of connections & concurrency

### 1. Number of connections supported by each accounting platform is not a constraint on growth in number of client users

1. **WHY:** We aim to serve 100-1000 client users through the MVP. The limiting factor to growth needs to be sales capacity, rather than constraints imposed by accounting platforms.
2. **WHAT:**
    1. Xero imposes limits on the number of active connections between itself and the LLM app. We need to ensure that we comply with their requirements for these limits not to constrain growth in client user numbers.
        1. Needs to be addressed via partnership certification process (see ticket [#1144](https://github.com/CredComSoc/cofi-app-llm/issues/1144)).
    2. QuickBooks don't impose equivalent limits.
    3. Concurrency/limitations imposed by Promis: has been upgraded by Neil, and should be fine for MVP, but will need to be load tested.

---

**Document Metadata:**
- **Created:** 2025-01-06
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-4435
- **Authors:** Tom Woodroof (87646788)
- **Contributors:** Paul Maker (100554191), Abrar Chowdhury (94738045), Jimmy Mo (94532600)
