> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

> **Note:** This RFC integrates content from Cal Cooper's "RFC: AI-Assisted Documentation Pipeline" (January 26, 2026) with workflow automation requests from Jehan Zouak (Marketing), Cal Cooper (People Ops), and Gabriel Tsoi (Product).

# RFC: Product Release & Documentation System
**Submitted by:** Jehan Zouak (Marketing), Cal Cooper (People Ops), Gabriel Tsoi (Product)
**Impact Score:** 5 | **Scale:** System | **Frequency:** Weekly + as-needed
**Hours:** Product marketing release and changelog: 20 hrs/week; documentation pipeline: 15 hrs/week; release notes and support articles: 3 hrs/month | **Annual Hours Savings:** 1,856

## 1. Problem Statement
Product release and documentation today are manual and siloed across Marketing, Product Management, Knowledge Management, and Product Marketing. Vendasta currently faces challenges maintaining coherent documentation, release communications, and enablement materials as the platform evolves. Manual processes create:
- **Redundant work** across PM, PMM, and documentation teams; the same information is rewritten multiple times for release notes, customer-facing docs, changelog posts, support articles, and internal communications.
- **Inconsistencies** between documentation, release notes, and marketing materials.
- **Documentation lagging behind** platform changes; knowledge scattered across teams and tools (Confluence, JIRA, Google Chat, Google Docs, Google Sheets, Partner Center, Business App, Canny, GitHub, Docusaurus).
- **High cognitive load** on engineers and product managers for non-engineering tasks; platform changes originate in engineering repos but humans manually identify them through release notes tables or internal meetings, then rewrite (often with siloed AI assistance) and redistribute.
This creates a large coordination burden: 20 hrs/week (product marketing and changelog) + 15 hrs/week (documentation pipeline) + 3 hrs/month (release notes and support articles) = 1,856 hours/year combined across the three workflows.
**Who is affected:** Product Managers, Product Marketing, Knowledge Managers, Engineers, Sales, Partners and SMBs.
**Impact:** Delayed and inconsistent release communications; duplicated effort; risk of missed or wrong information when people are the bridge between systems.

## 2. Context & Goals
**Context:** Product releases are critical for adoption and revenue. Vendastians, partners, and SMBs need to know about and be empowered to sell or use new features. Today the steps required to properly release even a minor update require significant communication and task completion; for large releases, the number of stakeholders and coordination is even greater.
**Goals:**
1. Operate a documentation and release system that ingests platform change signals from engineering repositories, interprets those changes once, and produces and maintains multiple downstream knowledge artifacts automatically.
2. Single source of truth (GitHub repos) → multiple outputs with AI performing synthesis and humans acting as reviewers and governors (checkpoints for accuracy, intent, and risk).
3. Reduce release coordination time. [PLACEHOLDER: target % reduction.]
4. Consistency across channels (release notes, docs, changelog, support articles, announcements); documentation and releases kept coherent as the platform evolves.
5. Annual savings: 1,856 hours (validated quarterly).
6. Platform updates consistently and accurately translated into customer-facing documentation, internal release notes, and external product updates.

**Guiding Principles (non-negotiable):**
- **One Source of Truth → Many Outputs:** Repos are the signal; docs, marketing, and release notes are interpretations. A single change signal produces multiple downstream artifacts, ensuring consistency across all communication channels.
- **AI Does Synthesis; Humans Do Judgment:** AI drafts, structures, and cross-references content. Humans validate accuracy, intent, and risk. The system optimizes for human time spent on high-value judgment rather than manual writing.
- **Docs Are Not Downstream of Releases:** Documentation is generated from the same change signals as releases, not as a post-release activity. Documentation and releases are parallel outputs of the same source.
- **No Net-New Burden on PMs or Engineers:** At most: light metadata, tags, or commit conventions. No new writing responsibilities. The system works with existing development workflows.

**Success Criteria (6 weeks / 3 sprints):**
- Continuously ingests changes from engineering repos that impact platform functionality.
- Automatically generates three distinct outputs from the same source of truth: Customer-facing Help / How-To Documentation; External "What's New" / Product Marketing updates (Roadmap); Internal Release Notes (if necessary – or docs are new source of truth for this).
- Pushes draft content via PRs into GitHub, where AI handles first-pass synthesis and humans act as checkpoints and approvers, not authors; eliminates manual release notes, roadmap write-ups, and redundant PM/PMM handoffs.

## 3. Personas & User Stories
- As a **Product Manager**, I can have release notes generated from JIRA product matrix and story context so that I review and publish instead of writing from scratch.
- As a **Product Marketing Manager**, I can have changelog posts and partner-facing materials generated from the same source so that messaging is consistent and I focus on strategy.
- As a **Knowledge Manager**, I can have product documentation drafts generated from code and JIRA so that I edit and govern instead of manually tracking changes.
- As an **Engineer**, I can have my work reflected in docs and release notes from repo/JIRA so that I don't chase documentation updates.
- As a **Sales** user, I can have asset and announcement updates from the release pipeline so that I have current materials.
- As **Partners and SMBs**, I can see accurate, timely information about new features so that I can sell and use them.
- As a **Human Reviewer**, I can validate accuracy, intent, and risk at checkpoints so that I spend time on high-value judgment rather than manual writing.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
**High-level flows:**
- **Flow 1: GitHub commit → auto-generated outputs.** Code and/or docs change in GitHub; system parses commits and linked JIRA context; content is generated for each output type; drafts are routed to reviewers; humans review and approve; system publishes or schedules per release calendar.
- **Flow 2: JIRA story completion → coordinated release communications.** Story completed in JIRA; system extracts context and matches to release categories; release notes, Docusaurus drafts, and changelog entries are generated; review workflow routes to owners; after approval, outputs are published to Confluence, Docusaurus, changelog roadmap, Google Chat, Partner Center, Business App, Canny as applicable.

**System architecture (5 layers):**
- **Layer 1: Change Signal Intake.** The system monitors designated engineering repositories that impact platform functionality. Signals include: feature additions or enhancements, functional changes, renames or structural adjustments, deprecations or removals. Requirements: no documentation writing required from engineers; relies on existing development workflows; uses agreed-upon indicators of change (commits, PRs, tags, etc.).
- **Layer 2: Change Classification & Intent Framing.** Each detected change is interpreted to determine: nature of change (additive, mutative, or subtractive); scope of impact (localized vs platform-level); intended audience(s) (customer, partner, internal, or combination); type of explanation required (procedural, conceptual, or operational). This layer encodes product, marketing, and documentation intent so that downstream outputs remain aligned.
- **Layer 3: Knowledge Impact Analysis.** When a change affects a shared platform concept (e.g., naming, structure, or behavior), the system identifies all existing knowledge artifacts that reference it. Artifacts analyzed: help articles, FAQs, conceptual documentation, onboarding and enablement materials, internal reference content. For each affected artifact, the system determines where the reference appears, the type of update required (simple replacement, contextual adjustment, structural revision), and the relative risk of making the update automatically. Output is a structured impact set rather than a list of individual edits.
- **Layer 4: Output Generation & Mass Update.** From a single classified change, the system produces and updates multiple artifacts: (1) Customer-facing Help Documentation – user-focused, task-oriented, aligned to current UI and workflows; (2) External "What's New" Updates – value-oriented summaries framed for partners and customers; (3) Internal Release Notes – operationally focused, highlighting impact and dependencies. For systemic updates (e.g., renames), the system applies changes across all impacted artifacts, groups updates into manageable PRs, and preserves traceability and rollback capability.
- **Layer 5: Review, Approval, and Governance.** Human reviewers interact with the system through PR-based workflows. Reviewer responsibilities: verifying accuracy and clarity; confirming alignment with product intent; approving or requesting changes at the change-set level rather than per article. This model emphasizes review and judgment over manual authorship.

[PLACEHOLDER: Manual trigger path for ad-hoc or major releases.]

## 5. Technical Requirements
**Systems Accessed:**
- GitHub API (production repos, documentation repos)
- JIRA API (product matrix, stories)
- Confluence API (strategy docs, release tables)
- Google Chat API (announcements)
- Docusaurus (documentation site)
- Partner Center API
- Business App
- Canny API
- Changelog roadmap system

**Data Requirements:**
- Read: Git commits, JIRA tickets, Confluence pages, product metadata.
- Write: Release notes, documentation pages, changelog entries, notifications.
- Transform: Technical changes → customer-facing language across output types.

**Permissions:**
- [PLACEHOLDER: Service account details needed.]
- GitHub read access (production + docs repos)
- JIRA read access
- Confluence read/write
- Documentation repo write access

**Input → Processing → Output (aligned to 5 layers):**
- **Input:** GitHub commits (code changes, feature flags); JIRA stories (completion status, descriptions); Confluence release tables; manual trigger for releases.
- **Processing:** Layer 1 – intake change signals; Layer 2 – classify and frame intent; Layer 3 – analyze knowledge impact; Layer 4 – generate content for each output type (marketing communications, customer-facing documentation, technical release notes, changelog posts, support articles) and apply mass updates where needed; Layer 5 – route to human reviewers.
- **Output:** Marketing: release announcements (Partner Center, Business App); Documentation: updated docs in Docusaurus; Product: release notes in Confluence; External: changelog posts; Notifications: Google Chat alerts, Canny updates.

**Technical Considerations:**
- **Change Detection:** The system must reliably detect changes without requiring engineers to modify their workflows. Options include: git commit analysis, pull request monitoring, code diff analysis, tag-based triggers, CI/CD integration points.
- **AI Model Selection:** Considerations include context window size for analyzing code changes; multi-output generation capability; consistency across related artifacts; cost and latency requirements; fine-tuning requirements for domain-specific language.
- **Knowledge Graph Management:** The system requires a knowledge graph or similar structure to map platform concepts to documentation artifacts, track relationships between features and documentation, and enable impact analysis across artifacts.
- **Version Control Integration:** All generated content must be version controlled in appropriate repositories; support rollback capabilities; maintain traceability to source changes; enable collaborative review workflows.

**Integration Points:** GitHub webhooks for commit monitoring; JIRA webhooks for story completion; Confluence API for release tracking; documentation deployment pipeline.

**Limits and Expectations:** [PLACEHOLDER: API quotas needed.] [PLACEHOLDER: Processing time estimate.] Release frequency: Weekly (standard), as-needed (major releases).

## 6. Implementation
**High-level approach:**
1. Event listener monitors GitHub commits and JIRA stories (Layer 1).
2. AI agent parses technical changes, classifies intent, and analyzes knowledge impact (Layers 2–3).
3. Content generator creates outputs for each persona: marketing-focused (announcements, partner materials), developer-focused (technical docs, API changes), end-user-focused (changelog, support articles) (Layer 4).
4. Review workflow routes drafts to appropriate reviewers (PM, Knowledge Manager, Product Marketing); humans act as checkpoints (Layer 5).
5. Auto-publish or schedule based on release calendar after human approval.

**Delivery Plan (6 weeks / 3 sprints):**
- **Sprint 1 (Weeks 1–2): Scope, Standards, Signal Definition.** Objectives: identify and finalize in-scope engineering repositories; define the change classification taxonomy and intent model; establish documentation and messaging standards; align on review roles, approval thresholds, and governance expectations. Deliverables: repository inventory and selection criteria; initial change classification schema; documentation style guide and content templates; review workflow and role definitions.
- **Sprint 2 (Weeks 3–4): Change Interpretation and Impact Analysis.** Objectives: prototype automated change classification; implement knowledge impact detection; validate accuracy using historical platform changes; refine confidence thresholds for automated vs reviewed updates. Deliverables: change classification and intent-framing prototype; impact detection validation results; accuracy metrics and confidence thresholds.
- **Sprint 3 (Weeks 5–6): Output Generation, PR Workflow, and Operational Readiness.** Objectives: implement automated PR generation for new and updated artifacts; enable mass updates and batching for systemic changes; validate review and approval workflows with real reviewers; define success metrics, escalation paths, and ownership model. Deliverables: automated PR generation and update system; mass update and batching capability; review and approval workflow implementation; governance documentation and rollout readiness assessment.

[PLACEHOLDER: Phasing – e.g., release notes first, then docs, then changelog/marketing.]

## 7. Alternatives Considered
**Alternative 1: Continue manual process with AI assistance.** Rejected: Still requires copying between systems, maintains silos; would reduce time but not eliminate coordination burden. Conflicts with Guiding Principle: One Source of Truth → Many Outputs.
**Alternative 2: Separate automation for each output type.** Rejected: Maintains duplication, each team builds their own solution; would miss opportunity for integrated system. Conflicts with Guiding Principle: AI Does Synthesis; Humans Do Judgment at a single pipeline.
**Alternative 3: Third-party release management tool.** Rejected: [PLACEHOLDER: Need to research options e.g. LaunchDarkly.] Vendor lock-in, may not integrate with Vendasta systems; may not support "docs not downstream of releases" principle.

## 8. Risks and Dependencies
**Risks:**
- [PLACEHOLDER: API rate limits need verification.] GitHub/JIRA API changes could break integration.
- **Accuracy:** AI-generated content may contain inaccuracies or misinterpretations. Mitigation: human review checkpoints at every output; confidence scoring for automatic vs manual review; escalation paths for high-risk changes; continuous model improvement based on review feedback.
- **Adoption:** Teams may resist using the system or bypass it. Mitigation: clear value proposition demonstration; minimal workflow disruption; training and enablement; gradual rollout with early adopters.
- **Maintenance:** System may require ongoing maintenance and tuning. Mitigation: clear ownership and responsibility model; monitoring and alerting for system health; regular review of classification accuracy; documentation of system behavior and edge cases.
- AI-generated content quality may need human review initially. Multiple output formats increase complexity.

**Dependencies:** Access to all systems (GitHub, JIRA, Confluence, etc.). [PLACEHOLDER: Which teams need to approve?] SOP documentation exists but may need updates. Changelog roadmap system details unknown.

**Open Questions:**
- What are the exact API rate limits for GitHub, JIRA, Confluence?
- Who reviews and approves auto-generated content? What is the approval chain for publishing?
- What is the rollback process if output quality is poor?
- How do we handle manual overrides for sensitive releases?
- Which repositories should be included in the initial scope?
- What level of change granularity should trigger documentation generation?
- How should the system handle breaking changes vs additive changes?
- What is the review SLA and approval workflow?
- How should the system handle conflicting changes or rapid iterations?
- What is the rollback strategy for incorrect auto-generated content?
- How should the system integrate with existing documentation platforms?
- What are the cost implications of AI model usage at scale?

## 9. Test Plan and Success Criteria
**Test Plan:** Unit tests for individual content generators (release notes, docs, changelog); integration tests end-to-end from commit → published output; content quality review comparing AI-generated vs manual versions; pilot with non-critical release. [PLACEHOLDER: Specific test scenarios needed.]

**Success Criteria:**
- 90% of releases use automated system (measured weekly).
- Time from code commit to published docs under [PLACEHOLDER: target time].
- Content quality scores 4+ out of 5 from stakeholders.
- Zero missed releases due to automation failures.
- Annual hours saved 1,856 (validated quarterly).
- By end of 6 weeks / 3 sprints: pipeline continuously ingests changes, generates three distinct outputs, pushes draft content via PRs with humans as checkpoints.

**Success Metrics:**
- **Efficiency:** Reduction in manual documentation writing time; time from code change to published documentation; number of artifacts generated per change signal.
- **Quality:** Review approval rate; post-publication correction rate; consistency scores across related artifacts.
- **Adoption:** Percentage of changes processed through the system; reviewer satisfaction scores; system usage frequency.

**Validation:** Weekly review of generated content with stakeholders; monthly metrics on time savings; quarterly stakeholder satisfaction survey.

**Monitoring:** Dashboard tracking releases processed, outputs generated, errors; alert on failures or delays; weekly report to leadership on adoption and time savings.
