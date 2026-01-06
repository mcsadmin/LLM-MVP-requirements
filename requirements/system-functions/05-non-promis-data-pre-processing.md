# Non-Promis Data Pre-Processing

**Sequence:** 05  
**Source:** MVP Requirements / Non-Promis Data Pre-Processing #SystemFunction  
**ClickUp Page ID:** 8cp80ab-4615  
**Last Updated:** 2025-12-16  
**Tags:** #SystemFunction #PromisIntegration #DataProcessing

---

# 1\. Non-Promis Data Pre-Processing
### 1\. Process Client User's data [collected via file upload](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-5475) and [extracted by an AI](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4475) in preparation for amalgamation with Promis data
1. WHY: This data needs pre-processing before it can be amalgamated with Promis data into an [initial unified invoice table](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4455?block=block-3c3e2c38-0672-48ce-9a2b-7cae0bade50d).
2. WHAT:
    1. See 'Requirements' section of [Non-Promis Data Extraction & Pre-Processing](https://hackmd.io/O9Spdn2ET0u5TjSgPasI9Q) (NB that this also contains requirements for prior [extraction of this data](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4475)).
        1. This also contains a full specification for meeting the requirements via spreadsheet operations.

#### 10\. Post-MVP notes
*   Current AI extraction doesn't reliably determine who is the creditor and who is the debtor
*   Tracking & inference of Amount Due via expected partial payments
*   Requirements for checking if invoice creditor really is Client User (i.e. validation of whether the invoice is definitely issued, and not received or not even referencing client user)
    *   Notes:
        *   organization\_id in invoices\_staging is used to link to organizations table (using id field): MVP assumes that creditor is Client User for both Promis and non-Promis data
        *   Promis and non-Promis v1.1/1.2 pre-processing both contain an instance of the organisation identification function to confirm that the invoice creditor is also the Client User. For Promis data, discuss how to augment this with Invoice Type (i.e. payable or receivable).
        *   Received and self-billing invoices: finalise requirements for these (see v1.2 pre-processing documentation for notes) once organisation ID & reconciliation functionality and tables finalised.
*   MVP implementation is to assign 'Status' directly, then rely on existing onward mapping to Issuance, Payment and Voided statuses. Post-MVP: review adequacy with respect to e.g. note in v1.1/1.2 documentation on 'Due Date in the past might be 'clear evidence'' for Payment Status of 'Paid'.

---

**Document Metadata:**
- **Created:** 2025-06-26
- **Sequence Number:** 05
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-4615
