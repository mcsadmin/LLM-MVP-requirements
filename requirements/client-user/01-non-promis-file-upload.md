# Non-Promis File Upload

**Sequence:** 01  
**Source:** MVP Requirements / Non-Promis File Upload #ClientUser  
**ClickUp Page ID:** 8cp80ab-5475  
**Last Updated:** 2025-11-25  
**Tags:** #ClientUser #PromisIntegration

---

# **1\. File Upload**
### 1\. Client user has the simplest practical means of sharing invoice data with LLM in near real-time, in a way which gives confidence and reassurance without additional effort.
1. WHY: Invoice data is the basis for service delivery.
2. WHAT:
    1. File Upload
        1. Instantaneous client user interactions as per [v1.1 requirements](https://hackmd.io/x7b95YKQQs2ApC9PGFHVSQ?both) 1.1.2.7, 1.2.3.3, and 2.3.4.
        2. File types: .pdf only.
        3. Client user can see progress of file upload.
        4. Client user can cancel file upload whilst in progress.
        5. Uploaded files are immediately available for [AI-powered data extraction](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4475).
        6. Client user made aware once data has been [automatically extracted from uploaded files](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4475).
        7. Client user made aware that data extracted from their uploaded files is (or will very soon be) [visible](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-4495).

### 3\. Increment to existing implementation
#### Increments to v1.1
*   1.1.2aii, iii, iv, v, vi, vii.

### 9\. Additional testing notes
*   Tickets with relevant testing scripts/requirements:
    *   1315; 1407; 1413; 1103
        *   Need to check with Paul to ensure that this list is complete.
*   Ensure that timestamp of file upload is propagated to created\_at timestamp and/or otherwise handled such that auto-exclude during Submission Window is applied.
    *   Need to consider file upload timestamp vs extraction into invoice\_staging timestamp

**Board clean-up notes**
*   Tickets that can be closed (archived?) because their testing scripts are relevant, but captured by #1315:
    *   1003
*   Tickets that can be closed (archived?) as obsolete:
    *   816; 1107; 1179; 997; 1384; 1332; 1333; 1004; 1012; 971; 885; 817; 886; 850; 621; 608; 1113

### 10\. Post-MVP notes
*

---

**Document Metadata:**
- **Created:** 2025-08-13
- **Sequence Number:** 01
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5475
