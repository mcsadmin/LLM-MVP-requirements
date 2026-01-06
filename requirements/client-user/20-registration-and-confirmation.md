# Registration and Confirmation

**Sequence:** 20  
**Source:** MVP Requirements / Registration and Confirmation #ClientUser  
**ClickUp Page ID:** 8cp80ab-4935  
**Last Updated:** 2025-11-25  
**Tags:** #ClientUser

---

# 1\. Registration and Confirmation
### 1\. Registration to Local Loop should be as straightforward as possible.
1. WHAT:
    1. See [static designs](http://Get Started now Back  Next Sign in to your Account Get Started now Enter your email and password  Enter your Organisation name Enter your email and password to log in  Email Organization Name Email localloop@gmail.com localloop@gmail.com localloop@gmail.com Password Password ******* ******* Forgot Password ? Next By registering, you confirm that you are authorized to share business data on behalf of your organization. All data will be kept confidential, used only to provide feedback to you/your Organization or for anonymized aggregated analysis, and never shared without explicit consent. We comply fully with UK GDPR and store all data securely. Log In Description Or Or Continue with QuickBooks Read full Terms & Conditions Continue with QuickBooks Continue with Xero Back  Join  Continue with Xero Already have an account? Login Already have an account? Login Don’t have an account? Sign Up Forgot Password Reset Password Enter your Email Enter and confirm your new password Email New Password localloop@gmail.com ******* Confirm Password ******* Forgot Password  Reset Password  Already have an account? Login Already have an account? Login) for interface.
        1. 'Contact us' form accessible?
        2. 'About' page accessible?
    2. Functional requirements:
        1. Organisation Name field has a dropdown populated with IDM data and known debtor organisations. May or may not include existing Client Users.
            1. [These notes](https://app.clickup.com/9015918923/v/dc/8cp80ab-3915/8cp80ab-4215?block=block-7db61d18-cc8c-4d21-8e98-704f68ac7b98) suggest that since using organizations\_public, invoice debtor orgs will not appear - for review.
        2. Successful registration:
            1. Sets Membership Status to 'true'
                1. Need to review whether this will happen with respect to whether or not this is even a field in the organizations table, and how this relates to Client User org identification and reconciliation workflow.
            2. Sends confirmation email
                1. Review v1.1/1.2 implementation - see ticket #893
            3. Redirects to main [Client User Interface](../../requirements/general/13-client-user-interface.md)

### 9\. Additional testing notes
*   Blaze Media mailbox not created when registered on v1.1/1.2.
    *   Display name of org/email associated with Client User’s connected accounting platform?
*   Tickets with relevant testing scripts:
    *   1315; 1487

**Board clean-up notes**
*   Tickets that can be closed because their testing scripts are relevant, but captured by #1315:
    *   1228
*   Tickets that can be closed as obsolete:
    *   1081; 1098; 1006; 884; 965; 953; 951; 772; 852; 773; 596; 744; 963; 964; 933; 299; 1214; 1216

### 10\. Post-MVP notes
**Dil's draft:**
**Headline Requirement:**
1.     1. **New registrations** to Local Loop should be as straightforward as possible, consistent with validating that membership is appropriate and confirming details. The result of a successful registration is a one-to-one relationship between a unique-to-LLM Organisation name and a unique-to-LLM user account email, alongside acceptance of Ts & Cs and any GDPR conditions.
    2. **Confirmations:**
        1. User receives information (by email) about Local Loop, including any specifics about their likely benefits (Refer to System functions: Transactional Emails).
        2. User confirms (by link in email) Email address and Organisation name and location as necessary has been confirmed, Ts and Cs reaffirmed.
2.     1. **Available affordances before registration complete**: Meet marketing requirements: It should be possible to achieve any of these, as decided later, without breaking accepted design or workflow.:
        1. Display short texts, with links to explanatory material
        2. Send a message to LLM support
        3. Access an About page
        4. Access FAQs
        5. Access a video or gif as a popover
3.     1. User can continue without immediately confirming email
        1. Users who have not confirmed their email (via the confirmation email) within a configurable time are not allowed to directly sign in, but should go through the email confirmation email step
        2. Users who have provided a broken email address should have a way back.
4. ACCEPTANCE CRITERIA for a. New Registrations: New signups have provided information which provides validation that they are candidates for Local Loop membership, and provided a unique (to LLM) Organisation name and a unique (to LLM) email address, which has been validated as active and under the user's control. They must also have confirmed their acceptance of the Ts and Cs (and any required GDPR choices).

A 'Starter for ten' workflow suggestion follows, which should be the starting point for solutions.
*   Brief welcome text
    *   Completion by the user of the validation questions (three checkboxes):
        *   That their business is within the LLM area (**condition cb1**).
        *   That they confirm whether the Organisation buys and sells locally on trade credit terms (two checkboxes - (**condition cb2**) for buying and (**condition cb3**) for selling)
*   (Conditional text:
    *   \- \[cb1 false and/or both cb2 and cb3 false\]: 'Sorry but not eligible' message, offering an email newsletter signup.
    *   \- \[cb1 true and either cb2 or cb3 true\]: 'Success' message, and registration continues.
*   App displays:
    *   Terms and Conditions message with link.
*   User provides:
    *   A unique Organisation Name. UI should make it as easy as practical for the user to provide an accurate and valid name, although no hard constraints should be imposed.
        *   Refer to System functions: Organisation Identification, Reconciliation and Characterisation
    *   A unique email as the Client User account identifier. UI should emphasise that it should be a work email address associated with the Organisation.
    *   An acceptable password.
*   \[Only as necessary\] Postcode check
    *   IF: the Organisation name can be confirmed internally as being 'in area', (Refer to System functions: Organisation Identification, Reconciliation and Characterisation) then this step is omitted.
    *   ELSE:
        *   Require Organisation postcode entry by user, with explanation
        *   (As appropriate):
            *   \- \[postcode out of area\]: 'Sorry but not eligible' message, offering an email newsletter signup)
            *   \- \[postcode in area\]: 'Success' message, and registration continues.
*   Confirmation email with link sent to user supplied email - see next section for detail (NB: failure to immediately confirm link should not restrict access to app functions for a defined time period - period to be configurable).
*   User can continue in the app without confirming email.

5. ACCEPTANCE CRITERIA for b. Confirmations: New registrations should be sent a welcome and confirmation email, to which the Client user must respond. Access to the app should be restricted if a satisfactory response to this email has not been received with a defined time period.

This email will be used for any secondary confirmations needed; a 'Starter for ten' workflow suggestion follows, which should be the starting point for solutions.

*   Email is programatically constructed on the basis of information supplied at registration, as followed:
    1. \[Always present\] - Standard welcome text.
    2. \[Conditional\] - if only one of cb2 or cb3 are true, then explanatory text as to options. (_Local Loop will not immediately provide value to such users, as they cannot be in loops. We'd like to encourage them to stay registered, and give us their data, so that we can let them know when we can provide value - say on introduction of Liquidity Injection_)
    3. \[Always present\] - Standard explanatory material, links to Ts&Cs, educational material etc.
    4. \[Always Present\] - Reminder that clicking button is an assertion that the user is authorised to share Organisation financial data with LLM
    5. \[Always present\] - Confirmation button with link to login page, for a normal registered user experience.
    6. \[Conditional as 'b.' above\] - 'Delete Local Loop account' advice - 'go to app Profile/Account screen and use the delete option'.
6. Needs System functions:
    1. Transactional Emails
    2. Organisation Identification, Reconciliation and Characterisation functions
7. A variant of the conditional flow (for an online survey) is shown in [this flowchart](https://hackmd.io/@mcsdocs/r10Rmh-zgg) 

*   Additional membership eligibility notes arising from invoice data processing requirements:
    *   May be desirable to include question about whether typically receive partial payments as part of Registration/onboarding workflow, so that can present relevant prompts/education to either reconcile bank feed (Promis data) or use 'edit amount' functionality (non-Promis data).
    *   May be desirable to include question about whether typically receive standing orders and/or direct debits as part of Registration/onboarding workflow, and possibly prevent businesses who do from joining, or perhaps prompt them to permanently exclude invoices from these trading partners?
    *   May be desirable to include question about whether typically issue pro forma invoices as part of Registration/onboarding workflow.
    *   Include question about whether part of CIS as part of Registration/onboarding workflow, and prevent businesses who are from joining.

#

---

**Document Metadata:**
- **Created:** 2025-07-10
- **Sequence Number:** 20
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-4935
