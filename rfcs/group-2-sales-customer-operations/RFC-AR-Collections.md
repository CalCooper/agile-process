> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# RFC: AR Collections
**Submitted by:** Mitch Hymers (Finance & Admin)  
**Impact Score:** 5 | **Scale:** Workflow | **Frequency:** Daily | **Weekly Hours:** 20 | **Annual Hours Savings:** 1,040

## 1. Problem Statement
AR Collections work for various internal PIDs is done manually. The process relies on knowledge that lives in people's heads rather than in documented artifacts. When people change roles, that knowledge is at risk. Some documentation exists but would need to be improved before automation.
**Who is affected:** Finance & Admin (AR/collections team), internal PIDs that depend on timely collections.
**Impact:** 20 hours/week spent on AR collections work; 1,040 hours/year that could be saved. Process runs daily. Knowledge gap blocks automation until a durable artifact exists.

## 2. Context & Goals
**Context:** AR collections are critical for cash flow and partner billing. Today an AI employee could perform this work if the process were documented and systems were integrated.
**Goals:**
1. AR Collections work completed by an AI employee for our various internal PIDs.
2. Reduce manual AR work from 20 hours/week to [PLACEHOLDER: target].
3. Create or improve documentation so knowledge is not lost when people move roles.
4. Annual savings: 1,040 hours (validated quarterly).

## 3. Personas & User Stories
- As a **Finance Analyst**, I can have AR collections run by an AI employee so that I focus on exceptions and edge cases instead of routine work.
- As a **Collections Manager**, I can rely on documented, repeatable process so that turnover does not create knowledge gaps.
- As an **internal PID owner**, I can have collections completed consistently and on time so that my account stays in good standing.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
[PLACEHOLDER: Map current manual steps from Premium reports and Kixie through to platform; then define target flow with AI employee.]
**Current state (high level):** Knowledge is hidden; process uses Premium reports, Kixie, and platform. Exact steps need to be documented as part of knowledge capture.

## 5. Technical Requirements
**Systems Accessed:**
- Premium reports (source of AR data)
- Kixie (calling/communications)
- Platform (collections workflow, internal PIDs)
**Data Requirements:**
- Read: [PLACEHOLDER: AR data from Premium reports; PID/account data from platform.]
- Write: [PLACEHOLDER: Collections status, call outcomes, next steps in platform.]
- Transform: [PLACEHOLDER: Raw report data → actionable collections queue.]
**Permissions:**
- [PLACEHOLDER: Service account or user access to Premium reports, Kixie, platform.]
**Input → Processing → Output:**
- Input: [PLACEHOLDER: Premium report exports or API; schedule or trigger.]
- Processing: [PLACEHOLDER: Identify overdue/at-risk PIDs; queue outreach; record outcomes.]
- Output: [PLACEHOLDER: Updated collections status in platform; logged calls in Kixie; reports.]
**Integration Points:** [PLACEHOLDER: How Premium reports, Kixie, and platform connect.]
**Limits and Expectations:** [PLACEHOLDER: Volume of PIDs, call volume, API quotas.]

## 6. Implementation
[PLACEHOLDER: High-level approach – e.g., automated pull from Premium reports, rules-based or AI-driven prioritization, integration with Kixie and platform for outreach and status updates. Document current process first to close knowledge gap.]

## 7. Alternatives Considered
[PLACEHOLDER: e.g., keep manual process; automate only reporting; outsource collections.]

## 8. Risks and Dependencies
**Risks:** Knowledge is currently in people's heads; automation depends on creating or improving documentation first. Some documentation exists but is incomplete.
**Dependencies:** Access to Premium reports, Kixie, and platform; participation from current AR owners to document process; [PLACEHOLDER: any approvals.]
**Open Questions:** [PLACEHOLDER: Exact data format from Premium reports; platform API capabilities; Kixie integration options.]

## 9. Test Plan and Success Criteria
**Success Criteria:** AR collections work completed by AI employee for internal PIDs; 1,040 hours/year saved; no increase in disputes or delays.
**Test Plan:** [PLACEHOLDER: Pilot with subset of PIDs; compare outcomes to manual baseline.]
**Validation:** [PLACEHOLDER: Weekly review of AI-collections outcomes; quarterly hours-saved validation.]