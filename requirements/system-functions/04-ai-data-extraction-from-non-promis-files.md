# AI Data Extraction from Non-Promis Files

**Sequence:** 04  
**Source:** MVP Requirements / AI Data Extraction from Non-Promis Files #SystemFunction  
**ClickUp Page ID:** 8cp80ab-4475  
**Last Updated:** 2025-11-25  
**Tags:** #SystemFunction #PromisIntegration #DataProcessing

---

# 1\. AI data extraction
### 1\. Rapid and accurate automatic extraction of obligation data from uploaded/non-Promis files
1. WHY: manual extraction of data from [uploaded/non-Promis files](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4335) is time-consuming, tedious, and error-prone, and is hard to subject to continuous improvement.
2. WHAT:
    1. See 'Requirements' section of [Non-Promis Data Extraction & Pre-Processing](https://hackmd.io/O9Spdn2ET0u5TjSgPasI9Q) (NB that this also contains requirements for subsequent [pre-processing of this data](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4615)).
        1. This also contains a full specification for meeting the requirements via spreadsheet operations.

#### 9\. Additional testing notes
*   Tickets with relevant testing scripts/requirements:
    *   1338; 1340; 1341; 1541; 1542
        *   Need to check with Paul to ensure that this list is complete.
*   Ensure that pdf files which appear to have multiple invoices are marked as invalid/quarantined.

**Board clean-up notes**
*   Tickets that can be closed as obsolete:
    *   819; 774; 609; 753; 859; 860; 1182; 684; 858; 675; 608; 602

#### 10\. Post-MVP notes
*   AI data extraction for multiple invoices per pdf has been built by Eugene, but [@Paul Maker](#user_mention#100554191) decided not to merge for MVP - need to merge this in due course. Until it has been merged and tested, will be marked as invalid/quarantined
*   Handling of credit/debit notes, any other obligation types?
*   Contacting Swati for large invoice data set to train our own AI invoice data extraction model.
    *   Done - see email 15th September
####

---

**Document Metadata:**
- **Created:** 2025-06-25
- **Sequence Number:** 04
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-4475
