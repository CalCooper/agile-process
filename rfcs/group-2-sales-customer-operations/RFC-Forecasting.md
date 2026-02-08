> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# RFC: Forecasting
**Submitted by:** Tiffany Pennycook (Sales)  
**Impact Score:** 5 | **Scale:** Workflow | **Frequency:** Weekly  
**Weekly Hours:** [Unknown – new process; past forecasting took ~12 hours/week]

## 1. Problem Statement
Sales is not doing formal forecasting today but needs to build it out for 2026. Past forecasting methods took around a dozen hours per week and were largely subjective. The goal is to move to AI-supported predictive revenue models: close likelihood, forecast variance, and scenario planning instead of subjective judgment.
**Who is affected:** Sales leadership, Finance (for revenue planning), Exec team (for board and strategy).
**Impact:** High impact (score 5). Without forecasting, revenue planning and pipeline management are reactive. Building this will require data, models, and process; time savings and accuracy are to be defined.

## 2. Context & Goals
**Context:** Reliable forecasting supports revenue planning, resource allocation, and executive reporting. Current state: no structured forecasting process; historical approach was manual and time-consuming.
**Goals:**
1. AI predictive revenue models to project close likelihood, forecast variance, and enable scenario planning.
2. Move away from purely subjective forecasting.
3. [PLACEHOLDER: Target hours per week for forecasting process.]
4. [PLACEHOLDER: Target accuracy or variance metrics.]

## 3. Personas & User Stories
- As a **Sales Leader**, I can see AI-generated close likelihood and forecast variance so that I can plan capacity and report to execs with confidence.
- As a **Finance** user, I can consume forecast outputs for revenue planning so that we align on pipeline and commit.
- As an **AE**, I can see how my pipeline contributes to forecast and what’s at risk so that I can prioritize.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
**Current state:** No formal forecasting; historically manual, ~12 hours/week when done.
**Target state:**
1. [PLACEHOLDER: Data pulled from CRM/Looker/sheets on a schedule.]
2. [PLACEHOLDER: Model runs (close probability, scenarios).]
3. [PLACEHOLDER: Outputs: forecast report, variance view, scenario comparison.]
4. [PLACEHOLDER: Review and override by Sales/Finance where needed.]
5. [PLACEHOLDER: Distribution to leadership.]

## 5. Technical Requirements
**Systems Accessed:**
- Google Sheets (today’s ad-hoc use)
- Looker (revenue/pipeline data)
- CRM (pipeline, stages, history)
**Data Requirements:**
- Read: Pipeline data (stage, value, age, history), closed-won/lost outcomes, [PLACEHOLDER: external signals if any.]
- Write: Forecast outputs (sheets, Looker, or BI); [PLACEHOLDER: scenario tables.]
- Transform: Pipeline + history → close probability; scenarios → variance and scenarios.
**Permissions:**
- [PLACEHOLDER: Read access to CRM and Looker; write access to forecast output location.]
**Input → Processing → Output:**
- Input: Pipeline and historical close data from CRM/Looker; [PLACEHOLDER: trigger schedule.]
- Processing: Train or run model for close likelihood; compute forecast and variance; generate scenarios.
- Output: Forecast report; variance view; scenario comparison; [PLACEHOLDER: format and audience.]
**Integration Points:** CRM, Looker, Sheets (or replacement). Spreadsheet template exists for structured output; some knowledge still in people’s heads – document for 2026 build.
**Limits and Expectations:** [PLACEHOLDER: Data volume, refresh frequency, model ownership.]

## 6. Implementation
[PLACEHOLDER: High-level approach – e.g., Looker + embedded model vs separate forecasting service; how scenarios are defined; review and override workflow; rollout for 2026.]

## 7. Alternatives Considered
[PLACEHOLDER: Continue subjective forecasting; buy third-party forecasting tool; build lightweight model in sheets vs dedicated platform.]

## 8. Risks and Dependencies
**Risks:** Model accuracy may be poor initially; data quality in CRM affects results; scope creep if “forecasting” expands to many use cases.
**Dependencies:** CRM and Looker data access; spreadsheet template for output format; documentation of current (historical) process and desired metrics. Knowledge gap: some process in people’s heads – capture before full build.
**Open Questions:** [PLACEHOLDER: Who owns model and refresh; how scenarios are defined; approval chain for forecast submission.]

## 9. Test Plan and Success Criteria
**Success Criteria:** Forecast and variance produced on a defined schedule; scenario planning available; [PLACEHOLDER: accuracy target]; reduction in manual forecasting hours.
**Test Plan:** [PLACEHOLDER: Backtest on historical data; pilot with one segment; compare to actuals over 1–2 quarters.]
**Validation:** [PLACEHOLDER: Monthly or quarterly accuracy review; stakeholder adoption.]