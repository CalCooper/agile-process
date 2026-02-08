> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# RFC: Updating Operating Model
**Submitted by:** Jordan Watson (Sales)  
**Impact Score:** 4 | **Scale:** Workflow | **Frequency:** Monthly | **Weekly Hours:** 24 | **Annual Hours Savings:** 1,248

## 1. Problem Statement
The Operating Model spreadsheet is updated monthly with actual results. Numbers are pulled from varying Looker sources and translated into the format required by the Operating Model. People are the bridge: manual copy-paste and reformatting between Looker and Google Sheets. The steps to pull exact data (e.g., filters for bookings) change over time and that knowledge is often hidden. Not enough time is left for analysis because of the maintenance overhead.
**Who is affected:** Sales/Finance/Ops teams that own or consume the Operating Model; leadership that uses it for planning and reporting.
**Impact:** 24 hours/week spent on updating the model (1,248 hours/year). Monthly process. Knowledge about data sources and filters lives in people’s heads; when it’s wrong or outdated, the model is wrong. Reduces time available for actual analysis.

## 2. Context & Goals
**Context:** The Operating Model is a key planning and reporting artifact. It depends on multiple Looker sources and a specific spreadsheet structure. Keeping it current is manual and brittle.
**Goals:**
1. Translate numbers from varying Looker sources into the format that fits the Operating Model spreadsheet automatically.
2. Reduce manual update time from 24 hours/week to [PLACEHOLDER: target].
3. Free time for analysis instead of data movement and formatting.
4. Document or automate “how we pull exact data” so knowledge is not lost. Annual savings: 1,248 hours.

## 3. Personas & User Stories
- As a **Sales Ops or Finance Analyst**, I can run an automated refresh of the Operating Model from Looker so that I spend time on analysis, not on copy-paste.
- As a **Consumer of the Operating Model**, I can trust that the numbers are current and sourced correctly so that I can make decisions.
- As a **Model Owner**, I can change or add Looker sources in one place so that the refresh still works without tribal knowledge.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
**Current state:** People pull data from multiple Looker reports/dashboards, apply filters (e.g., for bookings), copy into the Operating Model spreadsheet, and format. Steps evolve as requirements change; knowledge is partly documented, partly in people’s heads.
**Target state:**
1. [PLACEHOLDER: Trigger – schedule or manual – to refresh Operating Model.]
2. System reads from defined Looker sources with defined filters.
3. Data is transformed to match the Operating Model sheet layout.
4. Spreadsheet is updated (or a new version generated).
5. [PLACEHOLDER: Notifications, versioning, or review step.]
6. Analysts use the updated model for analysis and reporting.

## 5. Technical Requirements
**Systems Accessed:**
- Looker (multiple reports/sources)
- Google Sheets (Operating Model spreadsheet)
**Data Requirements:**
- Read: Defined Looker explores/reports/dashboards; filters (e.g., date range, bookings) as configured.
- Write: Operating Model sheet – specific tabs/cells with numeric and formatted data.
- Transform: Looker result set → layout and format required by the Operating Model.
**Permissions:**
- [PLACEHOLDER: Looker API or embed credentials; Sheets API write access to Operating Model.]
**Input → Processing → Output:**
- Input: Looker report IDs or queries; filter parameters; schedule or manual trigger.
- Processing: Call Looker API, apply filters, map fields to Operating Model layout, format (e.g., numbers, dates).
- Output: Updated Operating Model spreadsheet (or new sheet/version).
**Integration Points:** Looker API (or scheduled exports) → automation (e.g., Apps Script, middleware) → Google Sheets API.
**Limits and Expectations:** [PLACEHOLDER: Looker API quotas; sheet size and refresh time; how often filters/sources change.]

## 6. Implementation
[PLACEHOLDER: High-level approach – e.g., Apps Script vs external service; how Looker sources and filters are configured (config table vs code); versioning and rollback if refresh is wrong.]

## 7. Alternatives Considered
[PLACEHOLDER: Keep manual process; automate only some sources; build the Operating Model inside Looker instead of Sheets.]

## 8. Risks and Dependencies
**Risks:** Looker schema or report changes can break the refresh; filter logic must be documented and maintained. Some pieces are documented, not all – remaining knowledge needs to be captured.
**Dependencies:** Looker and Google Sheets access; documentation of current “pull steps” and filter logic. Knowledge gap: document remaining steps and filters before full automation.
**Open Questions:** [PLACEHOLDER: Exact Looker report IDs and filter set; who approves changes to sources or layout; refresh SLA.]

## 9. Test Plan and Success Criteria
**Success Criteria:** Operating Model updated from Looker on schedule; 1,248 hours/year saved; no increase in errors; more time for analysis.
**Test Plan:** [PLACEHOLDER: Compare automated output to manual run for one month; validate key numbers; pilot with one consumer group.]
**Validation:** [PLACEHOLDER: Monthly check of refresh success and number sanity; quarterly hours-saved validation.]