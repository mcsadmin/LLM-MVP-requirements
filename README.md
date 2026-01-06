# LLM MVP Requirements Documentation

## Overview

This repository contains product requirements documentation for the Local Loop Merseyside (LLM) MVP platform.

**Target Audience:** Small development team (product owner, junior to senior developers)  
**Purpose:** Source of truth for ongoing MVP and post-MVP development  
**Total Requirements:** 33

---

## Quick Navigation

- [System Functions](#system-functions) (8 requirements)
- [Client User Features](#client-user-features) (8 requirements)
- [Admin User Features](#admin-user-features) (3 requirements)
- [General Requirements](#general-requirements) (14 requirements)
- [Tag Index](#tag-index)

---

## System Functions

02. [Promis Data Collection](requirements/system-functions/02-promis-data-collection.md) `#SystemFunction #PromisIntegration #DataProcessing`
03. [Promis Data Pre-Processing](requirements/system-functions/03-promis-data-pre-processing.md) `#SystemFunction #PromisIntegration #DataProcessing`
04. [AI Data Extraction from Non-Promis Files](requirements/system-functions/04-ai-data-extraction-from-non-promis-files.md) `#SystemFunction #PromisIntegration #DataProcessing`
05. [Non-Promis Data Pre-Processing](requirements/system-functions/05-non-promis-data-pre-processing.md) `#SystemFunction #PromisIntegration #DataProcessing`
06. [Organisation Identification & Reconciliation](requirements/system-functions/06-organisation-identification-reconciliation.md) `#SystemFunction`
07. [Unified Invoice Entries Tables & ETL](requirements/system-functions/07-unified-invoice-entries-tables-etl.md) `#SystemFunction #Invoices`
12. [Clearing Cycle](requirements/system-functions/12-clearing-cycle.md) `#SystemFunction #Clearing`
30. [App Texts Framework](requirements/system-functions/30-app-texts-framework.md) `#SystemFunction`

---

## Client User Features

01. [Non-Promis File Upload](requirements/client-user/01-non-promis-file-upload.md) `#ClientUser #PromisIntegration`
08. [Invoice Eligibility Status Actions](requirements/client-user/08-invoice-eligibility-status-actions.md) `#ClientUser #Invoices`
09. [Invoices Visibility](requirements/client-user/09-invoices-visibility.md) `#ClientUser #Invoices`
10. [Invoice Submission Status Actions](requirements/client-user/10-invoice-submission-status-actions.md) `#ClientUser #Invoices`
11. [Non-Promis Issued Invoice Edit & Report Actions](requirements/client-user/11-non-promis-issued-invoice-edit-report-actions.md) `#ClientUser #PromisIntegration #Invoices`
15. [Visibility of Client User's Received Invoices](requirements/client-user/15-visibility-of-client-user-s-received-invoices.md) `#ClientUser #Invoices`
20. [Registration and Confirmation](requirements/client-user/20-registration-and-confirmation.md) `#ClientUser`
21. [Sign In and Password Reset](requirements/client-user/21-sign-in-and-password-reset.md) `#ClientUser`

---

## Admin User Features

16. [Send & Receive Clearing Sets to/from Cycles](requirements/admin-user/16-send-receive-clearing-sets-to-from-cycles.md) `#AdminUser #Clearing`
18. [Admin User Interface](requirements/admin-user/18-admin-user-interface.md) `#AdminUser`
26. [Process Results from Cycles](requirements/admin-user/26-process-results-from-cycles.md) `#AdminUser`

---

## General Requirements

13. [Client User Interface](requirements/general/13-client-user-interface.md) 
14. [Logging](requirements/general/14-logging.md) 
17. [General UI/UX](requirements/general/17-general-ui-ux.md) 
19. [Account/Profile](requirements/general/19-account-profile.md) 
22. [Support](requirements/general/22-support.md) 
23. [In-app Education](requirements/general/23-in-app-education.md) 
24. [App Texts](requirements/general/24-app-texts.md) 
25. [Data Security Audit](requirements/general/25-data-security-audit.md) `#DataProcessing`
27. [NFRs](requirements/general/27-nfrs.md) 
28. [Clearing Outcomes](requirements/general/28-clearing-outcomes.md) `#Clearing`
29. [Notifications](requirements/general/29-notifications.md) 
31. [CRM integration](requirements/general/31-crm-integration.md) 
32. [Requirements Template](requirements/general/32-requirements-template.md) 
33. [Automated results implementation](requirements/general/33-automated-results-implementation.md) 

---

## Tag Index

### #AdminUser (3 requirements)

- [16. Send & Receive Clearing Sets to/from Cycles](requirements/admin-user/16-send-receive-clearing-sets-to-from-cycles.md)
- [18. Admin User Interface](requirements/admin-user/18-admin-user-interface.md)
- [26. Process Results from Cycles](requirements/admin-user/26-process-results-from-cycles.md)

### #Clearing (3 requirements)

- [12. Clearing Cycle](requirements/system-functions/12-clearing-cycle.md)
- [16. Send & Receive Clearing Sets to/from Cycles](requirements/admin-user/16-send-receive-clearing-sets-to-from-cycles.md)
- [28. Clearing Outcomes](requirements/general/28-clearing-outcomes.md)

### #ClientUser (8 requirements)

- [01. Non-Promis File Upload](requirements/client-user/01-non-promis-file-upload.md)
- [08. Invoice Eligibility Status Actions](requirements/client-user/08-invoice-eligibility-status-actions.md)
- [09. Invoices Visibility](requirements/client-user/09-invoices-visibility.md)
- [10. Invoice Submission Status Actions](requirements/client-user/10-invoice-submission-status-actions.md)
- [11. Non-Promis Issued Invoice Edit & Report Actions](requirements/client-user/11-non-promis-issued-invoice-edit-report-actions.md)
- [15. Visibility of Client User's Received Invoices](requirements/client-user/15-visibility-of-client-user-s-received-invoices.md)
- [20. Registration and Confirmation](requirements/client-user/20-registration-and-confirmation.md)
- [21. Sign In and Password Reset](requirements/client-user/21-sign-in-and-password-reset.md)

### #DataProcessing (5 requirements)

- [02. Promis Data Collection](requirements/system-functions/02-promis-data-collection.md)
- [03. Promis Data Pre-Processing](requirements/system-functions/03-promis-data-pre-processing.md)
- [04. AI Data Extraction from Non-Promis Files](requirements/system-functions/04-ai-data-extraction-from-non-promis-files.md)
- [05. Non-Promis Data Pre-Processing](requirements/system-functions/05-non-promis-data-pre-processing.md)
- [25. Data Security Audit](requirements/general/25-data-security-audit.md)

### #Invoices (6 requirements)

- [07. Unified Invoice Entries Tables & ETL](requirements/system-functions/07-unified-invoice-entries-tables-etl.md)
- [08. Invoice Eligibility Status Actions](requirements/client-user/08-invoice-eligibility-status-actions.md)
- [09. Invoices Visibility](requirements/client-user/09-invoices-visibility.md)
- [10. Invoice Submission Status Actions](requirements/client-user/10-invoice-submission-status-actions.md)
- [11. Non-Promis Issued Invoice Edit & Report Actions](requirements/client-user/11-non-promis-issued-invoice-edit-report-actions.md)
- [15. Visibility of Client User's Received Invoices](requirements/client-user/15-visibility-of-client-user-s-received-invoices.md)

### #PromisIntegration (6 requirements)

- [01. Non-Promis File Upload](requirements/client-user/01-non-promis-file-upload.md)
- [02. Promis Data Collection](requirements/system-functions/02-promis-data-collection.md)
- [03. Promis Data Pre-Processing](requirements/system-functions/03-promis-data-pre-processing.md)
- [04. AI Data Extraction from Non-Promis Files](requirements/system-functions/04-ai-data-extraction-from-non-promis-files.md)
- [05. Non-Promis Data Pre-Processing](requirements/system-functions/05-non-promis-data-pre-processing.md)
- [11. Non-Promis Issued Invoice Edit & Report Actions](requirements/client-user/11-non-promis-issued-invoice-edit-report-actions.md)

### #SystemFunction (8 requirements)

- [02. Promis Data Collection](requirements/system-functions/02-promis-data-collection.md)
- [03. Promis Data Pre-Processing](requirements/system-functions/03-promis-data-pre-processing.md)
- [04. AI Data Extraction from Non-Promis Files](requirements/system-functions/04-ai-data-extraction-from-non-promis-files.md)
- [05. Non-Promis Data Pre-Processing](requirements/system-functions/05-non-promis-data-pre-processing.md)
- [06. Organisation Identification & Reconciliation](requirements/system-functions/06-organisation-identification-reconciliation.md)
- [07. Unified Invoice Entries Tables & ETL](requirements/system-functions/07-unified-invoice-entries-tables-etl.md)
- [12. Clearing Cycle](requirements/system-functions/12-clearing-cycle.md)
- [30. App Texts Framework](requirements/system-functions/30-app-texts-framework.md)

---

## Document Structure

Each requirement document follows this structure:

1. **Metadata Header**
   - Sequence number
   - Source reference
   - ClickUp page ID
   - Last updated date
   - Tags

2. **Main Requirements**
   - Numbered sections with WHY and WHAT
   - Detailed specifications

3. **Testing Notes (Section 9)**
   - Test scenarios and scripts
   - Board cleanup notes
   - Regression testing requirements

4. **Post-MVP Notes (Section 10)**
   - Future enhancements
   - Deferred features
   - Technical debt

5. **Document Metadata Footer**
   - Creation date
   - Source system details
   - ClickUp IDs for traceability

---

## Internal Links

✅ **All internal ClickUp links have been converted to relative markdown links**

Links between requirements automatically navigate to the correct document. All cross-references are preserved and functional.

---

## Migration Notes

**Source:** ClickUp workspace (ID: 9015918923)  
**Source Document:** MVP Requirements (ID: 8cp80ab-3995)  
**Migration Date:** 2026-01-06  
**Mapping:** One-to-one from ClickUp pages to markdown files  
**Preservation:** All original content preserved without modification  
**Link Conversion:** All internal ClickUp links converted to relative paths

---

## Publishing to GitBook

This repository is configured for GitBook publishing:

1. **SUMMARY.md** - Table of contents for GitBook navigation
2. **.gitbook.yaml** - GitBook configuration

### To publish:

1. Go to [gitbook.com](https://gitbook.com)
2. Create a new space
3. Enable Git Sync (Configure → Git Sync → Enable GitHub Sync)
4. Connect to: **mcsadmin/LLM-MVP-requirements**
5. Choose sync direction: **GitHub → GitBook**

---

**Repository Created:** 2025-01-06  
**Last Updated:** 2026-01-06  
**Total Requirements:** 33
