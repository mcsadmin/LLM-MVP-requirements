# Invoice Eligibility Status Actions

**Sequence:** 08  
**Source:** MVP Requirements / Invoice Eligibility Status Actions #ClientUser  
**ClickUp Page ID:** 8cp80ab-5715  
**Last Updated:** 2025-11-24  
**Tags:** #ClientUser #Invoices

---

# 1\. Eligibility Status & Associated Actions
### 1\. Eligibility Status reflects whether or not an invoice can in principle be submitted for clearing, and so determines whether or not it is [visible](../../requirements/client-user/09-invoices-visibility.md) to Client Users, and if so what actions are available to them.
1. WHY: the likelihood of submission of invoices will increase if:
    1. The interface is not cluttered with invoices which can't be submitted, even in principle
    2. Client User attention is directed toward desirable actions associated with those which are eligible.
2. WHAT:
    1. Eligibility Status values:
        1. 'Eligible': debtor is also a Client User (i.e. Membership Status is 'true'; Issuance Status is 'Issued'; Payment Status is 'Not paid'; Voided Status is 'Not voided':
            1. Available action: all [Submission Status Actions](../../requirements/client-user/10-invoice-submission-status-actions.md)
        2. 'Potentially eligible': debtor is not a Client User (i.e. Membership Status is 'false'), but is a candidate member (i.e. 'B2B?' is 'true' and 'In Catchment Area?' is 'true')
            1. Available action: invite debtor to Local Loop Merseyside (or perhaps request that we invite on Client User's behalf)
                1. NB that debtor characterisation in terms of requirements for candidate membership is carried out by us as part of [Organisation Identification & Reconciliation](https://app.clickup.com/9015918923/v/dc/8cp80ab-3995/8cp80ab-5675) - the Client User does not need to know this information themselves.
                2. NB that since we are not currently collecting received invoices, inviting creditors will have to rely on a different process - could be as simple as a ‘tell us about a supplier’ form with fields for ‘name’, ‘Merseyside?’, and ‘B2B?’.
                    1. Update: might be possible to have identical functionality for suppliers by using contacts data?
        3. 'Ineligible': debtor is not a Client User (i.e. Membership Status is 'false'), and is not a candidate member (i.e. 'B2B?' is 'false' or 'not sure', and/or 'In Catchment Area?' is 'false' or 'not sure')
            1. Available action: none, since these should not be [visible](../../requirements/client-user/09-invoices-visibility.md) in the first place.

###

---

**Document Metadata:**
- **Created:** 2025-08-31
- **Sequence Number:** 08
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5715
