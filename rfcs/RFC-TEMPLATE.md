> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# [RFC Title]
> **Instructions:** Replace bracketed text with your content. Every RFC must include these 9 sections in this exact order. Use placeholders where information is missing.

## 1. Problem Statement
**What problem are you solving? Why does it matter to users or the business?**
**Quality criteria:**
- Identify who is affected (users, teams, stakeholders)
- Quantify impact (time, cost, errors, frequency)
- Make the pain point concrete and specific
- Avoid generic statements (e.g., "improve efficiency" without specifics)
**Example:** "Finance spends 20 hours/week manually copying AR data from Premium reports into the platform. Errors in copy-paste cause 2-3 billing disputes per month. The process runs daily and blocks collections until complete."

## 2. Context & Goals
**What context does this work fit into? What are the measurable outcomes?**
**Quality criteria:**
- Provide business or operational context
- State 2-4 specific, measurable goals
- Use numbers when possible (time saved, errors reduced, users impacted)
- Avoid vague goals like "make it better"
**Example:**
- Reduce manual data entry from 20 hours/week to under 1 hour/week
- Eliminate copy-paste errors that cause billing disputes
- Free Finance team to focus on exception handling and analysis

## 3. Personas & User Stories
**Who will use this? What do they need to do?**
**Quality criteria:**
- Identify 1-3 specific personas (roles, not individual names)
- Write user stories in format: "As a [persona], I can [action] so that [benefit]"
- Focus on user needs, not technical implementation
- Make success clear from the user's perspective
**Example:**
- As a Finance Analyst, I can run the AR sync with one click so that I don't spend hours copying data between systems.
- As a Billing Manager, I can see when the sync last ran and any errors so that I can trust the data before running collections.

## 4. User Flows
**What is the step-by-step experience?**
**Quality criteria:**
- Show the complete flow from start to finish
- Include what users see, do, and experience at each step
- Note any decision points or branches
- Can be a numbered list or simple diagram description
- Written in plain language, not technical terms
**Example:**
1. User opens the automation dashboard and sees last sync time and status.
2. User clicks "Run sync" (or sync runs on schedule).
3. System fetches data from Source A and transforms it.
4. System writes to Destination B and shows success or error count.
5. If errors: user sees list of failed rows and can retry or fix manually.

## 5. Technical Requirements
**What systems, data, and permissions are involved?**
**Quality criteria (CRITICAL - this section must be explicit):**
- **Systems accessed or modified** - List every system, API, or service touched
- **Data requirements** - What data is read, written, or transformed
- **Permissions needed** - Service accounts, API keys, access levels
- **Input/Output model** - What goes in, what happens, what comes out
- **Integration points** - How this connects to other systems
- **Limits and expectations** - Quotas, rate limits, response times, data volume
**Use the Input → Processing → Output model:**
```
Input: [What data/triggers start this?]
Processing: [What happens to that data?]
Output: [What's the result?]
```
**Template:**
**Systems Accessed:**
- [List each system, API, or service]
**Data Requirements:**
- Read: [What data is read, from where]
- Write: [What data is written, to where]
- Transform: [What transformations occur]
- PII/Sensitivity: [Any restrictions]
**Permissions:**
- [Service accounts, API keys, access levels]
**Input → Processing → Output:**
- Input: [Triggers and source data]
- Processing: [Steps applied to the data]
- Output: [Resulting artifacts, notifications, updates]
**Integration Points:**
- [How this connects to other systems]
**Limits and Expectations:**
- [Quotas, rate limits, response times, data volume]

## 6. Implementation
**How will the solution work at a high level?**
**Quality criteria:**
- Describe the approach without writing code
- Clear enough that a reviewer can understand the flow
- Identify key technical decisions or approaches
- Concrete, not vague (avoid "we'll figure it out later")
**Example:** "An Apps Script runs on a time-based trigger (e.g., daily at 6 AM). It reads from Sheet A via the Sheets API, filters rows by date, aggregates by region, and writes the result to a new tab in Sheet B. It then calls the Gmail API to send a summary email to the Finance distribution list. Error handling: on failure, the script logs to a dedicated error sheet and sends an alert to the script owner."

## 7. Alternatives Considered
**What other approaches did you explore? Why did you choose this one?**
**Quality criteria:**
- List 2-3 alternative approaches
- State why each was rejected or not chosen
- Show you've thought through options
- Concise (one paragraph per alternative)
**Example:**
- **Manual process with AI assistance:** Would reduce time but still require copying between systems; rejected because it doesn't remove the coordination burden.
- **Separate tool per team:** Each team builds their own automation; rejected because it duplicates logic and misses integration opportunities.
- **Third-party vendor:** Rejected because [cost, lock-in, or integration gaps].

## 8. Risks and Dependencies
**What could go wrong? What do you need from others?**
**Quality criteria:**
- **Technical Risks** - Performance, security, failure modes, maintenance
- **Dependencies** - Other teams, platform features, infrastructure, approvals
- **Open Questions** - Things you're unsure about or need feedback on
- Honest and specific (this is maturity, not weakness)
**Template:**
**Technical Risks:**
- [List risks]
**Dependencies:**
- [Other teams, approvals, infrastructure]
**Open Questions:**
- [Unresolved items]

## 9. Test Plan and Success Criteria
**How will you validate this works? How will you measure success?**
**Quality criteria:**
- **Test Plan** - Specific steps to verify the solution works
- **Success Criteria** - Measurable outcomes that prove success
- **Validation approach** - Manual testing, automated tests, user validation
- **Monitoring** - How you'll track it after deployment (if applicable)
**Template:**
**Test Plan:**
1. [Step 1]
2. [Step 2]
3. [Step 3]
**Success Criteria:**
- [Measurable outcome 1]
- [Measurable outcome 2]
**Validation Approach:**
- [How you'll validate]
**Monitoring:**
- [How you'll track after deployment]

## Validation Checklist
Before submitting the RFC, verify:
- [ ] All 9 sections are present and in order
- [ ] Section 5 (Technical Requirements) is explicit and detailed
- [ ] No AI slop ("delve", "seamlessly", "robust", "leverage")
- [ ] Written for non-engineer readability
- [ ] Concrete and specific (no vague statements)
- [ ] Open questions and risks are called out
- [ ] Placeholders used where information is missing