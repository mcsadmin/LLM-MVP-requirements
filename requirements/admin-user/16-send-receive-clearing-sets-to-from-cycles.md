# Send & Receive Clearing Sets to/from Cycles

**Sequence:** 16  
**Source:** MVP Requirements / Send & Receive Clearing Sets to/from Cycles #AdminUser  
**ClickUp Page ID:** 8cp80ab-5855  
**Last Updated:** 2025-11-24  
**Tags:** #AdminUser #Clearing

---

# 1\. Send & Receive Clearing Sets to/from Cycles
### 1\. Clearing Sets need to be delivered to Cycles team for analysis
1. WHAT:
    1. Admin User can immediately and securely share the [Clearing Set](../../requirements/admin-user/18-admin-user-interface.md?block=block-ed049ab3-0265-4606-8b94-139203a8886e) for current [Clearing Cycle](../../requirements/system-functions/12-clearing-cycle.md) with the Cycles team via a shared Proton Drive folder.
    2. Include any additional information as agreed with the Cycles team to allow verification of the results data (for example the 'run UUID').
        1. tbc
    3. Admin User can notify Cycles team that there is a Clearing Set that needs analysing.
### 2\. After analysis, the Cycles team needs to return the results to us
1. WHAT:
    1. Cycles can immediately and securely share clearing results with the Admin User via a shared Proton Drive folder.
        1. Results should be in same format as Clearing Set
    2. Include any additional information as agreed with the Cycles team to allow verification of the results data (for example the 'run UUID').
        1. tbc
    3. Cycles can notify Admin User that analysis is available.

### 10\. Post-MVP notes
*   **Encryption**
    1. **Headline Requirement:** A Clearing Dataset, once created, needs to be suitably encrypted
        1. Load [Clearing Dataset](https://app.clickup.com/9015918923/v/dc/8cp80ab-3035/8cp80ab-1355?block=block-1ab8231d-810c-4cee-a961-e7a6766e4f53).
        2. Verify by comparing published hash with computed hash.
        3. Encrypt node/organisation identities differently for each run.
            1. Possible approach: Use the 'run hash' as a salt to an encryption process to transform the two Organisation UUID elements of each row of data (note that there will likely be many instances of most Organisation UUIDs - occurring in both Debtor and Creditor position, so that encryption need be carried out only once per unique Organisation UUID).
*   **Verification**
    *   Possible to create a hash from data object for verification use
        *   (could the hash be used as the key for the database row - as an analogue of 'content addressable hash'? See [https://en.wikipedia.org/wiki/Content-addressable\_storage](https://en.wikipedia.org/wiki/Content-addressable_storage))
*   **Automation**:
    *   Raise failure mode analysis & pre-emption with Dil & Tomaž
    *   Cycles team are intending to create an API.
    *   See other MVP requirements, also consult with Tomaž and Majita
*   **Clearing Process Run Control**
    *   **Headline Requirement:** Clearing runs take place at times specified by Admin User, and consist of a sequence of operations which must all be completed on the basis of verifiable data integrity for a clearing run to have been completed. All stages should be stored for audit purposes. **Reliable Traceable Reproducible Able to report any errors**
        1. A control process is needed which:
            1. Covers all stages of the sequence.
            2. initiates the sequence, each run to be allocated:
                1.     1. an UUID identifier, which will be a key to:
                        1. a string identifying the software instance (like "LLM-dev-deployID, "LLM-prod
                            1. Here 'instance name" will be "LLM"
                            2. Sequence number will a simple incremented integer.
                        2. <timestamp> - initiation time.
                    2. String, sequence number and timestamp will be used to form an appropriate 'Run Display Name' for Admin use.
            3. verifies that each stage has been completed successfully,
            4. checks that the data involved at each stage is verifiably derived solely and completely from the data of the previous stage.
            5. Maintains a 'state' record of each run.
        2. The whole process should be logged along with the verification results. Each stage of the data should be retained as it was delivered to the next stage. This includes failed/incomplete runs.

---

**Document Metadata:**
- **Created:** 2025-10-28
- **Sequence Number:** 16
- **Source System:** ClickUp
- **Workspace ID:** 9015918923
- **Doc ID:** 8cp80ab-3995
- **Page ID:** 8cp80ab-5855
