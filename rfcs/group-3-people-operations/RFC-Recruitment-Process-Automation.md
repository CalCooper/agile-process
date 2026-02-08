> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# RFC: Recruitment Process Automation
**Submitted by:** Natasha Cooke (People Operations)  
**Impact Score:** 4 | **Scale:** System | **Frequency:** Daily | **Weekly Hours:** 40 | **Annual Hours Savings:** 2,080

## 1. Problem Statement
Recruitment today involves multiple manual steps: blocking interviews on Google Calendar, creating job postings after job description approval, creating interview guides manually every time (Chat GPT helps but there is no system that breaks down each step), using Gemini for cleaned-up transcripts and automatic scoring rubrics, resume parsing, and updating the ATS. There is no single dashboard for recruitment summary; Global Hiring Lifeline is not automated. The process runs daily and consumes 40 hours/week (2,080 hours/year).
**Who is affected:** People Operations (recruiters, coordinators), hiring managers, candidates.
**Impact:** 40 hours/week across recruitment tasks; 2,080 hours/year that could be reduced. Scale: System – automation would touch calendar, job postings, interview guides, transcripts, scoring, resume screening, and reporting.

## 2. Context & Goals
**Context:** Talent density and speed of hire depend on efficient recruitment. Today the process is fragmented across Google Sheets, Bamboo, and Calendar with heavy manual coordination.
**Goals:**
1. Block interviews on Google Calendar automatically (or from a single trigger).
2. Create job postings after job description approval without manual copy-paste.
3. Create interview guides from a system that breaks down each step and produces a solution (not just ad-hoc ChatGPT).
4. Use Gemini (or equivalent) to provide cleaned-up transcripts and automatic scoring rubrics based on templates.
5. Resume parsing: structured extraction from resumes into ATS/tracker.
6. Skills builder on ATS: auto-screen internal and external candidates and share most suited candidates for the role.
7. Automate Global Hiring Lifeline to create one dashboard for recruitment summary and dashboard.
8. Annual savings: 2,080 hours; single source of truth for recruitment status.

## 3. Personas & User Stories
- As a **Recruiter**, I can have interviews blocked on Calendar and job postings created from approved JDs so that I focus on candidate engagement and hiring manager alignment.
- As a **Recruiter**, I can get cleaned-up transcripts and scoring rubrics from interview recordings so that I don’t manually transcribe and score.
- As a **Hiring Manager**, I can see a shortlist of candidates ranked by fit (skills builder) so that I spend time on interviews, not screening.
- As a **People Ops Lead**, I can see one recruitment dashboard (Global Hiring Lifeline) so that I have a single view of pipeline and activity.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
**Current state (high level):**
- Calendar: Manual blocking of interview slots.
- Job postings: Created manually after JD approval.
- Interview guides: Created manually each time; ChatGPT used ad hoc.
- Transcripts/scoring: Gemini used for cleanup and rubrics but not integrated into a repeatable workflow.
- Resumes: Manual review and entry into ATS/tracker.
- Screening: Manual; no automated skills-based shortlist.
- Reporting: No single automated dashboard; data scattered across sheets and Bamboo.
**Target state:** [PLACEHOLDER: For each of the 7 areas, define trigger → system action → output. E.g., JD approved → job posting created; interview scheduled → calendar blocked and guide generated; recording done → transcript + rubric generated; resume received → parsed and scored; shortlist shared with hiring manager; dashboard refreshed from ATS/Bamboo/Sheets.]

## 5. Technical Requirements
**Systems Accessed:**
- Google Sheets (RFR tracker, ad-hoc trackers)
- Bamboo (ATS)
- Google Calendar (interview blocking)
- [PLACEHOLDER: Source of job descriptions; interview recording/transcript tool; Gemini or equivalent API.]
**Data Requirements:**
- Read: Job descriptions, interview schedules, recordings/transcripts, resumes, candidate data from ATS, scoring templates.
- Write: Calendar events, job postings (where published), interview guides, transcripts, rubrics, ATS/tracker records, shortlists, dashboard data.
- Transform: JD → job posting; recording → transcript → rubric; resume → structured fields; candidates → ranked shortlist; ATS/Sheets → dashboard.
**Permissions:**
- [PLACEHOLDER: Calendar API; Bamboo API; Sheets API; Gemini/transcript API; access to job posting channels.]
**Input → Processing → Output:**
- Input: JD approval, interview schedule, recording file, resume file, candidate applications; [PLACEHOLDER: triggers for each.]
- Processing: Calendar block; post creation; guide generation; transcript cleanup + rubric; resume parse; skills match; dashboard aggregate.
- Output: Blocked calendar; published posting; interview guide; transcript + rubric; parsed candidate; shortlist; recruitment dashboard.
**Integration Points:** Bamboo ↔ Sheets ↔ Calendar; [PLACEHOLDER: transcript service, job board, dashboard tool.]
**Limits and Expectations:** [PLACEHOLDER: Volume of roles, interviews, resumes; API quotas; SLA for transcript/rubric turnaround.]

## 6. Implementation
[PLACEHOLDER: High-level approach – e.g., implement in phases (calendar + posting first, then transcripts/rubrics, then resume/skills, then dashboard); use of low-code vs custom; how Gemini/templates are wired in.]

## 7. Alternatives Considered
[PLACEHOLDER: Keep full manual process; automate only one slice (e.g., calendar only); buy a single recruitment platform that does all of this.]

## 8. Risks and Dependencies
**Risks:** Multiple systems and steps increase complexity; transcript and scoring quality may vary; resume parsing may need tuning per role/source. Skills builder logic must be fair and explainable.
**Dependencies:** SOP exists (step-by-step guide) and spreadsheet template exists for structured output. Access to Bamboo, Calendar, Sheets, and [PLACEHOLDER: transcript and job posting systems.] [PLACEHOLDER: Ownership for Global Hiring Lifeline dashboard.]
**Open Questions:** [PLACEHOLDER: Which ATS features exist for skills/shortlist; where job postings are published; who owns dashboard product.]

## 9. Test Plan and Success Criteria
**Success Criteria:** Interview blocking, job posting creation, interview guides, transcripts/rubrics, resume parsing, shortlist, and dashboard all working per design; 2,080 hours/year saved; recruiters and hiring managers adopt new flow.
**Test Plan:** [PLACEHOLDER: Pilot with one role or one recruiter; validate each output (calendar, posting, guide, transcript, shortlist, dashboard); measure time before/after.]
**Validation:** [PLACEHOLDER: Weekly usage and time savings; quarterly recruitment metrics and stakeholder feedback.]