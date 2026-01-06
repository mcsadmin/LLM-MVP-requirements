# General UI/UX

**Sequence:** 17  
**Source:** MVP Requirements / General UI/UX  
**ClickUp Page ID:** 8cp80ab-6235  
**Last Updated:** 2025-11-25  
**Tags:** 

---

# 1\. General UI/UX
**Notes on Components Framework**
1. **Headline Requirement:** Component framework in place to make UI elements and behaviours consistent across the app, with minimal effort to implement and maintain. Framework should be selected and implemented so that these elements are standards based, straightforward, easy to manage, adaptable and extensible.
    1. UI Component Library to be selected with regard to provision of standard components to meet majority of app requirements, and allow necessary customisation without 'breaking' the approach.
    2. Must work for mobile and desktop, using the most common browsers.
    3. Must address existing issues with inconsistent styling and/or behaviour across these elements:
        1. Loading states and associated spinners (ensuring that spinners persist in line with loading states - see ticket [#1005](https://github.com/CredComSoc/cofi-app-llm/issues/1005))
            1. Noted as needed individual implementation in each instance - for thorough review.
        2. 'Success' and 'error' messages styling and placement.
            1. Patchy implementation - needs to be thoroughly reviewed, designed, and implemented across all pages, modals etc.
        3. 'Success' and 'error' message persistence.
            1. Patchy implementation - needs to be thoroughly reviewed, designed, and implemented across all pages, modals etc.
        4. Button disable/grey-out when requirements to use not met.
            1. Patchy implementation - needs to be thoroughly reviewed, designed, and implemented across all pages, modals etc.
        5. Auto-populate form fields where useful and appropriate.
            1. Patchy implementation - needs to be thoroughly reviewed and implemented across all pages, modals etc.
                1. Already implemented in auth version of Contact Us form, could usefully be implemented in Password Reset flow (for both instances where resending reset links is possible), and probably elsewhere.
        6. Button size and styling.
        7. 'x' button to clear Org Name field in all relevant forms (see ticket [#710](https://github.com/CredComSoc/cofi-app-llm/issues/710)).
        8. Font sizes.
            1. Needs thorough review across app.
            2. Seems quite small on mobile.
        9. Brand fonts.
            1. Needs thorough review and implementation.
        10. Highlighting entered text in bold in all form field autocompletes.
            1. Needs thorough review and implementation.
        11. Field labelling texts.
            1. Needs thorough review and implementation.
        12. Field placeholder texts.
            1. Needs thorough review and implementation.
        13. Validity checks on email addresses (string@domain.extension format) in form fields:
            1. Needs thorough review and implementation.
        14. Validity checks on other form field field values.
            1. Needs thorough review, specification, and implementation.
        15. Modals styling.
            1. Needs thorough review and implementation.
        16. Fit to screen on desktop for all app pages
        17. Fit to screen on mobile for all app pages
        18. . All pages, modals, menus etc. match designs.

# UI/UX Standards Requirements (ticket for designer) #ClientUsers
### 1\. To ensure the application delivers a consistently high-quality user experience, the development team must adopt and commit to a clearly defined set of usability and UI/UX standards, with accompanying assessment tools and measurable achievement targets.
1. WHY: The application includes a multi-stage workflow involving interaction with and dependency upon actions from other users. This complexity increases the need for simplicity, clarity, and consistency in the user interface and user experience. A core success factor is that Client Users find the app intuitive and easy to navigate. Without this, engagement with the more complex workflow will be significantly impaired.
2. WHAT: Detailed Requirements:
    1. Standards Selection
        1. The developer must select and document a small, focused set of relevant UI/UX and usability standards (e.g., WCAG, Nielsen Norman heuristics, ISO 9241).
        2. Standards should be widely recognized, current, and appropriate to the app’s context and user base.
    2. Assessment Tools & Methods
        1. For each selected standard, one or more published assessment tools or scoring methodologies must be identified (e.g., System Usability Scale \[SUS\], WCAG compliance checkers, heuristic evaluation methods).
        2. These tools should support objective evaluation of the application during development and at key milestones.
    3. Target Achievement Levels
        1. Clear target scores or achievement levels must be defined and agreed upon (e.g., “SUS score ≥ 80,” “WCAG 2.1 Level AA compliance”).
        2. These targets should be achievable but ambitious enough to drive high-quality outcomes.
    4. Application Coverage
        1. Standards and assessment must be applied to all aspects of the application that affect the user experience, including:
            1. Navigation and workflow
            2. Visual design and responsiveness
            3. Accessibility
            4. User feedback and system messaging
            5. Onboarding and help resources
    5. Consistency of application:
        1. The selected standards must be applied consistently across the entire application, with particular attention to areas where multiple features or user journeys intersect.
    6. Inconsistencies should be tracked and addressed during design reviews and testing phases.

**Dil's notes on 'system holds users'**
#### The app must catch all exceptions, service dropouts, unexpected occurrences within an LLM framework
LLM is a financial app. Users must trust the LLM app to manage their money well. Appearances of non LLM-framed error screens undermine trust.
#### (as relevant) Candidate acceptance Criteria
As far as is practical, there are no 'uncaught' error conditions.
Generic LLM framed 'Something went wrong' pages are acceptable.
Ensure that server crash errors (for example) aren't shown to client users - need a catch-all with friendlier messages/behaviour.
#### (as relevant) Candidate solution material 
Develop a framework which supports working both 'upward' and 'downward'.
'upward' from baseline 'unknown error' pages
'downward' from specific workflow condition 'catches'
This will allow design and testing efforts to push 'downward' with requests for specific catches, in confidence that no catchable condition will ever 'fall out' of the LLM user experience.

---

**Document Metadata:**
- **Created:** 2025-11-24
- **Sequence Number:** 17
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-6235
