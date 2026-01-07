# Testing Script: Invoice Submission Status Actions

**Related Requirements:** [10-invoice-submission-status-actions.md](10-invoice-submission-status-actions.md)  
**Feature:** Invoice Submission Status Actions #ClientUser  
**Test Scope:** Submission Status (creditor) and Submission Status (debtor) state transitions, visibility rules, action availability, and cross-party behavior  
**Created:** 2026-01-07

---

## Overview

This testing script validates the Invoice Submission Status Actions feature, which manages whether invoices are included in the clearing cycle through two independent fields: **Submission Status (creditor)** and **Submission Status (debtor)**. Both parties must consent via an opt-out design.

### Key Testing Principles

1. **Dual-field independence**: Creditor and debtor statuses operate independently
2. **Cross-party visibility**: When one party excludes, invoice disappears for counterparty
3. **Time-window sensitivity**: Different actions available during Data Acceptance/Review Window vs Submission Window
4. **Auto-exclusion rules**: Multiple conditions trigger automatic exclusion (creditor only)
5. **Multi-user coordination**: Tests require multiple Client User accounts to validate cross-party behavior

---

## Test Environment Setup

### Prerequisites

- **Multiple Client User accounts** (minimum 2): Required to test cross-party visibility and coordination
- **Connected trading partners**: Accounts must have invoices linking them (creditor-debtor relationships)
- **Time window control**: Ability to simulate Data Acceptance/Review Window and Submission Window states
- **Invoice types**: Both Promis and non-Promis invoices available for testing
- **Timestamp control**: Ability to set/manipulate collected_on and updated_at timestamps
- **Eligibility Status control**: Ability to set invoices to 'eligible', 'potentially eligible', or 'ineligible'

### Test Data Requirements

| Invoice ID | Type | Creditor | Debtor | Eligibility Status | Due Date | Notes |
|------------|------|----------|--------|-------------------|----------|-------|
| INV-001 | Promis | User A | User B | eligible | Future (normal) | Baseline case |
| INV-002 | Promis | User A | User B | eligible | Adverse | For adverse Due Date testing |
| INV-003 | non-Promis | User A | User B | eligible | Future (normal) | File upload invoice |
| INV-004 | Promis | User A | User B | potentially eligible | Future | Ineligible status test |
| INV-005 | Promis | User A | User B | eligible | Future | For Total Due revision test |
| INV-006 | non-Promis | User A | User B | eligible | Future | For incorrect data extraction test |
| INV-007 | Promis | User A | User B | eligible | Future | Fresh invoice (recent timestamp) |

---

## Section 1: Status Field Initialization and 'Submission not Possible' Status

### Test 1.1: Default Status for Eligible Invoices
**Objective**: Verify that eligible invoices default to 'Ready for Final Submission' for both creditor and debtor

**Preconditions**:
- Invoice INV-001 exists with Eligibility Status = 'eligible'
- No manual actions performed yet

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to invoice list
3. Locate INV-001
4. Check Submission Status (creditor) value

**Expected Result**:
- Submission Status (creditor) = 'Ready for Final Submission'

**Test Steps** (continued):
5. Log in as debtor (User B)
6. Navigate to invoice list
7. Locate INV-001
8. Check Submission Status (debtor) value

**Expected Result**:
- Submission Status (debtor) = 'Ready for Final Submission'

---

### Test 1.2: 'Submission not Possible' Due to Ineligible Status
**Objective**: Verify invoices with Eligibility Status other than 'eligible' have 'Submission not Possible' status

**Preconditions**:
- Invoice INV-004 has Eligibility Status = 'potentially eligible'

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to invoice list
3. Attempt to locate INV-004

**Expected Result**:
- INV-004 is **not visible** to creditor

**Test Steps** (continued):
4. Log in as debtor (User B)
5. Navigate to invoice list
6. Attempt to locate INV-004

**Expected Result**:
- INV-004 is **not visible** to debtor
- No actions available for either party

**Repeat test with**:
- Eligibility Status = 'ineligible'

---

### Test 1.3: 'Submission not Possible' Due to Upward Total Due Revision (Promis)
**Objective**: Verify Promis invoices with upward Total Due revision after collection are blocked from submission

**Preconditions**:
- Invoice INV-005 is a Promis invoice
- INV-005 was initially collected with Total Due = £1,000
- INV-005 Eligibility Status = 'eligible'

**Test Steps**:
1. Via Promis platform (e.g., Xero), increase Total Due to £1,200
2. Wait for platform sync/collection
3. Log in as creditor (User A)
4. Navigate to invoice list
5. Attempt to locate INV-005

**Expected Result**:
- INV-005 is **not visible** to creditor
- Submission Status (creditor) = 'Submission not Possible'

**Test Steps** (continued):
6. Log in as debtor (User B)
7. Attempt to locate INV-005

**Expected Result**:
- INV-005 is **not visible** to debtor
- Submission Status (debtor) = 'Submission not Possible'

**Important**: Test that **downward** revisions do NOT trigger 'Submission not Possible':
- Repeat test reducing Total Due from £1,000 to £800
- Expected: Invoice remains visible with 'Ready for Final Submission' status

---

### Test 1.4: 'Submission not Possible' Due to Reported Incorrect Data (non-Promis)
**Objective**: Verify non-Promis invoices reported as having incorrectly extracted data are blocked from submission (creditor only)

**Preconditions**:
- Invoice INV-006 is a non-Promis (file upload) invoice
- Creditor has reported INV-006 as having incorrectly extracted data (see requirement 11-non-promis-issued-invoice-edit-report-actions.md)

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to invoice list
3. Attempt to locate INV-006

**Expected Result**:
- INV-006 is **not visible** to creditor
- Submission Status (creditor) = 'Submission not Possible'

**Test Steps** (continued):
4. Log in as debtor (User B)
5. Attempt to locate INV-006

**Expected Result**:
- INV-006 is **not visible** to debtor
- Submission Status (debtor) = 'Submission not Possible'

---

## Section 2: Manual Exclusion Actions - Creditor Perspective

### Test 2.1: Creditor Excludes from 'Ready for Final Submission' Status
**Objective**: Verify creditor can manually exclude an invoice from their clearing set

**Preconditions**:
- Invoice INV-001 has Submission Status (creditor) = 'Ready for Final Submission'
- INV-001 is in Data Acceptance/Review Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'clearing set'
3. Locate INV-001
4. Verify 'exclude' action is available
5. Click 'exclude' action

**Expected Result**:
- Submission Status (creditor) changes to 'Excluded (manual)'
- INV-001 disappears from 'clearing set'
- INV-001 appears in creditor's 'excluded' list

---

### Test 2.2: Invoice Disappears for Debtor After Creditor Exclusion
**Objective**: Verify cross-party visibility rule when creditor excludes invoice

**Preconditions**:
- Test 2.1 completed successfully
- INV-001 has Submission Status (creditor) = 'Excluded (manual)'

**Test Steps**:
1. Log in as debtor (User B)
2. Navigate to 'clearing set'
3. Attempt to locate INV-001

**Expected Result**:
- INV-001 is **not visible** in debtor's 'clearing set'

**Test Steps** (continued):
4. Navigate to debtor's 'excluded' list
5. Attempt to locate INV-001

**Expected Result**:
- INV-001 is **not visible** in debtor's 'excluded' list
- Invoice has disappeared **almost immediately** (verify timing: should be < 2 seconds)

---

### Test 2.3: Creditor Undo Action After Manual Exclusion (Data Acceptance/Review Window)
**Objective**: Verify creditor can undo manual exclusion immediately after action

**Preconditions**:
- Test 2.1 completed
- Still within Data Acceptance/Review Window
- No time elapsed since exclusion (test immediately)

**Test Steps**:
1. Remain logged in as creditor (User A)
2. In 'excluded' list, locate INV-001
3. Verify 'undo' action is available
4. Click 'undo' action

**Expected Result**:
- Submission Status (creditor) changes back to 'Ready for Final Submission'
- INV-001 disappears from 'excluded' list
- INV-001 reappears in 'clearing set'

---

### Test 2.4: Creditor Restore Action After Time Elapsed (Data Acceptance/Review Window)
**Objective**: Verify creditor can restore excluded invoice using 'restore' action (standing option)

**Preconditions**:
- Invoice INV-001 has Submission Status (creditor) = 'Excluded (manual)'
- Time has elapsed since exclusion (simulate passage of time)
- Still within Data Acceptance/Review Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'excluded' list
3. Locate INV-001
4. Verify 'undo' action is **not available** (temporary option expired)
5. Verify 'restore' action **is available** (standing option)
6. Click 'restore' action

**Expected Result**:
- Submission Status (creditor) changes back to 'Ready for Final Submission'
- INV-001 disappears from 'excluded' list
- INV-001 reappears in 'clearing set'

---

### Test 2.5: Creditor Undo Action During Submission Window
**Objective**: Verify creditor can undo exclusion during Submission Window (restores to 'Final Submitted' not 'Ready for Final Submission')

**Preconditions**:
- Invoice INV-001 was in 'Final Submitted' status
- Creditor excluded INV-001 during Submission Window
- Submission Status (creditor) = 'Excluded (manual)'
- Still in Submission Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'excluded' list
3. Locate INV-001
4. Verify 'undo' action is available
5. Click 'undo' action

**Expected Result**:
- Submission Status (creditor) changes back to 'Final Submitted' (NOT 'Ready for Final Submission')
- INV-001 disappears from 'excluded' list
- INV-001 reappears in 'clearing set'

---

### Test 2.6: Adverse Due Date Warning on Restore (Creditor)
**Objective**: Verify warning message appears when creditor restores invoice with adverse Due Date

**Preconditions**:
- Invoice INV-002 has adverse Due Date (on/after present date, before end of Submission Window)
- INV-002 has Submission Status (creditor) = 'Excluded (manual)' or 'Excluded (auto)'

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'excluded' list
3. Locate INV-002
4. Click 'restore' (or 'undo') action

**Expected Result**:
- Warning message displayed: "This may encourage your debtor to pay late" (or similar wording per requirement)
- User must confirm or cancel
- If confirmed, Submission Status (creditor) changes to 'Ready for Final Submission'

---

## Section 3: Manual Exclusion Actions - Debtor Perspective

### Test 3.1: Debtor Excludes from 'Ready for Final Submission' Status
**Objective**: Verify debtor can manually exclude an invoice from their clearing set

**Preconditions**:
- Invoice INV-001 has Submission Status (debtor) = 'Ready for Final Submission'
- INV-001 is in Data Acceptance/Review Window

**Test Steps**:
1. Log in as debtor (User B)
2. Navigate to 'clearing set'
3. Locate INV-001
4. Verify 'exclude' action is available
5. Click 'exclude' action

**Expected Result**:
- Submission Status (debtor) changes to 'Excluded (manual)'
- INV-001 disappears from 'clearing set'
- INV-001 appears in debtor's 'excluded' list

---

### Test 3.2: Invoice Disappears for Creditor After Debtor Exclusion
**Objective**: Verify cross-party visibility rule when debtor excludes invoice

**Preconditions**:
- Test 3.1 completed successfully
- INV-001 has Submission Status (debtor) = 'Excluded (manual)'

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'clearing set'
3. Attempt to locate INV-001

**Expected Result**:
- INV-001 is **not visible** in creditor's 'clearing set'

**Test Steps** (continued):
4. Navigate to creditor's 'excluded' list
5. Attempt to locate INV-001

**Expected Result**:
- INV-001 is **not visible** in creditor's 'excluded' list
- Invoice has disappeared **almost immediately** (verify timing: should be < 2 seconds)

---

### Test 3.3: Debtor Undo Action After Manual Exclusion (Data Acceptance/Review Window)
**Objective**: Verify debtor can undo manual exclusion immediately after action

**Preconditions**:
- Test 3.1 completed
- Still within Data Acceptance/Review Window
- No time elapsed since exclusion (test immediately)

**Test Steps**:
1. Remain logged in as debtor (User B)
2. In 'excluded' list, locate INV-001
3. Verify 'undo' action is available
4. Click 'undo' action

**Expected Result**:
- Submission Status (debtor) changes back to 'Ready for Final Submission'
- INV-001 disappears from 'excluded' list
- INV-001 reappears in 'clearing set'

---

### Test 3.4: Debtor Restore Action After Time Elapsed (Data Acceptance/Review Window)
**Objective**: Verify debtor can restore excluded invoice using 'restore' action (standing option)

**Preconditions**:
- Invoice INV-001 has Submission Status (debtor) = 'Excluded (manual)'
- Time has elapsed since exclusion
- Still within Data Acceptance/Review Window

**Test Steps**:
1. Log in as debtor (User B)
2. Navigate to 'excluded' list
3. Locate INV-001
4. Verify 'undo' action is **not available** (temporary option expired)
5. Verify 'restore' action **is available** (standing option)
6. Click 'restore' action

**Expected Result**:
- Submission Status (debtor) changes back to 'Ready for Final Submission'
- INV-001 disappears from 'excluded' list
- INV-001 reappears in 'clearing set'

---

### Test 3.5: Debtor Undo Action During Submission Window
**Objective**: Verify debtor can undo exclusion during Submission Window (restores to 'Final Submitted')

**Preconditions**:
- Invoice INV-001 was in 'Final Submitted' status
- Debtor excluded INV-001 during Submission Window
- Submission Status (debtor) = 'Excluded (manual)'
- Still in Submission Window

**Test Steps**:
1. Log in as debtor (User B)
2. Navigate to 'excluded' list
3. Locate INV-001
4. Verify 'undo' action is available
5. Click 'undo' action

**Expected Result**:
- Submission Status (debtor) changes back to 'Final Submitted' (NOT 'Ready for Final Submission')
- INV-001 disappears from 'excluded' list
- INV-001 reappears in 'clearing set'

---

### Test 3.6: Adverse Due Date Warning on Restore (Debtor)
**Objective**: Verify warning message appears when debtor restores invoice with adverse Due Date

**Preconditions**:
- Invoice INV-002 has adverse Due Date
- INV-002 has Submission Status (debtor) = 'Excluded (manual)'

**Test Steps**:
1. Log in as debtor (User B)
2. Navigate to 'excluded' list
3. Locate INV-002
4. Click 'restore' (or 'undo') action

**Expected Result**:
- Warning message displayed: "This may send a signal that intending to pay their creditor late" (or similar wording per requirement)
- User must confirm or cancel
- If confirmed, Submission Status (debtor) changes to 'Ready for Final Submission'

---

## Section 4: Auto-Exclusion Rules (Creditor Only)

### Test 4.1: Auto-Exclusion Due to Adverse Due Date
**Objective**: Verify invoices with adverse Due Date are automatically excluded for creditor

**Preconditions**:
- Invoice INV-002 has Eligibility Status = 'eligible'
- INV-002 Due Date is on or after present date, but before end of Submission Window
- Currently in Submission Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'excluded' list (NOT 'clearing set')
3. Locate INV-002

**Expected Result**:
- INV-002 is visible in creditor's 'excluded' list
- Submission Status (creditor) = 'Excluded (auto)'
- INV-002 is **not** in 'clearing set'

**Test Steps** (continued):
4. Log in as debtor (User B)
5. Navigate to 'clearing set'
6. Locate INV-002

**Expected Result**:
- INV-002 is **visible** in debtor's 'clearing set'
- Submission Status (debtor) = 'Ready for Final Submission'
- Debtor is unaffected by creditor's auto-exclusion

---

### Test 4.2: Auto-Exclusion Due to Recent collected_on Timestamp
**Objective**: Verify invoices with collected_on timestamp within Submission Window are auto-excluded for creditor

**Preconditions**:
- Invoice INV-007 has Eligibility Status = 'eligible'
- INV-007 collected_on timestamp is within current Submission Window
- Currently in Submission Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'excluded' list
3. Locate INV-007

**Expected Result**:
- INV-007 is visible in creditor's 'excluded' list
- Submission Status (creditor) = 'Excluded (auto)'

**Test Steps** (continued):
4. Log in as debtor (User B)
5. Navigate to 'clearing set'
6. Locate INV-007

**Expected Result**:
- INV-007 is visible in debtor's 'clearing set'
- Submission Status (debtor) = 'Ready for Final Submission'

---

### Test 4.3: Auto-Exclusion Due to Recent updated_at Timestamp
**Objective**: Verify invoices with updated_at timestamp within Submission Window are auto-excluded for creditor

**Preconditions**:
- Invoice INV-001 has Eligibility Status = 'eligible'
- Invoice data was updated during current Submission Window (e.g., Total Due revised downward)
- updated_at timestamp reflects this change

**Test Steps**:
1. Update invoice data during Submission Window
2. Log in as creditor (User A)
3. Navigate to 'excluded' list
4. Locate INV-001

**Expected Result**:
- INV-001 is visible in creditor's 'excluded' list
- Submission Status (creditor) = 'Excluded (auto)'

**Note**: Per requirements, for new invoices, created_at = updated_at, so checking updated_at covers both new and modified invoices.

---

### Test 4.4: Auto-Exclusion Due to Debtor Registration During Submission Window
**Objective**: Verify invoice is auto-excluded for creditor when debtor registers during Submission Window

**Preconditions**:
- Invoice INV-001 exists with creditor User A
- Debtor User B is not yet registered on platform
- INV-001 has Eligibility Status = 'potentially eligible' (debtor not registered)
- Currently in Submission Window

**Test Steps**:
1. Debtor User B registers on platform during Submission Window
2. Wait for Eligibility Status to update to 'eligible'
3. Log in as creditor (User A)
4. Navigate to 'excluded' list
5. Locate INV-001

**Expected Result**:
- INV-001 is visible in creditor's 'excluded' list
- Submission Status (creditor) = 'Excluded (auto)'
- Eligibility Status = 'eligible'

**Test Steps** (continued):
6. Log in as newly registered debtor (User B)
7. Navigate to 'clearing set'
8. Locate INV-001

**Expected Result**:
- INV-001 is visible in debtor's 'clearing set'
- Submission Status (debtor) = 'Ready for Final Submission'

---

### Test 4.5: Creditor Can Restore Auto-Excluded Invoice
**Objective**: Verify creditor can override auto-exclusion using 'restore' action

**Preconditions**:
- Invoice INV-002 has Submission Status (creditor) = 'Excluded (auto)' (any auto-exclusion condition)
- Within Data Acceptance/Review Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'excluded' list
3. Locate INV-002
4. Verify 'restore' action is available
5. Click 'restore' action

**Expected Result**:
- Submission Status (creditor) changes to 'Ready for Final Submission'
- INV-002 disappears from 'excluded' list
- INV-002 appears in 'clearing set'
- If adverse Due Date, warning message displayed (as per Test 2.6)

---

## Section 5: Final Submission Confirmation

### Test 5.1: Creditor Performs Final Submission Confirmation
**Objective**: Verify creditor can perform final submission confirmation during Submission Window

**Preconditions**:
- Invoice INV-001 has Submission Status (creditor) = 'Ready for Final Submission'
- Currently in Submission Window (NOT Data Acceptance/Review Window)
- INV-001 is in creditor's 'clearing set'

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'clearing set'
3. Verify 'final submission confirmation' action is available
4. Perform 'final submission confirmation' action for all invoices in clearing set (including INV-001)

**Expected Result**:
- Submission Status (creditor) changes to 'Final Submitted' for INV-001
- INV-001 remains in 'clearing set' (still visible)

---

### Test 5.2: Debtor Performs Final Submission Confirmation
**Objective**: Verify debtor can perform final submission confirmation during Submission Window

**Preconditions**:
- Invoice INV-001 has Submission Status (debtor) = 'Ready for Final Submission'
- Currently in Submission Window
- INV-001 is in debtor's 'clearing set'

**Test Steps**:
1. Log in as debtor (User B)
2. Navigate to 'clearing set'
3. Verify 'final submission confirmation' action is available
4. Perform 'final submission confirmation' action for all invoices in clearing set (including INV-001)

**Expected Result**:
- Submission Status (debtor) changes to 'Final Submitted' for INV-001
- INV-001 remains in 'clearing set' (still visible)

---

### Test 5.3: Final Submission Confirmation Not Available Outside Submission Window
**Objective**: Verify 'final submission confirmation' action is only available during Submission Window

**Preconditions**:
- Invoice INV-001 has Submission Status (creditor) = 'Ready for Final Submission'
- Currently in Data Acceptance/Review Window (NOT Submission Window)

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'clearing set'
3. Locate INV-001
4. Check available actions

**Expected Result**:
- 'final submission confirmation' action is **not available**
- Only 'exclude' action is available

**Repeat for debtor perspective**.

---

### Test 5.4: Creditor Excludes from 'Final Submitted' Status
**Objective**: Verify creditor can exclude invoice even after performing final submission

**Preconditions**:
- Test 5.1 completed
- Invoice INV-001 has Submission Status (creditor) = 'Final Submitted'
- Still within Submission Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'clearing set'
3. Locate INV-001
4. Verify 'exclude' action is available
5. Click 'exclude' action

**Expected Result**:
- Submission Status (creditor) changes to 'Excluded (manual)'
- INV-001 disappears from 'clearing set'
- INV-001 appears in 'excluded' list

---

### Test 5.5: Debtor Excludes from 'Final Submitted' Status
**Objective**: Verify debtor can exclude invoice even after performing final submission

**Preconditions**:
- Test 5.2 completed
- Invoice INV-001 has Submission Status (debtor) = 'Final Submitted'
- Still within Submission Window

**Test Steps**:
1. Log in as debtor (User B)
2. Navigate to 'clearing set'
3. Locate INV-001
4. Verify 'exclude' action is available
5. Click 'exclude' action

**Expected Result**:
- Submission Status (debtor) changes to 'Excluded (manual)'
- INV-001 disappears from 'clearing set'
- INV-001 appears in 'excluded' list

---

## Section 6: Cross-Party Coordination Scenarios

### Test 6.1: Both Parties Submit - Invoice Enters Clearing
**Objective**: Verify invoice enters clearing when both creditor and debtor have 'Final Submitted' status

**Preconditions**:
- Invoice INV-001 initially has:
  - Submission Status (creditor) = 'Ready for Final Submission'
  - Submission Status (debtor) = 'Ready for Final Submission'
- Currently in Submission Window

**Test Steps**:
1. Creditor (User A) performs final submission confirmation
2. Debtor (User B) performs final submission confirmation
3. Verify final status

**Expected Result**:
- Submission Status (creditor) = 'Final Submitted'
- Submission Status (debtor) = 'Final Submitted'
- Invoice is eligible for inclusion in clearing cycle

---

### Test 6.2: Creditor Submits, Debtor Excludes - Invoice Does Not Enter Clearing
**Objective**: Verify invoice does not enter clearing when one party excludes

**Preconditions**:
- Invoice INV-001 initially has both statuses = 'Ready for Final Submission'
- Currently in Submission Window

**Test Steps**:
1. Creditor (User A) performs final submission confirmation
   - Submission Status (creditor) = 'Final Submitted'
2. Debtor (User B) excludes invoice
   - Submission Status (debtor) = 'Excluded (manual)'
3. Check if invoice enters clearing

**Expected Result**:
- Invoice does **not** enter clearing cycle
- Creditor can no longer see INV-001 (cross-party visibility rule)

---

### Test 6.3: Creditor Auto-Excluded, Debtor Submits - Invoice Does Not Enter Clearing
**Objective**: Verify invoice does not enter clearing when creditor is auto-excluded

**Preconditions**:
- Invoice INV-002 has adverse Due Date
- Submission Status (creditor) = 'Excluded (auto)'
- Submission Status (debtor) = 'Ready for Final Submission'
- Currently in Submission Window

**Test Steps**:
1. Debtor (User B) performs final submission confirmation
   - Submission Status (debtor) = 'Final Submitted'
2. Verify creditor status remains 'Excluded (auto)'
3. Check if invoice enters clearing

**Expected Result**:
- Invoice does **not** enter clearing cycle
- Both statuses must be 'Final Submitted' for clearing inclusion

---

### Test 6.4: Race Condition - Simultaneous Exclusion by Both Parties
**Objective**: Verify system handles simultaneous exclusion actions gracefully

**Preconditions**:
- Invoice INV-001 has both statuses = 'Ready for Final Submission'
- Two users logged in simultaneously

**Test Steps**:
1. Creditor (User A) and Debtor (User B) click 'exclude' action simultaneously (or within 1 second)
2. Verify final state for both parties

**Expected Result**:
- Submission Status (creditor) = 'Excluded (manual)'
- Submission Status (debtor) = 'Excluded (manual)'
- Each user sees invoice in their own 'excluded' list
- Each user does **not** see invoice in counterparty's view
- No errors or data corruption

---

### Test 6.5: Creditor Excludes Then Restores - Debtor Sees Reappearance
**Objective**: Verify invoice reappears for debtor when creditor restores after exclusion

**Preconditions**:
- Invoice INV-001 initially visible to both parties

**Test Steps**:
1. Creditor (User A) excludes INV-001
2. Verify debtor (User B) can no longer see INV-001
3. Creditor (User A) restores INV-001
4. Immediately check debtor's view

**Expected Result**:
- After step 2: INV-001 not visible to debtor
- After step 4: INV-001 reappears in debtor's 'clearing set'
- Reappearance should occur almost immediately (< 2 seconds)

---

## Section 7: Time Window Transitions

### Test 7.1: Actions Change When Transitioning to Submission Window
**Objective**: Verify action availability changes when moving from Data Acceptance/Review Window to Submission Window

**Preconditions**:
- Invoice INV-001 has Submission Status (creditor) = 'Ready for Final Submission'
- Currently in Data Acceptance/Review Window

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'clearing set'
3. Note available actions for INV-001 (should be 'exclude' only)
4. Wait for transition to Submission Window (or simulate)
5. Refresh view
6. Check available actions

**Expected Result**:
- During Data Acceptance/Review Window: 'exclude' action available; 'final submission confirmation' NOT available
- During Submission Window: both 'exclude' and 'final submission confirmation' actions available

---

### Test 7.2: Undo vs Restore Action Availability Based on Window
**Objective**: Verify 'undo' behavior differs between Data Acceptance/Review Window and Submission Window

**Preconditions**:
- Invoice INV-001 was 'Ready for Final Submission', then excluded by creditor
- Submission Status (creditor) = 'Excluded (manual)'

**Test Steps**:
1. During Data Acceptance/Review Window:
   - Creditor clicks 'undo'
   - Expected: Status returns to 'Ready for Final Submission'
2. Exclude again
3. Perform 'final submission confirmation' (now in Submission Window)
   - Status changes to 'Final Submitted'
4. Exclude again during Submission Window
   - Status changes to 'Excluded (manual)'
5. Click 'undo'
6. Verify target status

**Expected Result**:
- Step 1: Undo returns status to 'Ready for Final Submission'
- Step 5: Undo returns status to 'Final Submitted' (NOT 'Ready for Final Submission')

---

## Section 8: Edge Cases and Error Conditions

### Test 8.1: Prompt Visibility Disappearance Timing
**Objective**: Verify invoice disappears for counterparty "almost immediately" (< 2 seconds) after exclusion

**Preconditions**:
- Invoice INV-001 visible to both parties
- Two browser sessions open simultaneously (creditor and debtor views)

**Test Steps**:
1. Start timer
2. Creditor (User A) clicks 'exclude'
3. Immediately observe debtor (User B) view (auto-refresh or manual refresh)
4. Measure time until INV-001 disappears from debtor's view

**Expected Result**:
- Invoice disappears from debtor's view in < 2 seconds
- No lag-induced bugs (e.g., debtor shouldn't be able to act on invoice after creditor exclusion)

**Note**: If immediate disappearance not possible, requirements note potential need for 'Excluded (by both)' status - flag as issue if timing exceeds 2 seconds.

---

### Test 8.2: Multiple Invoice Batch Operations
**Objective**: Verify correct behavior when user excludes multiple invoices simultaneously

**Preconditions**:
- Multiple invoices (INV-001, INV-002, INV-003) all with 'Ready for Final Submission' status
- Batch selection UI available

**Test Steps**:
1. Log in as creditor (User A)
2. Select multiple invoices in 'clearing set'
3. Perform batch 'exclude' action

**Expected Result**:
- All selected invoices change to 'Excluded (manual)'
- All disappear from creditor's 'clearing set'
- All appear in creditor's 'excluded' list
- All disappear from debtor's view

---

### Test 8.3: Eligibility Status Changes During Submission Process
**Objective**: Verify handling when Eligibility Status changes from 'eligible' to 'ineligible' mid-process

**Preconditions**:
- Invoice INV-001 has Eligibility Status = 'eligible'
- Submission Status (creditor) = 'Final Submitted'
- Submission Status (debtor) = 'Ready for Final Submission'

**Test Steps**:
1. Simulate Eligibility Status change to 'ineligible' (e.g., debtor account suspended)
2. Check visibility and status for both parties

**Expected Result**:
- Submission Status (creditor) changes to 'Submission not Possible'
- Submission Status (debtor) changes to 'Submission not Possible'
- Invoice becomes not visible to both parties
- Invoice is excluded from clearing cycle

---

### Test 8.4: Debtor Excluded Invoice Remains Hidden After Creditor Final Submission
**Objective**: Verify debtor exclusion persists even if creditor performs final submission

**Preconditions**:
- Invoice INV-001 has:
  - Submission Status (creditor) = 'Ready for Final Submission'
  - Submission Status (debtor) = 'Excluded (manual)'

**Test Steps**:
1. Creditor (User A) performs final submission confirmation
2. Check creditor's view
3. Check debtor's view

**Expected Result**:
- Creditor cannot see INV-001 (debtor exclusion causes invoice to disappear for creditor)
- Debtor still sees INV-001 in their 'excluded' list
- Invoice does not enter clearing cycle

---

### Test 8.5: System Performance Under High Volume
**Objective**: Verify system handles large clearing sets efficiently

**Preconditions**:
- Creditor (User A) has 100+ invoices in 'clearing set'
- All with 'Ready for Final Submission' status

**Test Steps**:
1. Log in as creditor
2. Load 'clearing set' view
3. Measure page load time
4. Perform final submission confirmation for all invoices
5. Measure processing time

**Expected Result**:
- Page load time < 3 seconds
- Batch final submission completes in < 10 seconds
- All statuses update correctly
- No timeout errors

---

## Section 9: User Interface and Experience Validation

### Test 9.1: Status Display Consistency
**Objective**: Verify Submission Status values are displayed consistently and correctly throughout UI

**Test Steps**:
1. Navigate to all views where Submission Status is displayed:
   - 'clearing set' view
   - 'excluded' list view
   - Individual invoice detail view
   - Invoice list/table view
2. Verify status labels match requirements exactly:
   - 'Submission not Possible'
   - 'Ready for Final Submission'
   - 'Excluded (manual)' or 'Excluded (auto)'
   - 'Final Submitted'

**Expected Result**:
- All status labels match requirements terminology
- No abbreviations or alternative wording
- Status values are clearly distinguishable

---

### Test 9.2: Action Button Labels and Placement
**Objective**: Verify action buttons use correct labels and are appropriately placed

**Test Steps**:
1. For each status and user role, verify action button labels:
   - 'exclude' button
   - 'undo' button
   - 'restore' button
   - 'final submission confirmation' button/action
2. Verify buttons are contextually appropriate (e.g., 'exclude' appears in 'clearing set', 'restore' in 'excluded' list)

**Expected Result**:
- Action labels match requirements exactly
- Buttons are accessible and visible
- No confusing or ambiguous labels

---

### Test 9.3: Warning Message Content and Timing
**Objective**: Verify warning messages for adverse Due Date use correct wording

**Test Steps**:
1. Trigger adverse Due Date warning for creditor (Test 2.6)
   - Verify message: "this may encourage your debtor to pay late"
2. Trigger adverse Due Date warning for debtor (Test 3.6)
   - Verify message: "this may send a signal that intending to pay their creditor late"

**Expected Result**:
- Warning messages appear before action completes
- Messages are clear and use correct wording per requirements
- User must explicitly confirm or cancel

---

### Test 9.4: Clearing Set vs Excluded List Navigation
**Objective**: Verify users can easily navigate between 'clearing set' and 'excluded' list views

**Test Steps**:
1. Log in as creditor (User A)
2. Navigate to 'clearing set'
3. Verify navigation to 'excluded' list is available and clear
4. Navigate to 'excluded' list
5. Verify navigation back to 'clearing set' is available

**Expected Result**:
- Both views are easily accessible
- Current view is clearly indicated
- Navigation is intuitive

---

## Section 10: Regression and Integration Tests

### Test 10.1: Integration with Eligibility Status Feature
**Objective**: Verify Submission Status correctly responds to Eligibility Status changes (see requirement 08-invoice-eligibility-status-actions.md)

**Test Steps**:
1. Create invoice with Eligibility Status = 'potentially eligible'
   - Verify Submission Status = 'Submission not Possible' (not visible)
2. Change Eligibility Status to 'eligible'
   - Verify Submission Status changes to 'Ready for Final Submission' (becomes visible)
3. Change Eligibility Status back to 'ineligible'
   - Verify Submission Status returns to 'Submission not Possible' (disappears)

**Expected Result**:
- Submission Status field values update immediately when Eligibility Status changes
- Visibility rules are enforced correctly

---

### Test 10.2: Integration with Invoice Visibility Feature
**Objective**: Verify Submission Status visibility aligns with general invoice visibility rules (see requirement 09-invoices-visibility.md)

**Test Steps**:
1. Review general visibility rules from requirement 09
2. Verify Submission Status visibility rules are consistent with general rules
3. Test edge cases where visibility rules might conflict

**Expected Result**:
- No conflicts between general visibility and Submission Status visibility
- Users only see invoices they should have access to

---

### Test 10.3: Integration with Clearing Cycle Feature
**Objective**: Verify invoices are correctly included/excluded from clearing based on Submission Status (see requirement 12-clearing-cycle.md)

**Test Steps**:
1. Set up multiple invoices with various status combinations:
   - Both 'Final Submitted'
   - One 'Final Submitted', one 'Excluded (manual)'
   - Both 'Ready for Final Submission' (not yet submitted)
2. Trigger clearing cycle
3. Verify which invoices were included

**Expected Result**:
- Only invoices with both Submission Status (creditor) = 'Final Submitted' AND Submission Status (debtor) = 'Final Submitted' are included in clearing
- All other combinations are excluded

---

### Test 10.4: Integration with Non-Promis Invoice Edit/Report Feature
**Objective**: Verify reported non-Promis invoices are blocked from submission (see requirement 11-non-promis-issued-invoice-edit-report-actions.md)

**Test Steps**:
1. Upload non-Promis invoice (INV-006)
2. Creditor reports invoice as having incorrectly extracted data
3. Verify Submission Status changes to 'Submission not Possible'
4. Verify invoice becomes not visible to both parties

**Expected Result**:
- Reporting action triggers 'Submission not Possible' status
- Invoice is effectively blocked from clearing

---

## Section 11: Accessibility and Localization

### Test 11.1: Screen Reader Compatibility
**Objective**: Verify all status values and actions are accessible via screen reader

**Test Steps**:
1. Enable screen reader (e.g., NVDA, JAWS, VoiceOver)
2. Navigate to 'clearing set' and 'excluded' list
3. Verify all status labels are read aloud
4. Verify all action buttons are announced correctly

**Expected Result**:
- Status values are clearly announced
- Action buttons are accessible and labeled appropriately
- Navigation is logical for screen reader users

---

### Test 11.2: Keyboard Navigation
**Objective**: Verify all actions can be performed using keyboard only (no mouse)

**Test Steps**:
1. Navigate to 'clearing set' using keyboard (Tab, Arrow keys)
2. Select invoice using keyboard
3. Trigger 'exclude' action using keyboard (Enter/Space)
4. Navigate to 'excluded' list using keyboard
5. Trigger 'restore' action using keyboard

**Expected Result**:
- All interactive elements are keyboard-accessible
- Focus indicators are visible
- Actions can be completed without mouse

---

## Test Execution Summary Template

### Test Run Information
- **Tester Name:** _________________
- **Test Date:** _________________
- **Build/Version:** _________________
- **Environment:** _________________

### Results Summary
| Test Section | Total Tests | Passed | Failed | Blocked | Notes |
|--------------|-------------|--------|--------|---------|-------|
| Section 1: Status Initialization | 4 | | | | |
| Section 2: Creditor Manual Exclusion | 6 | | | | |
| Section 3: Debtor Manual Exclusion | 6 | | | | |
| Section 4: Auto-Exclusion Rules | 5 | | | | |
| Section 5: Final Submission | 5 | | | | |
| Section 6: Cross-Party Coordination | 5 | | | | |
| Section 7: Time Window Transitions | 2 | | | | |
| Section 8: Edge Cases | 5 | | | | |
| Section 9: UI/UX Validation | 4 | | | | |
| Section 10: Integration Tests | 4 | | | | |
| Section 11: Accessibility | 2 | | | | |
| **TOTAL** | **48** | | | | |

### Critical Issues Found
1. 
2. 
3. 

### Non-Critical Issues Found
1. 
2. 
3. 

### Recommendations
1. 
2. 
3. 

---

## Appendix A: Terminology Reference

For consistent testing, use these exact terms from the requirements:

| Term | Definition |
|------|------------|
| **Submission Status (creditor)** | Field managing invoice submission status from creditor perspective |
| **Submission Status (debtor)** | Field managing invoice submission status from debtor perspective |
| **clearing set** | List view of invoices ready for or already submitted to clearing cycle |
| **excluded list** | List view of invoices manually or automatically excluded from clearing |
| **Client User** | User of the application (creditor or debtor) |
| **Eligibility Status** | Separate field determining if invoice qualifies for submission (see requirement 08) |
| **Data Acceptance/Review Window** | Time period for reviewing invoices before final submission |
| **Submission Window** | Time period during which final submission confirmations can be performed |
| **adverse Due Date** | Due Date that is on/after present date but before end of Submission Window |
| **Promis invoice** | Invoice collected from integrated accounting platform (e.g., Xero) |
| **non-Promis invoice** | Invoice uploaded via file upload feature |
| **Total Due** | Amount owed on invoice |
| **collected_on** | Timestamp when invoice data was first collected from source |
| **updated_at** | Timestamp when invoice data was last modified |

---

## Appendix B: Status Transition Diagrams

### Creditor Submission Status State Machine

```
[Eligibility Status ≠ 'eligible'] → Submission not Possible (not visible)
                                    ↓
[Eligibility Status = 'eligible'] → Ready for Final Submission
                                    ↓
                    ┌───────────────┴───────────────┐
                    ↓                               ↓
            Excluded (manual/auto)          Final Submitted
                    ↑                               ↓
                    └───────────────────────────────┘
                    (exclude action available)

Restore/Undo: Excluded → Ready for Final Submission (during Data Acceptance/Review Window)
Undo: Excluded → Final Submitted (during Submission Window, if excluded from Final Submitted)
```

### Debtor Submission Status State Machine

```
[Eligibility Status ≠ 'eligible'] → Submission not Possible (not visible)
                                    ↓
[Eligibility Status = 'eligible'] → Ready for Final Submission
                                    ↓
                    ┌───────────────┴───────────────┐
                    ↓                               ↓
            Excluded (manual)                Final Submitted
                    ↑                               ↓
                    └───────────────────────────────┘
                    (exclude action available)

Restore/Undo: Excluded → Ready for Final Submission (during Data Acceptance/Review Window)
Undo: Excluded → Final Submitted (during Submission Window, if excluded from Final Submitted)
```

---

**End of Testing Script**
