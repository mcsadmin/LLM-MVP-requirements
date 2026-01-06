# Notifications

**Sequence:** 29  
**Source:** MVP Requirements / Notifications  
**ClickUp Page ID:** 8cp80ab-5975  
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

### 10\. Post-MVP notes

**Dil's 'notifications' draft**
1. **Headline Requirement:** Notifications functionality in place, providing:
    *   Awareness to user that there are unread notices
    *   Immediate access to notices via popover from key pages
    *   Route to notifications from menu (not necessarily a top-level menu choice: could be via 'Profile/Account' page
    *   Notification content should be able to include functional buttons
#### Considerations for application:
1.     1.     1. Triggered by [next clearing run timeline](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-380b4a9a-e184-4883-aa98-cc48891549b6)
        2. Respond to the actions of other client users that may improve both parties' benefits, and perhaps those of the wider network:
            1. Submission Status actions
            2. Trading partner implementation of [results](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-14f699c1-da8d-4e59-9b48-b21416f02e7a)?
2.     1.     1. Delayed feedbacks from actions?
        2. Feedbacks from trading partners' actions?
            1. Imported invoice seen?
            2. Intention to pay? (highlight this as another outcome of submission?)
3.     1.     1. Trading partner has joined?
        2. See also Prompts
Additional notes:
*       *   Notification of creditor having made an edit to non-Promis data

**Dil's 'notifications framework' draft**
1. Consideration could be given to a cost/risk benefit analysis of combining all or parts of the  Prompt & Notifications frameworks.
2. _The app has a notifications system which allows information to be delivered to all user types, highlighted, displayed and interacted with. The system needs to be able to:_
    1. Deliver relevant Notifications to the attention of specific Users
    2. Allow relevant User interaction
    3. Allow Users to see the recency/urgency of Notifications
    4. track and respond to the status of Notifications
    5. allow for new Notification Types to be specified over time (and others removed)
    6. allow Notification Types to be set as Active/Inactive 
    7. Allow analytics (through logging) as to the outcomes of Notifications
    8. WHY: The LLM service offer depends upon coordinated information across Client Users and Admin Users. Timely and appropriate actions from users will improve the outcome of the Service for all (and thus impact, and thus user satisfaction and thus business viability).
        1. Different users may make changes at arbitrary times which may require responses.
        2. The 28 day Clearing Cycle will require various user responses at different points.
        3. Thus Users need to be made aware of novel information (data, events, opportunities) which they can act on - both within (and beyond) the app, in order to better achieve and deliver value through the app.
    9. WHAT: The Notification Framework supports creation, delivery, and tracking of state changes of  Notification Messages as uniquely identifiable instances created on the basis of a Notification Type Specification.
        1. Notification Messages are defined here as: messages to the User informing them of something new and relevant to their experience/usage of the LLM Service, coupled with a means whereby the User can indicate their action/preference in regard to individual messages. 
            1. Notification Content is ‘advice’ in text form, to consist of one or more paragraphs in a single text style. 
            2. The framework must also be able to deliver a clickable ‘Notification Call To Action’ alongside the Notification Content (typically a labeled button or linked text to take the user to a relevant page \[in or beyond the app\] with any necessary information embedded in the URL). 
            3. Notification Messages have state, so that Notification Status can be used to control display. 
                1. Notification Message State may be altered by user action - see below - or by changes in criteria  identified in the Notification Type specification.
            4. Notification Messages have a user affordance, such that User actions/preferences can be indicated on a message by message basis. This will usually include an ‘acknowledgement’ .
    10. HOW: 
        1. Delivery: Notifications can to be delivered to Users in two ways:
            1. In app: through a clearly identifiable Notifications component on specified pages with a Notification Status indicator to make it clear whether there are un-resolved notifications.
                1. Interaction with the Notifications component will give access to a structured list of Notification Messages
                2. Unresolved Notification Messages will be presented obviously
                3. Resolved notifications are to be accessible but not highlighted.
            2. By email: with descriptive text and link to the app
3. _(as relevant) Candidate acceptance Criteria_
4. _(as relevant) Candidate solution material_ 
    1. The Notification framework must allow for specification / editing / testing / switching on and off of an arbitrary number of Notification Type Specifications
        1. Notification Type Specification is defined here to consist of:
            1. Unique Notification Name (a few words)
            2. The Notification Conditions which trigger the creation of a Notification Message
            3. Setting of the initial Notification Attributes
                1. Notification Content
                2. Notification Call To Action
                3. Notification Status
                4. Notification Delivery rules
                    1. In app only / email only / both in-app and email
            4. Notification Status Conditions - Conditions  which will determine the Status of an individual Notification Message.
                1. Notification Status might include such conditions as:  ‘unread’, ‘read’, ‘actioned’, ‘hidden’.
            5. Notification Contexts - in-app pages where the Notification should be present
    2. Future-proofing considerations to support later iterations (not for MVP):
        1. Notification Message can include images/icons
        2. Allow simple html text styling for Notification Content (perhaps through Markdown so that app text framework does not need to accommodate html)
5. _(as relevant) Increment to existing implementation_
*   Identify the existing implementation
*   Clarify the increment the BRD is intended to deliver
    1. 
6. _(as relevant) Increment to existing implementation_
    *   Current notification-related tickets: [#517](https://github.com/orgs/CredComSoc/projects/6/views/8?filterQuery=&pane=issue&itemId=76192196); [#1133](https://github.com/CredComSoc/cofi-app-llm/issues/1133); [#1134](https://github.com/orgs/CredComSoc/projects/6/views/8?filterQuery=&pane=issue&itemId=78724443).
7.

---

**Document Metadata:**
- **Created:** 2025-11-24
- **Sequence Number:** 29
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5975
