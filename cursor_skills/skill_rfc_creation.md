---
name: rfc-creation
description: AI skill to create high-quality RFC (Request for Comments) documents for citizen developers. Takes a paragraph or initial idea and builds a complete, structured RFC through clarifying questions. Must be called explicitly. Focuses on structure enforcement, content quality, and conciseness.
---

# RFC Creation Skill for Citizen Developers

## Purpose

This skill helps create complete, high-quality RFC (Request for Comments) documents for citizen developers at Vendasta. It transforms an initial idea or paragraph into a comprehensive 9-section RFC by asking clarifying questions and ensuring all technical requirements are documented clearly.

**This skill must be called explicitly. It is not automatic.**

## When to Use This Skill

Use this skill when:
- A user provides a problem statement or initial idea for technical work
- A user asks to "create an RFC" or "write an RFC"
- A user provides a rough outline and needs it structured as a formal RFC
- A user needs help completing a partially written RFC

## RFC Structure

Every RFC must include these 9 sections in this exact order:

### 1. Problem Statement
What problem are you solving? Why does it matter to users or the business?

**Quality criteria:**
- Identifies who is affected (users, teams, stakeholders)
- Quantifies impact (time, cost, errors, frequency)
- Makes the pain point concrete and specific
- No generic statements (avoid "improve efficiency" without specifics)

### 2. Context & Goals
What context does this work fit into? What are the measurable outcomes?

**Quality criteria:**
- Provides business or operational context
- States 2-4 specific, measurable goals
- Uses numbers when possible (time saved, errors reduced, users impacted)
- Avoids vague goals like "make it better"

### 3. Personas & User Stories
Who will use this? What do they need to do?

**Quality criteria:**
- Identifies 1-3 specific personas (roles, not individual names)
- Writes user stories in format: "As a [persona], I can [action] so that [benefit]"
- Focuses on user needs, not technical implementation
- Makes success clear from the user's perspective

### 4. User Flows
What is the step-by-step experience?

**Quality criteria:**
- Shows the complete flow from start to finish
- Includes what users see, do, and experience at each step
- Notes any decision points or branches
- Can be a numbered list or simple diagram description
- Written in plain language, not technical terms

### 5. Technical Requirements
What systems, data, and permissions are involved?

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

### 6. Implementation
How will the solution work at a high level?

**Quality criteria:**
- Describes the approach without writing code
- Clear enough that a reviewer can understand the flow
- Identifies key technical decisions or approaches
- Concrete, not vague (avoid "we'll figure it out later")

### 7. Alternatives Considered
What other approaches did you explore? Why did you choose this one?

**Quality criteria:**
- Lists 2-3 alternative approaches
- States why each was rejected or not chosen
- Shows you've thought through options
- Concise (one paragraph per alternative)

### 8. Risks and Dependencies
What could go wrong? What do you need from others?

**Quality criteria:**
- **Technical Risks** - Performance, security, failure modes, maintenance
- **Dependencies** - Other teams, platform features, infrastructure, approvals
- **Open Questions** - Things you're unsure about or need feedback on
- Honest and specific (this is maturity, not weakness)

### 9. Test Plan and Success Criteria
How will you validate this works? How will you measure success?

**Quality criteria:**
- **Test Plan** - Specific steps to verify the solution works
- **Success Criteria** - Measurable outcomes that prove success
- **Validation approach** - Manual testing, automated tests, user validation
- **Monitoring** - How you'll track it after deployment (if applicable)

## Process for Creating an RFC

When the user provides an initial idea or paragraph, follow this process:

### Step 1: Understand the Problem
Read the user's input carefully. Identify:
- What problem they're trying to solve
- What system or process is involved
- Who is affected
- What they've described so far

### Step 2: Ask Clarifying Questions
Before writing anything, ask questions to fill gaps. Focus on:
- **Problem clarity** - Who is affected? How often does this happen? What's the cost?
- **User impact** - Who will use this? What do they need to accomplish?
- **Technical details** - What systems are involved? What data is needed? What permissions?
- **Success measurement** - How will we know this worked? What changes?

**Ask 3-5 focused questions at a time. Wait for answers before proceeding.**

### Step 3: Build the RFC Section by Section
Once you have answers:
1. Draft sections 1-4 (user-focused sections) first
2. Draft sections 5-9 (technical sections) second
3. Present the complete RFC to the user
4. Ask if any sections need more detail or clarification

### Step 4: Validate Quality
Check the RFC against these criteria:
- [ ] All 9 sections are present and in order
- [ ] Section 5 (Technical Requirements) is explicit and detailed
- [ ] No AI slop (avoid "delve", "seamlessly", "robust", "leverage")
- [ ] No verbose writing (every word earns its place)
- [ ] Written for non-engineers (jargon explained or avoided)
- [ ] Concrete and specific (no vague statements)
- [ ] Honest about risks and open questions

### Step 5: Iterate if Needed
If the user requests changes:
- Ask clarifying questions about the changes
- Update specific sections
- Maintain the 9-section structure
- Revalidate quality

## Writing Quality Rules

### Conciseness
- Remove qualifiers like "very", "really", "quite"
- Cut introductory phrases ("It's important to note that...")
- One clear sentence beats three explanatory ones
- Get to the point immediately

### No AI Slop
Avoid these overused AI phrases:
- "delve into", "dive deep"
- "seamlessly integrate"
- "robust solution"
- "leverage"
- "utilize" (use "use")
- "cutting-edge", "state-of-the-art"
- "game-changer", "revolutionize"

### Write for Non-Engineers
- Avoid technical jargon or explain it immediately
- Use analogies when helpful
- Assume readers understand business problems, not technical implementation
- Ask: "Would someone from Sales understand this?"

### Be Concrete and Specific
**Good**: "Fetches sales data from 5 sheets, aggregates weekly totals, and delivers a formatted report every Monday at 6 AM"  
**Bad**: "Improves the reporting process to make it more efficient"

**Good**: "Reduces manual report generation time from 3 hours to 5 minutes"  
**Bad**: "Significantly speeds up reporting"

## Example Quality Check

### Good Technical Requirements Section
```markdown
## Technical Requirements

**Systems Accessed**:
- Google Sheets API (read-only)
- Gmail API (send email)
- Apps Script runtime

**Data Requirements**:
- Read: Weekly sales numbers (numeric), customer names (string), deal stages (enum)
- Write: Aggregated report in new sheet tab (formatted as table)
- No PII (Personally Identifiable Information) beyond customer company names

**Permissions**:
- Service account with Sheets API read access
- Gmail send-as permission for service account
- Script must run with user's authorization

**Input → Processing → Output**:
- Input: 5 Google Sheets with sales data, trigger from time-based scheduler
- Processing: Fetch rows, filter by date range, aggregate by region, format as table
- Output: New sheet tab with formatted report, email to 3 recipients with summary

**Integration Points**:
- Sheets API v4 for data fetching
- Gmail API for email delivery
- Apps Script timer for scheduling

**Limits and Expectations**:
- Sheets API quota: 500 requests/min (fetching 5 sheets = 5 requests, well under limit)
- Processing time: ~30 seconds for 1000 rows
- Email delivery: sent within 2 minutes of report completion
- Data volume: handles up to 10,000 rows per sheet
```

### Bad Technical Requirements Section (Too Vague)
```markdown
## Technical Requirements

We'll use Google Sheets and Gmail to automate the reporting process. The script will fetch data and send emails. It should be fast and reliable.
```

## Important Reminders

1. **This skill must be called explicitly** - It does not activate automatically
2. **Ask clarifying questions** - Don't guess or make assumptions
3. **Focus on Section 5** - Technical Requirements is the most critical section
4. **Be concise** - Remove all unnecessary words
5. **Write for non-engineers** - Avoid or explain technical jargon
6. **Be specific** - Use numbers, names, and concrete details
7. **Validate completeness** - Check all 9 sections before presenting

## References

- Full RFC guide: `docusaurus/docs/guides/atlassian/workflows/create-rfcs.md`
- Documentation standards: `.cursor/skills/citizen-developer-docs-standards/SKILL.md`
- Vendasta Citizen Developers: Non-engineering teams building automation and tooling

## Output Format

When presenting the completed RFC to the user, use this format:

```markdown
# [RFC Title]

## 1. Problem Statement
[Content]

## 2. Context & Goals
[Content]

## 3. Personas & User Stories
[Content]

## 4. User Flows
[Content]

## 5. Technical Requirements
[Content with Input→Processing→Output model]

## 6. Implementation
[Content]

## 7. Alternatives Considered
[Content]

## 8. Risks and Dependencies
[Content]

## 9. Test Plan and Success Criteria
[Content]
```

## Success Criteria for This Skill

An RFC created by this skill is successful when:
- All 9 sections are present and complete
- Section 5 (Technical Requirements) is detailed and explicit
- A technical reviewer can understand what's being built
- A stakeholder can understand the user impact
- The RFC is concise with no AI slop
- Open questions and risks are called out honestly
- The user confirms the RFC accurately represents their intent

