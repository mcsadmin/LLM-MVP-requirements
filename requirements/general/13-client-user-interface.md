# Client User Interface

**Sequence:** 13  
**Source:** MVP Requirements / Client User Interface  
**ClickUp Page ID:** 8cp80ab-6095  
**Last Updated:** 2025-11-25  
**Tags:** 

---

# 1\. Client User Interface
### 1\. Specified via [functional prototype](https://www.figma.com/make/RfBiMBvhtNo9GvikU6l6FL/Local-Loop-MVP-prototype-v1?node-id=0-1&p=f) plus Harry Fox's [static designs](https://www.figma.com/design/VWYqn8yxSQqWw4j6q7s6wi/Local-Loop-Handover?node-id=0-1&p=f&t=iwIkCj58681n7XLB-0).

### 10\. Post-MVP notes
**Notes from invoice data processing doc**
*   Abstract new set of static designs from MVP and/or functional prototype and propagate comments on original so that we have a clean source of truth?
*   Presentation of likely benefits of upcoming cycle, plus scope/potential to improve my benefits (making an informed decision as to further attention/effort). See ['User Dashboard' section](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-f4f511a8-bd48-49ef-8253-fb4f0b9db4fe) of MVP drafting for further thinking.
*   See Harry's [Design Principles doc](https://docs.google.com/document/d/1WL-PB-Sk5HDVaj-mgeT4yvCsG7_Jont1qNzqS9RSsZU/edit?tab=t.0), [Round 2 Usability Testing Summary (5 participants) doc](https://docs.google.com/document/d/1-83NOPvN-0JCYG2KHm8NJeCngnHH07vUgBvKf3GdVjQ/edit?tab=t.0#heading=h.wlchplokysal), and [Handover doc](https://docs.google.com/document/d/1_kweEtATIpH2O0Vi3224a-x14ZPaqS0B7QSkdVvQWcA/edit?tab=t.0#heading=h.hpujvuoophzj) for some further notes.
*   Move/include Sent and Received amount totals in final confirmation?
*   Make 'Getting Started' on Home screen dynamic/responsive
*   Disable 'Submit for Clearing' button whilst Promis is syncing?
*   Show canonical (or other) names of trading partners, perhaps in invoice details?
*   Additional possible prompts:
    *   Pre-Submission Amounts Due confirmation/amendment (see also [note](../../requirements/system-functions/12-clearing-cycle.md?block=block-dce144e5-2d6b-46bc-b139-10c94bf840f9) on potential for corresponding window during Clearing Cycle)
    *   Post-clearing actions (see also [note](../../requirements/system-functions/12-clearing-cycle.md?block=block-229fb960-5031-44cd-a7d1-5256013daad1) on potential for corresponding window during Clearing Cycle):
        *   Implement results
        *   Make residual payments?
    *   See post-MVP notes for Registration for other possible prompts
    *   **Dil's 'prompt framework' draft**
        1. Consideration could be given to a cost/risk benefit analysis of combining all or parts of the  Prompt & Notifications frameworks.
        2. _The app has a Client user  prompting system which allows recommendations for action to be delivered to clients. The system needs to be able to:_
            1. Evaluate data relevant to the User to determine which Prompt to deliver, in which context
            2. Present the Prompt to the user  appropriately
            3. Allow the User to interact with the Prompt to as appropriate, which will take the form of either asking to be taken to the appropriate place in the app to act upon the Prompt or acknowledge (and thus dismiss) the Prompt
            4. allow for new Prompt Types to be specified over time (and others removed)
            5. allow Prompt Types to be set as Active/Inactive
            6. Allow analytics (through logging) as to the outcomes of Prompts
            7. WHY: Client Users’ benefit from using the LLM Service can be significantly increased if, in certain circumstances, they take certain actions. If Prompts can encourage such actions, this  will improve their outcome and also that of all Clients (and thus impact, and thus user satisfaction and thus business viability).
            8. WHAT: The Prompt Framework supports creation and delivery of  Prompt Messages as uniquely identifiable instances created on the basis of a Prompt Type Specification.
                1. Prompt Messages are defined here as: in-app popovers suggesting beneficial course of action to Users, relevant to their current Client User Account Conditions, coupled with a means whereby the User can select their action/preference in regard to individual messages
                    1. Prompt Content is ‘advice’ in text form, to consist of a single paragraph in a single text style. 
                    2. The framework must also be able to deliver a clickable ‘Prompt Call To Action’ alongside the Prompt Content (typically a labeled button or linked text to take the user to a relevant page \[in or beyond the app\] with any necessary information embedded in the URL). 
                    3. The User should have a way of acknowledging (and thus dismissing) the Prompt without using the Call To Action.
            9. HOW: Prompt Messages will be delivered to Users on the basis of Client User Account Conditions through a clearly identifiable Prompt component on specified pages.
        3. _Candidate solution material_ 
            1. The Prompt framework must allow for specification / editing / testing / switching on and off of an arbitrary number of Prompt Type Specifications
                1. Prompt Type Specification is defined here to consist of:
                    1. Unique Prompt Name (a few words)
                    2. The Client User Account Conditions which trigger the delivery of a Prompt Message
                    3. Setting of the initial Notification Attributes
                        1. Prompt Content
                        2. Prompt Call To Action
                    4. Prompt Contexts - in-app pages where the Prompt should appear

---

**Document Metadata:**
- **Created:** 2025-11-24
- **Sequence Number:** 13
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-6095
