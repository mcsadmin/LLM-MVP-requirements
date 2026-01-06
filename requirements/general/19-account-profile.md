# Account/Profile

**Sequence:** 19  
**Source:** MVP Requirements / Account/Profile  
**ClickUp Page ID:** 8cp80ab-4715  
**Last Updated:** 2025-11-25  
**Tags:** 

---

# 1\. Account/Profile page
### 1\. Enable client users to manage their account and Profile page
1. WHY: Client Users should be able to trigger account changes without contacting support/admin users; Client Users should be able to control the contents of their Profile.
2. WHAT:
    1. See Profile page on [functional prototype](https://www.figma.com/make/RfBiMBvhtNo9GvikU6l6FL/Local-Loop-MVP-prototype-v1?node-id=0-1&p=f&t=Nn2gwK7q7IWhfb8y-0) and [static designs](http://Profile  ⇤ Profile Profile  ⇤ Reset Password ⇤ Logout Display Name Mutual Credit Services Website www.mutualcredit.services Organisation Name Contact Email Mutua Credit Services Ltd tom@mutualcredit.services Account  Email Description admin@mutualcredit.services We are Mutual Credit Services, founded in 2020 to deliver the credit creation and accounting mechanisms used by the corporate and financial sectors to small businesses and communities. Access to decentralised credit systems promotes resilience, autonomy, and adaptive capacity. Display Name Mutual Credit Services Website www.mutualcredit.services Contact Email Cancel Save tom@mutualcredit.services Description We are Mutual Credit Services, founded in 2020 to deliver the credit creation and accounting mechanisms used by the corporate and financial sectors to small businesses and communities. Access to decentralised credit systems promotes resilience, autonomy, and adaptive capacity. Real Mobile Keyboard q w e r t y u i o p a s d f g h j k l Cancel Save 􀆝 z x c v b n m 􀆛 123 space return 􀆪 􀊰 Home Invoices Submitted Help Home Invoices Submitted Help)
    2. Post-auth password reset is triggered via the same menu

### 9\. Other testing notes
*   Tickets with relevant testing scripts/requirements:
    *   1530; 1531; 1532; 1533; 1534
        *   Might not be complete - need to check with Paul

**Board clean-up notes**
*   Tickets that can be closed as obsolete:
    *   [#1383](https://github.com/CredComSoc/cofi-app-llm/issues/1383); [#810](https://github.com/CredComSoc/cofi-app-llm/issues/810); [#815](https://github.com/CredComSoc/cofi-app-llm/issues/815); [#756](https://github.com/CredComSoc/cofi-app-llm/issues/756); [#995](https://github.com/CredComSoc/cofi-app-llm/issues/995).
### 10\. Post-MVP notes
1. Account management functionality:
    1. Subscription and billing
    2. Full account & data deletion
2. Profile/Account page
    1. Client user should be able to manage the visibility of all fields to other client users.
3. Profile to be populated automatically as far as possible through any data already held as a result of [Registration and Confirmation](../../requirements/client-user/20-registration-and-confirmation.md) and/or Organisation Identification & Reconciliation.
4. Might make Organisation Name and Account Email editable.
5. Retain their data for e.g. 15 days after account deletion in case they change their mind.
    1. Take into account overall service design, especially requirement for other clients to interact with client's data.
6. App also already includes an implementation of [obsolete 2024 design](https://www.figma.com/design/uBNHxRO15NxiDPaCaSSdmJ/LLM-Designs?node-id=1158-2839&t=vZAR2pCBLQPbJJPa-0) (URL: /profile-view) - remove this from codebase?

---

**Document Metadata:**
- **Created:** 2025-07-01
- **Sequence Number:** 19
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-4715
