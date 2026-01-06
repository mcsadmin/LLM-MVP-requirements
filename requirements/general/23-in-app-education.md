# In-app Education

**Sequence:** 23  
**Source:** MVP Requirements / In-app Education  
**ClickUp Page ID:** 8cp80ab-6015  
**Last Updated:** 2025-11-24  
**Tags:** 

---

# 1\. Requirement name - short, meaningful, unique, with a reference
### 1.
Requirement supporting text as needed - as clear and short as possible. **The Why** (plus the **Who** and the **What** if not obvious)...
1. WHY: ...
    1. ...
2. WHAT: ...
    1. Data collection
    2. Submission Status actions

**Dil's draft**
1. **Headline Requirement:** Client Users can access a small number of highly informative/impactful educational assets which convey fundamental aspects of the Local Loop service / offer and help them maximise Local Loop's benefit delivery to their organisation.
2. **Considerations**:
    1. NB: strongly driven by user testing
        1. Clickable prototypes testing sessions can perhaps identify issues which need education interventions (as opposed to refined design)
    2. Co-design with Ops input (Ops capacity to support features must be in place)
    3. Co-design with Marketing/Customer Engagement input (Assets/Content will be required to alongside functionality)
    4. Consider 'First Run / New User ' flag in /User knowledge state associated with Client User account to allow programmatic / configurable management of education offer.
    5. Ability to deliver content at appropriate points
    6. Cater for a variety of learning styles
    7. 'As simple as possible, but no simpler'
        1. Motivate (but do not interfere with or distract from) user actions that will improve their benefits
        2. 'Show not tell' - delivered implicitly through user actions and associated feedbacks?
    8. Testimonials/case studies of particular actions?
    9. Offer (unobtrusive) routes to further resources that augment in-app education
    10. Overlap / interaction with User Dashboard
    11. Use Scribe to capture video walkthrough and put on website?
3. **Notes from invoice data requirements:**
    1. Education to encourage Client Users to do bank reconciliations in the event of partial payments, which will update Amount Due in LLM App.
    2. Education about importance of doing bank feed reconciliations well in advance of (submission for?) clearing.
    3. Education that several things (partial payments (expected or otherwise), credit notes, debit notes...) may affect Amount Due, and they will need to review and perhaps amend this before submitting for clearing, and/or that we may contact them to confirm.
    4. Education that clearing will affect Amount(s) Due, and that results should be quickly implemented to avoid adversely affecting subsequent payments, and hence theirs and their trading partners' financial management.
    5. Education about not being able to accept invoices that have associated standing orders or direct debits.
        1. Education about what to do if they have submitted/cleared invoices anyway.
    6. Education about importance of not submitting invoices with associated standing orders or direct debits for clearing and removing them from clearing dataset via [Eligibility and Submission Status Actions](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-50932998-9cd8-4863-9aee-81599b304b53).
        1. Education about what to do if they have submitted/cleared invoices anyway.
    7. Education about importance of checking for pro forma invoices in advance of (submission for?) clearing and removing them from clearing dataset via [Eligibility and Submission Status Actions](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-50932998-9cd8-4863-9aee-81599b304b53), and/or creating them such that they are not collected in the first place.
        1. Can also include note in education that although we do our best to filter out pro forma invoices, it's primarily responsibility of Client User to create them properly (can link to Xero's instructions).
    8. Education for Promis (Xero) users that credit/debit notes need to be allocated to an invoice to affect Amount Due, and hence clearing.
    9. Education about inability to handle/clear CIS invoices for MVP.
        1. Education about what to do if they have submitted/cleared invoices anyway.
    10. Education about importance of not submitting disputed invoices for clearing and removing them from clearing dataset via [Eligibility and Submission Status Actions](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-50932998-9cd8-4863-9aee-81599b304b53).
    11. Education about importance of not submitting invoices which have been written off (but this is not yet reflected in Xero) for clearing and removing them from clearing dataset via [Eligibility and Submission Status Actions](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-50932998-9cd8-4863-9aee-81599b304b53).
    12. Education about importance of not submitting invoices which have not yet been through either side's approval process (including correct purchase orders) for clearing and removing them from clearing dataset via [Eligibility and Submission Status Actions](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-50932998-9cd8-4863-9aee-81599b304b53).
    13. See also Pre-processing (Promis and non-Promis) documentation for further notes.
    14. Propagated from UI/UX feedback doc: 'More emphasis on the fact that suppliers and customers also stand to benefit from submitting invoices for clearing would be nice.'
    15. Education about invoice Status: submitting means that confirming that invoice is: issued; unpaid; not voided.
        1. May be particularly important for file upload users, who may not understand that should only upload unpaid invoices. See also [this note](../../requirements/client-user/11-non-promis-issued-invoice-edit-report-actions.md?block=block-aed66c59-8d76-4000-9ad0-db58d1aaf87a) about prompting deletion for invoices with a Due Date far in the past.
        2. Education about what to do if they have submitted/cleared invoices anyway.
    16. Education for QuickBooks users that they have to email ('Save and send') invoices to their customers in order for them to appear in the app/be eligible for clearing
        1. This is because QuickBooks does not have a clear concept of a draft, and so if we just collect all saved invoices, it's very likely (particularly with autosubmit) that we'll end up clearing a lot of invoices that have not actually been finalised/would not be considered issued by one or both parties.
        2. Note that the other two sending options (sharing a link or sharing via WhatsApp) currently have no effect on Status, and so are effectively not supported by MVP.
4. See Harry's [Design Principles doc](https://docs.google.com/document/d/1WL-PB-Sk5HDVaj-mgeT4yvCsG7_Jont1qNzqS9RSsZU/edit?tab=t.0), [Round 2 Usability Testing Summary (5 participants) doc](https://docs.google.com/document/d/1-83NOPvN-0JCYG2KHm8NJeCngnHH07vUgBvKf3GdVjQ/edit?tab=t.0#heading=h.wlchplokysal), and [Handover doc](https://docs.google.com/document/d/1_kweEtATIpH2O0Vi3224a-x14ZPaqS0B7QSkdVvQWcA/edit?tab=t.0#heading=h.hpujvuoophzj) for some further notes.
5. Education about being able to review (add, exclude and restore) invoices to/from clearing set, even after final submission for this cycle.
6. Education about making residual payments on each invoice as per original terms?
7. Explain why sent/issued invoices that are imported or updated during Submission Window are auto-excluded, and cannot be restored.
8. Explain why received invoices from suppliers who are also in LLM are not visible if Client User (who is the debtor in this scenario) has registered during Submission Window
    1. Technical reason is that these are auto-excluded on the creditor Client User side, which means they are hidden from the debtor (at least for MVP)

### 10\. Post-MVP notes

---

**Document Metadata:**
- **Created:** 2025-11-24
- **Sequence Number:** 23
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-6015
