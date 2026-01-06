# Clearing Cycle

**Sequence:** 12  
**Source:** MVP Requirements / Clearing Cycle #SystemFunction  
**ClickUp Page ID:** 8cp80ab-5895  
**Last Updated:** 2025-11-24  
**Tags:** #SystemFunction #Clearing

---

# 1\. Clearing Cycle

1. WHAT:
    1. Each Clearing Cycle is 28 days in length
    2. A Clearing Cycle is divided into two windows (see [diagram](https://www.figma.com/design/W1pZMzwv0FZovtWVTIgquS/Cycle-windows?node-id=0-1&p=f&t=ibLw0n7P9NtQiw21-0)):
        1. Data Acceptance/Review Window (days 1-25 inclusive)
            1. This is the period from the start of the Cycle through to the start of the Submission Window
        2. Submission Window (days 26-28 inclusive)
            1. This is the period from the end of the Data Acceptance/Review Window through to the end of the Cycle
    3. Each Clearing Cycle should have an associated uuid
    4. All invoices with an Eligibility Status of 'eligible' should always be associated with the current Clearing Cycle via its uuid
        1. This ensures that invoices that were collected during previous Cycles and remain eligible (particularly because they have not been fully cleared or otherwise paid) are automatically propagated to/included in the current Cycle when it starts
    5. At the start of a new Clearing Cycle, Submission Statuses of invoices that were associated with the previous Cycle and that still have an Eligibility Status of 'eligible' should be modified as follows:
        1. Submission Status (creditor):
            1. 'Final Submitted' → 'Ready for Final Submission' if Due Date is not adverse for the new Cycle
                1. We assume that the creditor Client User will want us to keep trying to clear the invoices that they previously submitted
            2. 'Final Submitted' → 'Excluded (auto)' if Due Date is now adverse for the new Cycle
            3. 'Excluded (manual)' → 'Excluded (manual)'
                1. This preserves creditor Client User's deliberate exclusion choices
            4. 'Excluded (auto)' → 'Ready for Final Submission' if Due Date is not adverse for the new Cycle
                1. This restores any invoices that were automatically excluded because they:
                    1. had an adverse Due Date during the previous Cycle (but do not for the new Cycle), or
                    2. were imported or updated by the creditor Client User during the Submission Window of the previous Cycle, or
                    3. became eligible during the Submission Window of the previous Cycle because the debtor Client User registered during this period
            5. 'Excluded (auto)' → 'Excluded (auto)' if Due Date is still adverse for the new Cycle
        2. Submission Status (debtor):
            1. 'Final Submitted' → 'Ready for Final Submission'
                1. No need to apply logic for 'adverse' Due Date - the logic is applied on the creditor Client User's side to auto-exclude it, hiding it from the debtor Client User (so the Submission Status (debtor) can safely take this value)
            2. 'Excluded (manual)' → 'Excluded (manual)'

#### 10\. Post-MVP notes
*       *   Introduce window/declaration for reconciling bank feed/otherwise ensuring Amounts Due are up to date before next clearing cycle?
    *   Introduce 'Results Implementation' window? Ask users to confirm that they've done so before they can import new invoices/participate in next cycle?

---

**Document Metadata:**
- **Created:** 2025-10-30
- **Sequence Number:** 12
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5895
