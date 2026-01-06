# Logging

**Sequence:** 14  
**Source:** MVP Requirements / Logging  
**ClickUp Page ID:** 8cp80ab-5035  
**Last Updated:** 2025-11-24  
**Tags:** 

---

**Logging Plan**
*   Review existing logging implementation.
*   Prepare documentation and proposed action plan for review.
    *   **Considerations**: As per [Logging requirement](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-6b1fe0f1-ac93-43b7-becc-abe3cc7e7900) : App-wide logging framework in place to support consistent and unified methods for bug-tracing, attack tracing, key system and user actions, auditing.
    *   There may be ‘off-the peg’ logging libraries and/or services which provide near or similar functionality - these should be investigated for cost/benefit as part of the Logging spike

**Spike notes**

Result of this spike should be a simple document which can become the documented Requirement.
### From discussion with Yani, it seems as if many aspects of this document are already implemented. The spike report can thus be structured as:
1. what is being done at the moment (including a list of all existing logging calls)
2. Increments to be included in the doscumented Requirement
### A Structured Logging system is required, which allows a logging function to be placed at any point in the code, to log arbitrary relevant data as required.
1. _Logs may be required/used for any or all of: bug-tracing, attack tracing, key system and user actions, auditing. In order for this system to be useful it must be possible to query. Large numbers of log entries will be involved; thus log entries must at the same time be well structured and capable of handling arbitrary  data with full discoverability. Cross-reference and correlation with Analytics should be considered. The system needs to be able to:_
    1. Operate as a simple function call
    2. documentation:
        1. Logs and log entries should, as far as practical, be self-documenting and human-readable (semantic log type naming)
        2. A simple document listing all log function calls; stating workflow, page, code location and what is documented should be easy to maintain and update (could there be a script operating over the code to surface these?)
        3. 
    3. Logs and entries should be structured to facilitate rapid searching across very large numbers of entries
        1. This structure should be designed to allow for later development of a log query/analysis system - out of MVP scope.
    4. Log backups are to be:
        1. triggered on a volume, rather than a cron basis, 
        2. independent of main app backup for resilience.
    5. WHY: 
        1. the Local Loop Service will handle large amounts of sensitive commercial data, and the outcomes will affect company financial viability. Users have multiple opportunities to interact with their data. It is highly likely that results will be queried at some point by users. Users might initiate legal action against the company, or against each other, concerning payments. It must be possible for the company to provide - for example - the full history of any particular invoice.
        2. The data Local Loop collects as to User behaviour will only partially be collected through standard analytics services. Local Loop specific user behaviours which are useful to us in development of the Service may need to be captured through Logging.
    6. WHAT: The Logging System will consist of a Logging Function which will write Log Entries to a Log Storage System. 
        1. Log Entries will in all cases be particular instances of a defined Log Entry Type
        2. It must be possible to define new Log Entry Types
        3. There must be a Log Entry Types generic framework onto which Log Entry Types are specified.
        4. There will be a configurable system which manages the Log Storage System and the  Log Entry Types Storage System for access and backups.
    7. HOW: 
        1. Requirements will call for Logging in many cases
        2. The technical team should also raise - in documented form - their own Logging requirements.
        3. Implementation for a Logging requirement should be straightforward - the requirements for Log Entry Types will ensure consistency and available documentation.
        4. For MVP, logging access will not have any accessible admin functionality.
2. _(as relevant) Candidate acceptance Criteria_
    1. Provide a list of
3. _(as relevant) Candidate solution material_ 
    1. (see Logging Spike) There may be ‘off-the peg’ logging libraries or services or design methods  which provide near or similar functionality - these should be investigated as part of the Logging spike. A ‘tried-and tested’ solution with a community seems desirable - but requirements match will need to be considered.
    2. It may be useful to use a parallel approach to static site content files to allow for different log types, so that the meta-structure for a log entry type might look like this:
        1.     1. Standard required log data---:--- eg Timestamp etc
            2. Structured key:data elements in eg YAML format---:---eg Entry Type: <_File Upload_\> User:<_account_\>
            3. Unstructured data if needed---:---One data blob only - the ‘payload’
        2. This would allow a future log query/analysis system to rapidly parse a large log file and extract relevant subsets as structured data.
4. _(as relevant) Increment to existing implementation_
    *   The existing implementation is undocumented, so increments are unclear.
5. _(as relevant) Background/reference material_
*   [Structured Logging](https://middleware.io/blog/what-is-structured-logging/).
*   Notes from Invoice Data Processing:
    *   Review activity logging with Dil & Mohammed: see notes from 1st June
        *   Interspersed amongst steps, then compile.
        *   Consider capturing workflow
        *   Doc for logging actions directory?

Additional notes:
*   Review activity logging with Dil & Mohammed: see notes from 1st June
    *   Interspersed amongst steps, then compile.
    *   Consider capturing workflow
    *   Doc for logging actions directory?

---

**Document Metadata:**
- **Created:** 2025-07-16
- **Sequence Number:** 14
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5035
