# Sprint: Feb 9-20, 2026 - Enablement Team
**Sprint Name:** The Sorting Sprint 2  
**Duration:** 2 weeks (Feb 9 - Feb 20, 2026)  
**Team:** Enablement Team (L&E MASTER project)

---

## Sprint Overview

This sprint delivers comprehensive MIRA workforce intelligence data integration, Citizen Developer technical rigor training with Vibe alpha spike, Vendasta Services AI-ready knowledge system with Cursor automation, and AI at Vendasta learning portal architecture solidification.

**Key Priorities:**
1. MIRA Phase 2 complete with all signal sources + pilot consolidation
2. Citizen Developer content with 3 critical deadlines (Feb 10, 12, 20)
3. Vendasta Services MVP with Cursor-automated content migration
4. Learning portal architecture solidified with optimized guides

---

# Story 1: MIRA Workforce Intelligence - Comprehensive Data Integration (Phase 2 Complete)

**Epic:** ET-21 - Establish AI-powered pilot function workflows across People Ops and Vendasta Services  
**Owner:** Cal  
**Supporting:** Amita, Gwynneth Miller, Emma  
**Partnership:** Katelyn Dilsner (People Ops), Jason (Technical)  
**Priority:** High  
**Story Points:** 13

## Story Description

Deliver comprehensive workforce intelligence data integration across ALL signal sources to build unified person intelligence profiles. This consolidates the full Phase 2 data ingestion into a single coordinated effort, breaking down the large ET-78 backlog item.

## Acceptance Criteria

- [ ] All 6 primary signal sources integrated into MIRA unified person profiles
- [ ] Data quality report published showing coverage, gaps, and conflicts across sources
- [ ] Partnership models documented with People Ops (Katelyn) and Talent (Gwynneth)
- [ ] Privacy and consent framework established for LinkedIn data
- [ ] Skills inventory baseline established showing: formal training, self-reported capabilities, and career trajectories
- [ ] Gap analysis complete: identify where employees are upskilling outside current role requirements
- [ ] At least 80% of current employees have comprehensive person intelligence profiles
- [ ] MIRA pilot consolidation complete: takeaways, recommendations, and next steps presented to People Ops leadership

## Subtasks

### Subtask 1.1: MIRA Interview Data Consolidation [Amita]
- Consolidate existing MIRA pilot interview data into unified schema
- Extract: role context, responsibilities, contributions, collaboration patterns
- Document: tools and platform usage, daily and weekly work patterns
- **Output:** MIRA pilot data fully integrated into person intelligence profiles

### Subtask 1.2: BambooHR Work History Integration [Cal]
- Export and ingest: tenure, role transitions, org structure, reporting relationships
- Extract: previous positions within Vendasta, employment history and career progression
- Coordinate with Katelyn Dilsner (People Ops owner)
- **Output:** BambooHR data mapped to MIRA person profiles

### Subtask 1.3: Current Role Information Extraction [Cal]
- Extract: job descriptions, team assignments, department alignment
- Document: reporting structure and organizational context
- Capture: role-specific requirements and expectations
- **Output:** Current role data integrated into person profiles

### Subtask 1.4: LinkedIn Profiles Integration [Cal + Gwynneth]
- Pull LinkedIn data with employee consent: skills endorsements and self-reported capabilities
- Extract: career history and previous roles
- Capture: certifications and professional achievements
- Document: network connections and collaboration patterns
- Coordinate with Gwynneth Miller and Talent team
- **Output:** LinkedIn data integrated with privacy/consent framework documented

### Subtask 1.5: Lattice Growth & Goals Data Integration [Gwynneth]
- Pull Lattice Growth Paths and Grow Areas data
- Extract Lattice Goals from last 18 months to identify performance patterns
- Coordinate with Gwynneth Miller (Talent team contact)
- **Output:** Lattice data integrated showing growth trajectories and goals

### Subtask 1.6: Professional Development History Integration [Emma + Cal]
- Ingest Professional Development funding records (all time) - training, certifications, courses
- Document training history and upskilling records
- **Output:** Professional development data integrated showing investment in skills

### Subtask 1.7: MIRA Pilot Consolidation & Leadership Presentation [Amita]
- Consolidate existing MIRA interview data from People Ops pilot
- Analyze pilot outcomes: what worked, what didn't, data quality insights
- Develop takeaways and recommendations for broader MIRA implementation
- Present findings to People Ops leadership team with next steps for scaling MIRA
- Document lessons learned and implementation roadmap for other divisions
- **Output:** Leadership presentation complete with recommendations for scaling

## Dependencies

- Access to Lattice, BambooHR, LinkedIn APIs/exports
- Employee consent for LinkedIn data
- People Ops and Talent team partnerships (Katelyn, Gwynneth)
- MIRA pilot data from Amita's previous work

## Technical Notes

- Privacy and consent framework critical for LinkedIn data
- Coordinate across multiple stakeholders (People Ops, Talent, L&E)
- Cal owns technical coordination, Amita owns pilot consolidation analysis

---

# Story 2: People Ops Workflow Intelligence - 80% Coverage Completion

**Epic:** ET-21 - Establish AI-powered pilot function workflows across People Ops and Vendasta Services  
**Owner:** Amita  
**Supporting:** Cal  
**Priority:** High  
**Story Points:** 8  
**Continuation of:** ET-22 (already in progress)

## Story Description

Complete the 80% coverage target for People Operations workflow mapping. The goal is to document enough workflows to account for 80% of estimated manual People Ops effort, measured cumulatively across all mapped workflows.

## Acceptance Criteria

- [ ] 80% coverage target achieved (measured by cumulative manual effort across documented workflows)
- [ ] All documented workflows scored for AI automation potential using Impact Score framework (1-5)
- [ ] Baseline report published showing high-priority workflows for MIRA pilot automation
- [ ] Clear handoff to MIRA for "AI-ready" workflow candidates
- [ ] Process maps include: inputs, steps, outputs, decision points, failure modes
- [ ] Knowledge gaps identified: where process knowledge lives in people's heads vs. systems

## Subtasks

### Subtask 2.1: Complete Remaining Workflow Documentation [Amita]
- Document remaining workflows to reach 80% of estimated manual People Ops effort
- Prioritize workflows from workflow automation survey CSV (high-impact, high-frequency)
- Use standard process mapping format: inputs, steps, outputs, decision points, failure modes
- **Output:** Workflow documentation complete for 80% coverage

### Subtask 2.2: Identify Knowledge Gaps [Amita]
- For each workflow, identify where knowledge lives: documented vs. in people's heads
- Flag workflows where documentation doesn't exist but should
- Document tribal knowledge that needs to be captured
- **Output:** Knowledge gap assessment complete

### Subtask 2.3: Score Workflows for AI Automation Potential [Amita + Cal]
- Apply Impact Score framework (1-5) to each documented workflow
- Consider: data availability, API access, rule complexity, frequency
- Prioritize workflows for MIRA pilot automation
- **Output:** All workflows scored and prioritized

### Subtask 2.4: Publish People Ops Workflow Intelligence Baseline Report [Amita]
- Compile all workflow documentation into Confluence report
- Include: workflow maps, knowledge gaps, automation scores, recommendations
- Highlight high-priority workflows for MIRA pilot
- **Output:** Baseline report published to Confluence

## Dependencies

- Workflow automation survey CSV data
- Access to People Ops team for workflow validation
- Continuation of ET-22 (already in progress)

## Technical Notes

- Focus on workflows where "people are the bridge" between systems
- 80% coverage measured by cumulative manual effort (time × frequency)

---

# Story 3: Vendasta Services AI-Ready Knowledge System - MVP Launch with Cursor-Automated Migration

**Epic:** ET-21 - Establish AI-powered pilot function workflows across People Ops and Vendasta Services  
**Owner:** Dhanesh  
**Supporting:** Cal  
**Priority:** High  
**Story Points:** 13  
**Continuation of:** ET-44 (already in progress)

## Story Description

Establish the foundational AI-ready knowledge system for Vendasta Services pilot workflows, using Cursor to automate content migration from Google Sheets to GitHub repositories. Dhanesh's role is quality assurance, not manual data entry.

## Acceptance Criteria

- [ ] Cursor automation solution built and successfully migrates content from Google Sheets to GitHub
- [ ] At least one complete Vendasta Services workflow exists as AI-readable, version-controlled documentation in GitHub
- [ ] Google Chat AI successfully references new GitHub documentation source for pilot workflow questions
- [ ] First AI failure logged and produces trackable documentation action
- [ ] Operating model documented: who owns updates, how failures become improvements, how Cursor automation is maintained
- [ ] Dhanesh validates automation quality but does not manually migrate content

## Subtasks

### Subtask 3.1: Build Cursor Automation for Content Migration [Dhanesh]
- Use Cursor to build automation solution for migrating Vendasta Services content from Google Sheets to GitHub
- Choose approach: either build a Cursor application OR create a set of skill.md files in Cursor
- Ensure automation extracts, transforms, and organizes ALL content from sheets into AI-readable format
- Automate maintenance of content structure, relationships, and metadata
- **Output:** Cursor automation solution built and tested

### Subtask 3.2: Finalize Version-Controlled Documentation Repository [Dhanesh + Cal]
- Set up GitHub repository for Vendasta Services SOPs (following product docs model)
- Establish folder structure, naming conventions, and markdown standards
- Configure repository for AI ingestion
- **Output:** GitHub repo ready for automated content migration

### Subtask 3.3: Migrate Pilot Workflow Using Cursor Automation [Dhanesh]
- Run Cursor automation to migrate at least one pilot workflow from Google Sheets to GitHub
- Source content from: PDFs, plain-text exports, Google Sheets
- Dhanesh role: quality assurance of automated output, NOT manual data entry
- Ensure all migrated content is in markdown format, properly organized
- **Output:** One complete workflow migrated and validated in GitHub

### Subtask 3.4: Configure Google Chat AI Integration [Dhanesh + Cal]
- Configure Google Chat AI to reference new GitHub documentation source
- Replace manual upload pipeline with direct GitHub integration
- Test AI references to migrated workflow content
- **Output:** Google Chat AI successfully queries GitHub documentation

### Subtask 3.5: Implement AI Failure Capture Loop [Dhanesh]
- Log AI failures in structured format (when AI can't answer or answers incorrectly)
- Create feedback mechanism: AI failure → documentation team notification
- Document the "failure → signal → documentation update" workflow
- Test end-to-end: employee asks question → AI references source → failure logged → documentation updated
- **Output:** AI failure capture loop operational

### Subtask 3.6: Document Operating Model [Dhanesh]
- Document: who owns documentation updates
- Document: how AI failures become documentation improvements
- Document: how to maintain Cursor automation for future workflows
- **Output:** Operating model published to Confluence

## Dependencies

- Google Sheets with Vendasta Services content
- GitHub repository access
- Google Chat AI configuration permissions
- Cursor access for automation

## Technical Notes

- Dhanesh focuses on building automation and QA, not manual work
- Cursor automation establishes repeatable process for future workflows
- AI failure loop is critical for continuous improvement

---

# Story 4: Citizen Developer Content - RFC Gold Standard, Cursor, Platform AI & Vendasta Vibe

**Epic:** ET-18 - Develop and Manage a Global Citizen Developer Program  
**Owner:** Cal  
**Supporting:** Emma, Shiva, Ahnika, Jesse (Vibe product context)  
**Priority:** Critical  
**Story Points:** 13  
**Continuation of:** ET-3 (Weeks 1-3 curriculum already in progress)

## Story Description

Create the RFC technical rigor content, Cursor curriculum, Vendasta platform AI content development guidance, and complete full Vibe spike for internal trials. This story has THREE CRITICAL DEADLINES.

## Critical Deadlines

1. **Feb 10 (Day 2):** Cursor video walkthroughs created/sourced and added
2. **Feb 12 (Day 4):** Core training content (RFC, Cursor) published to Confluence
3. **Feb 20 (End of sprint):** Vibe full spike and Vendasta platform AI content published

## Acceptance Criteria

- [ ] **Critical Deadline 1 (Feb 10):** Cursor video walkthroughs created/sourced and added
- [ ] **Critical Deadline 2 (Feb 12):** Core training content (RFC, Cursor) published to Confluence and reviewed by Emma and Shiva
- [ ] **Critical Deadline 3 (Feb 20):** Vibe full spike and Vendasta platform AI content published for self-paced learning
- [ ] Vibe full spike complete by Feb 20: Vibe coding system understood, existing partner articles adapted for citizen developer audience
- [ ] At least 5 citizen developers enrolled in Vibe alpha trial program
- [ ] RFC guidance emphasizes rough draft state with technical requirement mapping, not final documents

## Subtasks

### Subtask 4.1: Create or Find Cursor Video Walkthroughs [Cal] - DUE FEB 10
- Create or source video walkthroughs for Cursor for non-engineers
- Add videos to Confluence by end of first two days of sprint (Feb 10)
- Ensure videos are accessible for non-technical audience
- **Output:** Cursor videos published by Feb 10

### Subtask 4.2: RFC Gold Standard Content Creation [Cal] - DUE FEB 12
- Create "Strategy vs. Technical RFC" comparison guide with side-by-side examples
- Define mandatory RFC sections for non-engineers: Technical Leverage Points, Failure Points, Data Access Points
- Develop RFC template with plain-language prompts
- Create "RFC Self-Sufficiency Checklist" - questions developers must answer before involving R&D
- Include 2-3 example RFCs (one "bad" strategic RFC, two "good" technical RFCs)
- Emphasize: RFCs at this stage are rough drafts with mapped technical requirements
- **Output:** RFC Gold Standard content published to Confluence by Feb 12

### Subtask 4.3: Cursor Curriculum Session Content [Cal] - DUE FEB 12
- ~~Finalize "Getting Started with Cursor for Non-Engineers" guide~~ (Already done)
- ~~Create tutorial: "Writing Your Personal README.md Using Cursor"~~ (Already done)
- Develop session content: "Using Cursor to Interrogate Technical Requirements"
- Develop 3-5 practice scenarios where CDs use Cursor to research technical requirements
- **Output:** Cursor session content ready for Emma and Shiva by Feb 12

### Subtask 4.4: Vendasta Platform AI Content Development [Cal] - DUE FEB 20
- Create self-paced content: "Deep Understanding of Vendasta 'Vibe' - The Vision and Technical Architecture"
- Document platform AI content development principles for citizen developers
- Explain how citizen developers can contribute to platform AI capabilities
- Provide context on how Vendasta platform AI differs from external AI tools
- **Output:** Platform AI content published by Feb 20

### Subtask 4.5: Vendasta 'Vibe' Full Spike [Cal + Ahnika] - DUE FEB 20
- Coordinate with Jesse to understand Vibe product vision, technical architecture, and coding system
- Deep dive into Vibe coding system and how it differs from standard coding approaches
- Ahnika: Understand Vibe coding system basics
- Ahnika: Adapt existing Vibe partner-facing articles to be applicable for citizen developer audience
- Ahnika: Rewrite/adapt Vibe content for internal audience
- Cal + Ahnika: Create internal trial program outline for citizen developers to test Vibe
- Develop "Vibe Early Access Guide" for citizen developer alpha testers (not partners)
- Document use cases where citizen developers can leverage Vibe for their internal projects
- Gather feedback mechanisms for alpha trial participants
- Publish citizen developer-focused Vibe documentation to internal learning portal
- **Output:** Vibe full spike complete with citizen developer-focused documentation by Feb 20

### Subtask 4.6: Multimedia Assets and Confluence Pages [Cal]
- Create interactive Confluence pages with embedded Cursor videos
- Add citizen developer-focused Vibe documentation (not partner-facing)
- **Output:** All content properly formatted and embedded in Confluence

### Subtask 4.7: Content Review with Emma and Shiva [Emma + Shiva]
- Review all training content (RFC, Cursor) for session delivery readiness
- Provide feedback on clarity and usability for NA and Chennai cohorts
- **Output:** Content reviewed and approved for training sessions

## Dependencies

- Jesse's availability for Vibe product context
- Cursor video creation/sourcing by Feb 10
- Ahnika's availability for Vibe content adaptation
- Emma and Shiva's review by Feb 12

## Technical Notes

- Three distinct deadlines require phased delivery
- Vibe spike is a full project with Cal and Ahnika co-leads
- RFC guidance emphasizes rough drafts, not final documents
- Content must support both NA and Chennai cohorts

---

# Story 5: Citizen Developer Training Delivery - NA & Chennai Cohorts

**Epic:** ET-18 - Develop and Manage a Global Citizen Developer Program  
**Owners:** Emma (NA cohort), Shiva (Chennai cohort)  
**Supporting:** Cal (content), Jason (technical Q&A)  
**Priority:** High  
**Story Points:** 5  
**Dependency:** Story 4 Critical Deadline 2 (Feb 12)

## Story Description

Execute training sessions for both NA and Chennai cohorts using the RFC Gold Standard and Cursor Curriculum content. Sessions must happen after Feb 12 when content is ready.

## Acceptance Criteria

- [ ] Both NA and Chennai sessions delivered by end of sprint
- [ ] Participants demonstrate ability to use Cursor for technical research
- [ ] Post-session feedback collected from all participants
- [ ] At least 80% of participants report confidence in writing technical RFCs
- [ ] Attendance and engagement levels documented

## Subtasks

### Subtask 5.1: Schedule NA Cohort Session [Emma]
- Schedule NA cohort session (after Feb 12 content delivery)
- Confirm participant list and send calendar invitations
- Prepare session logistics (Zoom link, Confluence pages, materials)
- **Output:** NA session scheduled and participants confirmed

### Subtask 5.2: Schedule Chennai Cohort Session [Shiva]
- Schedule Chennai cohort session (after Feb 12 content delivery)
- Adapt delivery for Chennai context (time zones, regional communication styles)
- Confirm participant list and send calendar invitations
- **Output:** Chennai session scheduled and participants confirmed

### Subtask 5.3: Facilitate NA Cohort Training Session [Emma]
- Walk through "Strategy vs. Technical RFC" guide with live examples
- Lead hands-on Cursor exercise: participants write personal README.md
- Conduct live technical research exercise using Cursor
- Review RFC Self-Sufficiency Checklist and "R&D Boundary" expectations
- Jason available for technical Q&A during session
- **Output:** NA cohort training complete

### Subtask 5.4: Facilitate Chennai Cohort Training Session [Shiva]
- Walk through "Strategy vs. Technical RFC" guide with live examples
- Lead hands-on Cursor exercise: participants write personal README.md
- Conduct live technical research exercise using Cursor
- Review RFC Self-Sufficiency Checklist and "R&D Boundary" expectations
- Jason available for technical Q&A (consider time zone)
- **Output:** Chennai cohort training complete

### Subtask 5.5: Collect Post-Session Feedback [Emma + Shiva]
- Collect participant feedback on content clarity and usefulness
- Document attendance and engagement levels
- **Output:** Feedback collected from all participants

## Dependencies

- Story 4 completion by Feb 12 (core training content ready)
- Jason's availability for technical Q&A
- Confirmed participant lists

## Technical Notes

- Sessions must emphasize: RFCs are rough drafts, focus on mapping technical requirements
- Jason should clarify the "R&D Boundary" during sessions
- Both cohorts should receive consistent training despite regional differences

---

# Story 6: Citizen Developer Program - Ongoing RFC Coaching & Technical Requirement Validation

**Epic:** ET-18 - Develop and Manage a Global Citizen Developer Program  
**Owners:** Emma (NA cohort), Shiva (Chennai cohort)  
**Technical Support:** Jason (early RFC reviews)  
**Priority:** High  
**Story Points:** 8

## Story Description

Provide ongoing, informal coaching to Citizen Developers as they develop rough draft RFCs with mapped technical requirements. Focus on iterative support rather than formal audits. All rough drafts published in Confluence by end of sprint (Feb 20).

## Acceptance Criteria

- [ ] All CD participants have at least one weekly check-in with Emma or Shiva throughout sprint
- [ ] 100% of participants have rough draft RFCs published in Confluence by Feb 20 (rough state acceptable)
- [ ] At least 80% of participants have identified 3+ key technical questions for their project
- [ ] At least 50% of participants have had early technical review with Jason on requirement mapping
- [ ] No formal feedback report required - focus is on iterative coaching and accountability

## Subtasks

### Subtask 6.1: Coordinate with Jason for Early RFC Reviews [Emma + Shiva]
- Schedule Jason's availability for early RFC reviews throughout sprint
- Establish process: when to bring Jason in, what to review
- Focus: validate technical requirements are properly mapped, not complete RFCs
- **Output:** Jason review process established

### Subtask 6.2: Weekly Individual Check-ins - NA Cohort [Emma]
- Check in with each NA participant at least once per week
- Check-in focus: How is your project concept coming? What technical questions have you uncovered? Where are you stuck?
- Provide informal, conversational feedback - no formal written summaries
- Help CDs identify who in R&D or technical teams they should talk to for discovery
- **Output:** All NA participants have weekly check-ins throughout sprint

### Subtask 6.3: Weekly Individual Check-ins - Chennai Cohort [Shiva]
- Check in with each Chennai participant at least once per week
- Check-in focus: How is your project concept coming? What technical questions have you uncovered? Where are you stuck?
- Provide informal, conversational feedback - no formal written summaries
- Help CDs identify who in R&D or technical teams they should talk to for discovery
- **Output:** All Chennai participants have weekly check-ins throughout sprint

### Subtask 6.4: Validate Minimum RFC Rough Draft Requirements [Emma + Shiva]
- Ensure each CD has identified at minimum 3 key technical questions for their RFC
- Technical questions should demonstrate understanding of: data sources, system integrations, failure modes, or technical constraints
- Rough drafts should show evidence of using Cursor to interrogate technical requirements
- **Output:** 80% of participants have 3+ key technical questions identified

### Subtask 6.5: Coordinate Early Jason Reviews for Technical Requirements [Emma + Shiva + Jason]
- Bring Jason in for early review of rough draft RFCs (at least 50% of participants)
- Focus: Is technical requirement mapping solid? Are they asking the right questions?
- Identify who in R&D participants should talk to for further discovery
- **Output:** 50% of participants have had early Jason review

### Subtask 6.6: Ensure All Rough Drafts Published in Confluence by Feb 20 [Emma + Shiva]
- Track RFC rough draft progress throughout sprint
- Ensure all participants publish rough drafts to Confluence by end of sprint
- RFCs in rough draft state (NOT verified or final state) are acceptable
- Each RFC includes: project concept, technical questions identified, preliminary technical requirements mapped
- **Output:** 100% of participants have rough draft RFCs in Confluence by Feb 20

## Dependencies

- Story 5 completion (training delivered)
- Jason's availability for early RFC reviews throughout sprint
- Participant engagement in weekly check-ins

## Technical Notes

- Focus on iterative coaching, not formal audits
- Goal: CDs develop technical thinking skills and ask the right questions
- Rough drafts with identified technical questions are the target, not perfect RFCs

---

# Story 7: Support Tool Migration - Loom to Google Vids Transition Guide

**Epic:** ET-43 - Business as Usual (BAUs)  
**Owner:** Cal  
**Reviewer:** Haley  
**Priority:** Medium  
**Story Points:** 3

## Story Description

Complete the Loom to Google Vids migration support for the Support team by testing Google Vids, documenting limitations, and publishing a comprehensive migration guide.

## Acceptance Criteria

- [ ] Migration guide published and approved by Haley
- [ ] Support team leadership briefed on transition
- [ ] Article shared in Support team channels
- [ ] Technical spike complete with limitations documented
- [ ] Manual "Save & Organize" workflow documented

## Subtasks

### Subtask 7.1: Technical Spike - Test Google Vids [Cal]
- Test Google Vids recording and sharing functionality from Support team perspective
- Document manual "Save & Organize" workflow to replace Loom's instant-cloud storage
- Identify key limitations vs. Loom (no Chrome extension, manual save step, folder organization)
- Create comparison table: Loom vs. Google Vids feature set
- Identify Support use cases where Google Vids may not be sufficient
- **Output:** Technical spike complete with findings documented

### Subtask 7.2: Write Comprehensive Migration Guide [Cal]
- Write migration article with sections:
  - Why the Change? (Context on the transition)
  - What's Different? (Key changes from Loom to Google Vids)
  - Step-by-Step Guide: Recording and sharing videos in Google Vids
  - Manual Save & Organize Workflow
  - Naming Conventions for easy retrieval
  - FAQs and Troubleshooting
- Include screenshots/GIFs for each step
- **Output:** Migration guide drafted

### Subtask 7.3: Review with Haley for Support Use Cases [Cal + Haley]
- Collaborate with Haley to ensure guide addresses Support team-specific use cases
- Add section: "When NOT to use Google Vids" (if any edge cases exist)
- Get Haley's approval before publishing
- **Output:** Guide reviewed and approved by Haley

### Subtask 7.4: Publish and Share Migration Guide [Cal]
- Publish to Confluence in Support team's knowledge base
- Brief Support team leadership on transition
- Share article in Support team channels (Slack/Google Chat)
- **Output:** Guide published and communicated to Support team

## Dependencies

- Access to Google Vids for testing
- Haley's availability for review
- Support team knowledge base access

## Technical Notes

- Tone should be supportive and practical, not dismissive of Loom preference
- Focus on making transition as smooth as possible

---

# Story 8: AI at Vendasta Learning Portal - Architecture Solidification & Content Optimization

**Epic:** ET-20 - Make AI execution visible across the organization  
**Owner:** Maryam  
**Supporting:** Cal, Emma  
**Priority:** High  
**Story Points:** 13

## Story Description

Solidify the AI at Vendasta learning portal architecture to ensure automation and AI material is consistent, concise, and appropriate for internal audience. Optimize existing tool guides (Atlassian, Cursor, Vendasta Platform) with end-to-end workflows, screenshots, and videos.

## Acceptance Criteria

- [ ] Learning portal architecture documented and content standards established
- [ ] Atlassian tools guides optimized with at least 3 end-to-end workflow guides, screenshots, and videos
- [ ] Cursor guides optimized with at least 3 end-to-end workflow guides, screenshots/GIFs, and videos
- [ ] Vendasta Platform guides optimized with at least 3 end-to-end workflow guides, screenshots, and videos
- [ ] RFC and Cursor training content published in self-paced format
- [ ] Content governance model documented and approved
- [ ] All content reviewed for consistency with established standards

## Subtasks

### Subtask 8.1: Solidify Learning Portal Architecture [Maryam]
- Define overall architecture: navigation, categorization, content hierarchy
- Establish content standards: tone, voice, formatting, length for internal automation and AI material
- Ensure all automation and AI content is consistent, concise, tailored to Vendasta employee audience
- Audit existing content for consistency and identify gaps in coverage
- **Output:** Portal architecture documented with content standards

### Subtask 8.2: Create Content Governance Model [Maryam]
- Define: who can publish, review process, update cadence
- Establish approval workflow for new content
- Document roles and responsibilities for content maintenance
- **Output:** Content governance model published

### Subtask 8.3: Optimize Atlassian Tools Guides with End-to-End Workflows [Maryam + Cal]
- Review existing Confluence, Jira, and other Atlassian tools guides
- Add screenshots and videos where applicable to improve clarity
- Create at least 3 end-to-end workflow guides for Atlassian tools:
  - "Creating a Jira Issue from Start to Finish"
  - "Publishing a Confluence Page: Complete Workflow"
  - "Collaborating on Confluence: From Draft to Published"
- Ensure guides show complete user journeys, not just feature explanations
- **Output:** Atlassian guides optimized with end-to-end workflows

### Subtask 8.4: Optimize Cursor Guides with End-to-End Workflows [Maryam + Cal]
- Review existing Cursor documentation for citizen developers
- Add screenshots, GIFs, and short videos where applicable
- Create at least 3 end-to-end workflow guides for Cursor:
  - "Writing Your First Code with Cursor: Complete Workflow"
  - "Using Cursor to Research Technical Requirements: End-to-End"
  - "Cursor for Non-Engineers: A Complete First Project"
- Ensure guides are optimized for non-technical audience
- **Output:** Cursor guides optimized with end-to-end workflows

### Subtask 8.5: Optimize Vendasta Platform Guides with End-to-End Workflows [Maryam]
- Review existing Vendasta platform documentation for internal users
- Add screenshots and videos where applicable
- Create at least 3 end-to-end workflow guides for Vendasta Platform:
  - "Setting Up Your First AI Employee: Complete Workflow"
  - "Configuring Knowledge Sources: End-to-End Guide"
  - "Testing and Deploying an AI Capability: Complete Process"
- Focus on internal employee use cases (not partner-facing)
- **Output:** Vendasta Platform guides optimized with end-to-end workflows

### Subtask 8.6: Convert Citizen Developer Training Content to Self-Paced Format [Maryam + Cal]
- Convert RFC Gold Standard content (from Story 4) into self-paced learning module
- Convert Cursor Curriculum into self-paced format with checkpoints
- Add practice exercises with answer keys
- Include "Next Steps: How to join Citizen Developer program"
- **Output:** RFC and Cursor training content published in self-paced format

### Subtask 8.7: Review All Content for Consistency [Maryam]
- Review all optimized content against established standards
- Ensure consistency in tone, voice, formatting across all guides
- Validate that end-to-end workflows show complete user journeys
- **Output:** All content reviewed and validated for consistency

## Dependencies

- Story 4 completion (RFC and Cursor content for self-paced conversion)
- Cal's availability for Atlassian and Cursor guide optimization
- Access to AI at Vendasta learning portal

## Technical Notes

- Focus on end-to-end workflows that show complete user journeys
- Portal needs solid foundation before scaling
- Content should be truly self-serve (no instructor required)

---

# Sprint Success Criteria Summary

By end of sprint (Feb 20, 2026):

1. ✅ **MIRA Phase 2 complete:** All signal sources integrated + pilot consolidation presented to People Ops leadership
2. ✅ **Citizen Developer content complete:** Three critical deadlines met (Feb 10, 12, 20)
3. ✅ **Citizen Developer training delivered:** NA and Chennai cohorts trained
4. ✅ **Citizen Developer RFC coaching complete:** Rough draft RFCs in Confluence, weekly check-ins conducted
5. ✅ **Vendasta Services MVP live:** Cursor-automated content migration operational
6. ✅ **People Ops 80% coverage achieved:** Workflow baseline ready for MIRA automation
7. ✅ **AI at Vendasta learning portal solidified:** Architecture and optimized guides with end-to-end workflows

---

# Team Capacity & Ownership Summary

| Team Member | Stories | Primary Responsibilities |
|-------------|---------|-------------------------|
| **Cal** | 1, 4, 7 | MIRA integration (owner), Citizen Dev content with 3 deadlines (owner), Loom migration (owner) |
| **Amita** | 1, 2 | MIRA pilot consolidation & People Ops presentation (Story 1), People Ops workflows 80% coverage (owner Story 2) |
| **Gwynneth Miller** | 1 | Talent data partnerships for MIRA (Lattice, LinkedIn) |
| **Dhanesh** | 3 | Vendasta Services with Cursor automation (owner) |
| **Emma** | 1, 5, 6, 8 | L&E learning data (Story 1), NA training delivery (owner Story 5), NA RFC coaching (owner Story 6), Learning portal support |
| **Shiva** | 5, 6 | Chennai training delivery (owner Story 5), Chennai RFC coaching (owner Story 6) |
| **Ahnika** | 4 | Vibe spike co-lead with Cal |
| **Maryam** | 8 | Learning portal architecture solidification (owner) |
| **Jason** | 1, 5, 6 | Technical support for MIRA, training Q&A, early RFC reviews |
| **Jesse** | 4 | Vibe product context |
| **Haley** | 7 | Loom migration guide review |
| **Katelyn Dilsner** | 1 | People Ops data partnership |

---

# Epic Alignment

- **ET-21** (AI-powered pilot workflows): Stories 1, 2, 3
- **ET-18** (Citizen Developer Program): Stories 4, 5, 6
- **ET-43** (BAUs): Story 7
- **ET-20** (Make AI execution visible): Story 8

---

# Critical Dependencies & Risks

**Critical Deadlines:**
- Story 4: Feb 10 (Cursor videos), Feb 12 (RFC/Cursor content), Feb 20 (Vibe + Platform AI)

**Key Dependencies:**
- Story 5 depends on Story 4 completion by Feb 12
- Story 6 depends on Story 5 completion (training first, then coaching)
- Story 8 depends on Story 4 completion for content conversion

**Cross-Team Coordination Required:**
- Cal coordinates across Stories 1, 4, 7, 8 (highest load)
- People Ops (Katelyn) and Talent (Gwynneth) partnerships for Story 1
- Jason availability for Stories 5 & 6 throughout sprint

---

**End of Sprint Plan Document**
