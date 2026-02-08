# Cursor Skill: Jira Sprint Creation (Discovery → Plan → MD Spec → Execution)

## Purpose

This skill helps create complete, high-quality sprint plans for Jira projects. It transforms project outlines and team objectives into a reviewable markdown sprint specification, then creates Jira stories with extensive, structured descriptions in the right epics, with strong acceptance criteria and owners.

**This skill must be called explicitly. It is not automatic.**

## When to Use This Skill

Use this skill when:
- You need to plan a new sprint and want to ground it in existing Jira reality (epics, backlog, previous sprint work)
- You have project outlines or objectives and need to break them into sprint-sized stories
- You want to create a reviewable markdown sprint plan before committing work to Jira
- You need to create Jira stories with detailed descriptions that can generate subtasks automatically
- You're working with a team that needs clear ownership, acceptance criteria, and epic alignment

---

## Inputs (you need these at minimum)
- **Jira project key** (variable: `<PROJECT_KEY>`, example: `ET`)
- **Sprint name** (variable: `<SPRINT_NAME>`, example: `The Sorting Sprint 2`)
- **Epic keys** that stories must align to (variable: `<EPIC_KEYS>`, example: `ET-18`, `ET-20`, `ET-21`, `ET-43`)
- **Project outlines** (paste them in: objectives, in/out of scope, signal sources, success criteria)
- **Team roster** + who owns what (and any fixed deadlines)

Optional but highly useful:
- Any “source-of-truth” docs (Confluence pages, RFCs, spreadsheets)
- Existing MD draft(s) of sprint plan (even messy)

### Board-agnostic note (important)
This skill works for **any Jira board/project** as long as you provide the correct inputs above.
- The JQL examples below use **ET** only as an example.
- Do **not** assume the same epics/sprint names exist on another board—swap in `<PROJECT_KEY>`, `<SPRINT_NAME>`, and `<EPIC_KEYS>`.

---

## Phase 0: Anchor to Jira reality (before drafting anything)

### 0.1 Pull the epic backbone (the constraints)
Goal: compile the “must-align” epic list and their intent.

JQL patterns:
- All epics in a project:
  - `project = <PROJECT_KEY> AND type = Epic ORDER BY key ASC`
- If you already know the epic keys:
  - `key in (<EPIC_KEYS>)`

Output:
- A short list of epics with keys + summaries + what work belongs there.

### 0.2 Pull last sprint + current sprint staging
Goal: understand what’s already in-flight, what rolled, and what’s already staged in the target sprint.

JQL patterns:
- Items already in the sprint:
  - `project = <PROJECT_KEY> AND sprint = "<SPRINT_NAME>" ORDER BY key ASC`
- Recently updated work (to see what the team touched):
  - `project = <PROJECT_KEY> AND updated >= -30d ORDER BY updated DESC`
- In progress items (work already consuming capacity):
  - `project = <PROJECT_KEY> AND status = "In Progress" ORDER BY updated DESC`

Output:
- “Reality map” of what’s already committed, in progress, and recently completed.

### 0.3 Identify “carry-over” stories vs “net-new” stories
Rule of thumb:
- If a story already exists and matches intent → **extend it** or add tasks to it.
- If it exists but is too broad → **split** into sprint-sized stories.
- If it exists but the new sprint needs a different outcome → create **new story** and link back in description.

Tip for other boards:
- Add `AND issuetype in (Story, Task)` or your board’s issue types if the board has custom types.
- If your org uses different status names, adjust `"In Progress"` accordingly.

### 0.4 No-comments policy (important)
This workflow assumes:
- **No automatic Jira comments** (keep the issue clean)
- All context should live in the **story description** itself and/or in the sprint MD spec.

---

## Phase 1: Turn project outlines into an initial sprint draft

### 1.1 Start with a “10-story max” constraint (then tighten)
Use an upper bound to force prioritization. You can later reduce to 8 (or fewer).

Guidelines:
- Each story should represent a clear deliverable a human can demo/verify.
- Each story should have an owner who can drive it to done.
- Avoid mixing unrelated outputs in one story unless they share the same deliverable.

### 1.2 Use this story template (copy/paste)
For each story:
- **Epic**: `<KEY> - <EPIC SUMMARY>`
- **Story title**: short + outcome-based
- **Owner**: `<Name>`
- **Supporting**: `<Names>`
- **Objective**: 1–2 lines
- **Scope**: bullets (what is included)
- **Out of scope**: bullets (what is explicitly excluded)
- **Acceptance Criteria**: checkboxes; outcomes measurable/observable
- **Execution Plan (ordered)**: numbered list in the exact order you’d want Jira to generate subtasks
- **Dependencies/Risks**: short bullets
- **Critical deadlines** (if any): dates + deliverables

### 1.3 Bake in “deadline ladders” when content is time-phased
If a story has multiple hard checkpoints (example: Feb 10/12/20), explicitly list:
- Deadline 1: minimal viable assets
- Deadline 2: cohort-ready content
- Deadline 3: end-of-sprint self-paced content

This prevents the story from becoming a vague “content blob”.

---

## Phase 2: Convert the draft into a reviewable MD spec (the collaboration artifact)

### 2.1 Write a single sprint MD file (source of truth)
Create a markdown file with:
- Sprint header (dates, sprint name)
- Stories 1–N (max 10; ideally 8)
- Owner + supporting + acceptance criteria + ordered execution plan
- Team capacity table
- Epic alignment section
- Dependency map (week 1 vs week 2)

Definition of done for the MD file:
- Every story has an epic key
- Every story has an owner
- Every story has acceptance criteria
- Every story has a clearly ordered execution plan (so Jira can generate subtasks later without inventing work)

### 2.2 Iteration protocol (fast edits)
When stakeholders change scope:
- Update owners/supporting inline
- Merge/split stories immediately (keep count ≤10)
- Move items to backlog explicitly (name the next sprint bucket)
- Remove over-specific sections if they aren’t needed in the sprint (ex: schema validation details)

Keep a “single source of truth” to avoid diverging drafts.

---

## Phase 3: Execute — create Jira stories with epics + owners

### 3.1 Create stories only (no subtasks, no comments)
Order matters:
1) Create the top-level stories (8)
2) Link each story to its epic
3) Assign each story owner
4) Paste the **extensive, ordered description** (see below) so Jira can generate subtasks later if desired

Do **not** create subtasks during initial sprint setup. Keep everything in the story description, ordered for subtask generation.

Board-agnostic execution reminder:
- When creating issues, ensure you’re using the correct `<PROJECT_KEY>` and the correct epic keys for that board.
- If the target board uses **Initiatives** or a different hierarchy level above epic, adapt “epic linking” to your hierarchy (still keep the story description structure the same).

### 3.2 Jira story description format (recommended)
Use headings so descriptions are readable and “subtask-ready”:
- `## Objective`
- `## Scope`
- `## Acceptance Criteria`
- `## Execution Plan (generate subtasks from this in order)`
- `## Links` (optional)

#### Execution Plan ordering rules (so Jira generates sensible subtasks)
Write the execution plan as a numbered list, grouped by phases. Example:
1. **Discovery**: access/inputs confirmed
2. **Build**: primary artifact produced
3. **Validate**: QA + stakeholder review
4. **Publish/Ship**: final placement + comms

Within each phase:
- Make each line a single “unit of work” (subtask-sized)
- Start with verbs (Export, Draft, Publish, Validate, Configure, Test)
- Include the owner in brackets at the end: `(Owner: Name)` if helpful

### 3.3 Subtasks policy
Default for this workflow:
- **Do not create subtasks during sprint setup.**
- Keep the story description detailed enough that Jira (or a human) can generate subtasks later.

If the team later wants subtasks:
- Generate them from the `## Execution Plan` section (in order), and keep the story description as the source of truth.

---

## Phase 4: Place work into the sprint (optional)
There are two legit approaches:
- **Approach A**: Add issues to sprint in the UI (fastest)
- **Approach B**: Use sprint assignment APIs if available in your integration

If sprint assignment is blocked by tooling permissions, do Approach A and keep the work moving.

---

## Quality gates (before you call it “done”)

### Gate 1: Epic alignment
- Every story has the correct epic parent.

### Gate 2: Owner clarity
- Every story is assigned to the correct owner.
- Execution plan steps have clear ownership where needed.

### Gate 3: Acceptance criteria completeness
- Not “do X”, but “X is true / observable outcome”.
- Deadlines listed explicitly where required.

### Gate 4: Scope discipline
- Sprint story count ≤10.
- Anything moved out is explicitly “Backlog: next sprint” with a named placeholder.

---

## Example: End-to-end checklist (copy/paste)
- [ ] Pull epics for project
- [ ] Pull last sprint + current sprint staged work
- [ ] Identify in-progress capacity constraints
- [ ] Draft max-10 stories aligned to epics
- [ ] Iterate to max-8 (or fewer) with stakeholders
- [ ] Create the sprint MD file (source of truth)
- [ ] Stakeholder review and edits
- [ ] Create 8 Jira stories (correct epics + owners)
- [ ] Ensure each Jira story has an ordered `## Execution Plan` (subtask-ready)
- [ ] (Optional) Add stories to sprint

