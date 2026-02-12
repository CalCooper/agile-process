# RFC: Support-Driven Docs Automation (Bottom-Up)
**Submitted by:** [To be filled]
**Impact Score:** [To be filled] | **Scale:** System | **Frequency:** Daily

## 1. Problem Statement

Support tickets (email and voice) contain valuable knowledge that resolves customer issues, but this knowledge remains trapped in individual ticket resolutions and is not systematically converted into living documentation. When similar issues arise, support agents must rediscover solutions or customers face repeated problems.

**Who is affected:**
- **Support Team** - Repeatedly solving the same issues without documentation to reference
- **Customers** - Experiencing delays when support must research solutions that were previously resolved
- **Product Managers** - Missing visibility into common customer pain points and resolutions
- **Knowledge Managers** - Struggling to keep documentation current as product evolves
- **Partners & SMBs** - Unable to self-serve due to outdated or missing documentation

**Impact:**
- Support tickets resolved daily contain reusable knowledge that is not captured
- Documentation gaps lead to longer resolution times for recurring issues
- Knowledge silos prevent scaling support operations efficiently
- Two separate documentation repositories (Partner-facing & SMB-facing) require manual maintenance

**Frequency:** Daily - tickets are resolved continuously, creating a constant stream of potential documentation updates that currently go unprocessed.

## 2. Context & Goals

**Context:** Vendasta maintains two Docusaurus documentation repositories (`vendasta/partner-docs` and `vendasta/smb-docs`) that require regular updates as the platform evolves. Support interactions (email tickets and voice calls) generate resolution knowledge that should flow into these repositories, but today this process is manual and inconsistent. The custom Ticket Entity in the CRM captures resolved tickets with transcripts, but there is no automated pipeline to convert this knowledge into verified, Docusaurus-compliant documentation.

**Goals:**
1. **Automate documentation generation** - Convert resolved support tickets into Docusaurus MDX files daily without manual intervention
2. **Reduce documentation lag** - Transform ticket knowledge into published docs within 24 hours of resolution (vs. weeks/months currently)
3. **Improve documentation accuracy** - Verify technical accuracy by linking ticket resolutions to actual product code via semantic code indexing
4. **Scale knowledge capture** - Process all resolved tickets daily (estimated 50-200 tickets/day) without requiring proportional increase in documentation team effort
5. **Route to correct repository** - Automatically determine whether content belongs in Partner-docs or SMB-docs based on customer segment

## 3. Personas & User Stories

**Primary Personas:**
- **Knowledge Manager** - Responsible for maintaining documentation quality and accuracy
- **Product Manager** - Needs visibility into customer issues and resolutions
- **Support Agent** - Benefits from having documentation to reference for common issues

**User Stories:**

- **As a Knowledge Manager**, I can review AI-generated documentation updates in pull requests so that I can verify accuracy and approve publication without manually writing every article.

- **As a Knowledge Manager**, I can see confidence scores on generated documentation so that I know which items need more thorough review vs. which can be quickly approved.

- **As a Product Manager**, I can see documentation generated from support tickets so that I understand common customer pain points and can prioritize product improvements.

- **As a Support Agent**, I can reference up-to-date troubleshooting documentation so that I can resolve customer issues faster without rediscovering solutions.

- **As a Customer (Partner or SMB)**, I can find accurate, current documentation so that I can self-serve common issues without contacting support.

## 4. User Flows

**Primary Flow: Automated Daily Documentation Generation**

1. **Daily Batch Trigger** - GitHub Action runs at 2:00 AM daily (scheduled cron job)

2. **Ticket Discovery** - System queries CRM Ticket Entity API for all tickets with:
   - `stage_id = "Resolved"`
   - `created_at` or `updated_at` > last run timestamp
   - `channel` = EMAIL or VOICE

3. **Transcript Retrieval** - For each resolved ticket:
   - If EMAIL: Fetch full email thread history
   - If VOICE: Retrieve Google Meet transcript (stored in CRM via Gemini-based recording)

4. **Artifact Generation** - Claude Code + MCP Server processes each ticket:
   - Analyzes ticket subject, transcript, and resolution
   - Determines customer segment (Partner vs SMB)
   - Generates structured JSON artifact with resolution summary, technical steps, and metadata

5. **Documentation Analysis** - System analyzes existing Docusaurus repositories:
   - Performs semantic search to find related content
   - Determines action: CREATE_NEW, UPDATE_EXISTING, or VERIFY_CORRECT
   - Verifies technical accuracy by searching product codebase

6. **MDX File Generation** - Claude Code generates Docusaurus-compliant MDX files:
   - Creates files with proper front matter (sidebar_position, tags, routing)
   - Generates _category_.json files if new sections needed
   - Splits content appropriately between Partner-docs and SMB-docs repos

7. **Pull Request Creation** - System creates separate branches and PRs:
   - One PR per repository (partner-docs and smb-docs)
   - PR includes confidence scores, ticket IDs processed, and change summary
   - Labels PR with "documentation" and "automated" tags

8. **Human Review** - Based on confidence score routing:
   - **90-100% confidence:** Knowledge Manager review only
   - **70-89% confidence:** Product Manager or Technical Writer review
   - **<70% confidence:** Knowledge Manager + Engineering review

9. **Approval & Merge** - Reviewer approves PR, documentation is published to production

**Alternative Flow: Manual Trigger**
- Knowledge Manager can manually trigger workflow via GitHub Actions `workflow_dispatch`
- Useful for testing or processing specific date ranges

## 5. Technical Requirements

**Systems Accessed:**
- **CRM Ticket Entity API** - Custom ticketing system (REST or GraphQL API)
  - Endpoint: `/tickets` (query resolved tickets)
  - Endpoint: `/tickets/{id}` (get full ticket details)
  - Endpoint: `/tickets/{id}/transcript` (retrieve email thread or voice transcript)
- **Google Meet/Gemini API** - For voice call transcript storage (already integrated in CRM)
- **GitHub API** - For repository operations (create branches, PRs, commits)
  - Repositories: `vendasta/partner-docs` and `vendasta/smb-docs`
- **Claude Code** - AI agent for artifact generation and documentation creation
- **MCP Server (Atlassian)** - Model Context Protocol server for ticket data access
- **Semantic Code Index** - For verifying technical accuracy against product codebase

**Data Requirements:**
- **Read:**
  - Ticket metadata: `ticket_id`, `subject`, `conversation_id`, `channel`, `stage_id`, `created_at`, `updated_at`
  - Ticket transcripts: Full email thread history or voice call transcript
  - Ticket custom fields: `customer_segment`, `was_ai_resolved`, `ai_confidence`
  - Existing Docusaurus documentation files (for comparison)
  - Product codebase (for technical verification)
- **Write:**
  - New MDX files in Docusaurus repositories
  - Updated MDX files (when updating existing documentation)
  - `_category_.json` files (when creating new documentation sections)
  - GitHub branches and pull requests
  - Artifact JSON files (temporary storage for batch processing)
- **Transform:**
  - Support ticket transcripts → Structured JSON artifacts
  - JSON artifacts → Docusaurus MDX files with front matter
  - Raw resolution steps → Formatted troubleshooting guides
  - Customer-specific details → Generic, reusable documentation
- **PII/Sensitivity:**
  - **CRITICAL:** All customer PII must be sanitized (names, emails, phone numbers)
  - Internal employee names must be removed
  - Replace with generic placeholders: `[PARTNER_NAME]`, `[CUSTOMER_EMAIL]`
  - Sanitization verified before PR creation

**Permissions:**
- **CRM API Access:**
  - Service account with read access to Ticket Entity
  - API key or OAuth token (stored in GitHub Secrets)
  - Permission to query tickets filtered by stage and date
  - Permission to retrieve transcripts
- **GitHub Repository Access:**
  - GitHub App or Personal Access Token with:
    - `contents: write` (create/update files)
    - `pull-requests: write` (create PRs)
    - `issues: read` (for linking tickets)
  - Access to both `vendasta/partner-docs` and `vendasta/smb-docs` repositories
- **Claude API:**
  - Anthropic API key (stored in GitHub Secrets)
  - Access to Claude Code agent capabilities
- **MCP Server:**
  - Network access to MCP server endpoint (SSE connection)
  - Authentication credentials for ticket API access

**Input → Processing → Output:**

**Input:**
- Resolved support tickets (filtered by `stage_id="Resolved"` and timestamp > last run)
- Ticket transcripts (email threads or voice call transcripts)
- Existing Docusaurus documentation files
- Product codebase (for semantic code indexing)

**Processing:**
1. Fetch resolved tickets from CRM API via MCP Server
2. For each ticket:
   - Retrieve full transcript (email or voice)
   - Analyze ticket content to extract problem, root cause, resolution steps
   - Determine customer segment (Partner vs SMB)
   - Generate structured JSON artifact with:
     - Resolution summary
     - Technical context (affected systems, error codes)
     - Step-by-step resolution instructions
     - Confidence score (0.0-1.0)
     - Suggested documentation location
   - Sanitize all PII from transcript
3. Semantic analysis of existing documentation:
   - Search both Docusaurus repos for similar content
   - Calculate similarity scores
   - Determine action: CREATE_NEW, UPDATE_EXISTING, or VERIFY_CORRECT
4. Code verification:
   - Search product codebase for related functionality
   - Verify resolution steps match current implementation
   - Adjust confidence score based on technical accuracy
5. Generate Docusaurus MDX files:
   - Apply correct front matter (id, title, sidebar_position, tags)
   - Format content according to Docusaurus standards
   - Create appropriate file structure
6. Group artifacts by target repository
7. Create GitHub branches and pull requests

**Output:**
- Pull requests in `vendasta/partner-docs` repository (for Partner-facing content)
- Pull requests in `vendasta/smb-docs` repository (for SMB-facing content)
- Each PR contains:
  - Generated/updated MDX files
  - PR description with confidence scores and ticket IDs
  - Labels for automated routing
  - Reviewers assigned based on confidence thresholds

**Integration Points:**
- **CRM Ticket Entity** → MCP Server → Claude Code (ticket data flow)
- **GitHub Actions** → Claude Code agent (orchestration)
- **Claude Code** → GitHub API (PR creation)
- **Semantic Code Index** → Claude Code (technical verification)
- **Docusaurus Repos** → Claude Code (documentation analysis)

**Limits and Expectations:**
- **Batch Processing:** Daily run processes all tickets resolved since last run (estimated 50-200 tickets/day)
- **API Rate Limits:**
  - CRM API: [To be determined - need to verify with CRM team]
  - GitHub API: 5,000 requests/hour (should be sufficient for daily batch)
  - Claude API: Based on token usage (estimated 10K-50K tokens per ticket)
- **Processing Time:** 
  - Target: Complete batch processing within 2-4 hours
  - Individual ticket processing: 30-60 seconds per ticket
- **Confidence Score Thresholds:**
  - High confidence (90-100%): Auto-approve after Knowledge Manager review
  - Medium confidence (70-89%): Requires Product Manager/Technical Writer review
  - Low confidence (<70%): Requires Engineering + Knowledge Manager review
- **Data Volume:**
  - Email transcripts: 1-10 KB per ticket
  - Voice transcripts: 5-50 KB per ticket
  - Generated MDX files: 2-20 KB per documentation article

## 6. Implementation

The solution will be implemented in three phases over 6 weeks:

**Phase 1: Foundation Setup (Weeks 1-2)**

1. **Ticket Entity API Integration**
   - Verify CRM Ticket Entity exposes REST/GraphQL API for querying resolved tickets
   - Confirm ability to filter by `stage_id="Resolved"` and timestamp ranges
   - Establish authentication method (API key, OAuth, or service account)
   - Validate transcript access (email threads and Google Meet transcripts)
   - Store credentials in GitHub Secrets

2. **MCP Server Setup**
   - **Option A (Recommended for MVP):** Direct API integration - Claude Code calls CRM API directly using `web_fetch` tool
   - **Option B (Future enhancement):** Build custom Go-based MCP Server to provide natural language ticket queries
   - Configure MCP server connection in Claude Code settings
   - Test ticket data retrieval via MCP

3. **GitHub Repository Configuration**
   - Set up GitHub Actions workflow in both `partner-docs` and `smb-docs` repositories
   - Configure scheduled trigger (daily at 2:00 AM)
   - Set up manual trigger option for testing
   - Configure repository permissions (contents: write, pull-requests: write)

4. **Claude Code Agent Setup**
   - Install Claude Code in GitHub Actions environment
   - Create agent configuration files (`.claude/agents/docusaurus-expert.json`)
   - Set up prompt templates for ticket-to-artifact conversion
   - Configure semantic code indexing for technical verification

**Phase 2: Artifact Generation Pipeline (Weeks 3-4)**

1. **Ticket Data Extraction**
   - Implement daily batch processor to fetch resolved tickets since last run
   - Retrieve full transcripts (email or voice) for each ticket
   - Store last run timestamp (in Git commit or external storage)

2. **Structured Artifact Generation**
   - Claude Code processes each ticket transcript
   - Generates JSON artifact with:
     - Ticket metadata and customer segment
     - Resolution summary and technical context
     - Step-by-step instructions
     - Confidence score calculation
     - Suggested documentation location
   - Sanitizes all PII from transcripts

3. **Batch Processing Logic**
   - Process all tickets in batch
   - Group artifacts by target repository (Partner vs SMB)
   - Save artifacts to temporary storage for review
   - Update last run timestamp

**Phase 3: Documentation Analysis & Generation (Weeks 5-6)**

1. **Semantic Documentation Analysis**
   - Claude Code searches existing Docusaurus repositories
   - Compares ticket content with existing documentation
   - Determines action: CREATE_NEW, UPDATE_EXISTING, or VERIFY_CORRECT
   - Calculates similarity scores

2. **Code Verification**
   - Semantic code indexing searches product codebase
   - Verifies resolution steps match current implementation
   - Flags discrepancies for engineering review
   - Adjusts confidence scores based on technical accuracy

3. **Docusaurus MDX Generation**
   - Claude Code generates MDX files with proper front matter
   - Applies correct `sidebar_position` and routing
   - Creates `_category_.json` files when needed
   - Formats content according to Docusaurus standards

4. **Pull Request Creation**
   - Creates separate branches for each repository
   - Generates PRs with confidence scores and ticket metadata
   - Assigns reviewers based on confidence thresholds
   - Adds appropriate labels and descriptions

**Architecture Overview:**
```
Support Tickets (Email/Voice) 
  → CRM Ticket Entity 
  → Daily Batch Processor (GitHub Action)
  → Claude Code + MCP Server (Artifact Generation)
  → Documentation Analysis (Semantic Search + Code Verification)
  → Docusaurus MDX Generation
  → GitHub Pull Requests
  → Human Review & Approval
  → Published Documentation
```

## 7. Alternatives Considered

**Alternative 1: Manual Documentation Process with AI Assistance**
- **Approach:** Support agents use AI tools (like Claude) to draft documentation, then Knowledge Managers review and publish manually
- **Why rejected:** Still requires manual coordination, doesn't scale to process all resolved tickets, creates bottleneck at Knowledge Manager review stage, doesn't use existing ticket data systematically

**Alternative 2: Third-Party Documentation Platform**
- **Approach:** Use vendor solution (like Zendesk Guide, Intercom Articles) that integrates with support tickets
- **Why rejected:** Would require migrating away from Docusaurus (significant effort), vendor lock-in, may not support dual repository structure (Partner vs SMB), higher ongoing costs, less control over documentation format and structure

**Alternative 3: Separate Tool Per Team**
- **Approach:** Each team (Support, Product, Engineering) builds their own documentation automation
- **Why rejected:** Duplicates logic and effort, misses integration opportunities, creates inconsistent documentation formats, harder to maintain and scale

**Alternative 4: Webhook-Based Real-Time Processing**
- **Approach:** Process tickets immediately when resolved via webhook, rather than daily batch
- **Why not chosen:** Daily batch is preferred because:
  - Allows batching API calls (more efficient)
  - Reduces risk of processing incomplete resolutions
  - Gives time for support agents to add final notes
  - Easier to monitor and debug batch processing
  - Can be enhanced to real-time later if needed

**Chosen Approach Rationale:**
The automated daily batch processing with Claude Code + MCP Server provides the best balance of automation, accuracy, and maintainability. It uses existing ticket data without requiring manual intervention, scales to process all resolved tickets, maintains Docusaurus as the documentation platform, and includes confidence-based routing to ensure quality.

## 8. Risks and Dependencies

**Technical Risks:**

1. **CRM API Availability and Rate Limits**
   - **Risk:** Ticket Entity API may not be ready or may have restrictive rate limits
   - **Mitigation:** Verify API availability in Phase 1, implement retry logic and rate limiting in batch processor, consider webhook fallback if API is delayed

2. **Transcript Quality and Format Inconsistency**
   - **Risk:** Email threads and voice transcripts may vary in format, making extraction unreliable
   - **Mitigation:** Build reliable parsing logic, test with diverse ticket samples, implement fallback to manual review for low-confidence extractions

3. **PII Sanitization Failures**
   - **Risk:** Customer PII may leak into published documentation
   - **Mitigation:** Multiple sanitization passes, automated PII detection, mandatory human review for all PRs, implement pre-commit hooks to flag potential PII

4. **Technical Accuracy Verification**
   - **Risk:** AI-generated documentation may not match actual product behavior
   - **Mitigation:** Semantic code indexing to verify against codebase, confidence-based routing to Engineering review, require code references in generated docs

5. **Claude API Costs and Token Limits**
   - **Risk:** Processing 50-200 tickets/day may incur high API costs or hit rate limits
   - **Mitigation:** Monitor token usage, implement caching for similar tickets, optimize prompts to reduce token consumption, set budget alerts

6. **Documentation Duplication**
   - **Risk:** System may create duplicate documentation or fail to recognize existing content
   - **Mitigation:** Reliable semantic search, similarity scoring thresholds, manual review process to catch duplicates

**Dependencies:**

1. **CRM Team** - Must provide:
   - Ticket Entity API access (REST or GraphQL)
   - API documentation and authentication method
   - Confirmation of transcript storage format and access method
   - Timeline for API availability if not yet ready

2. **Platform/Engineering Team** - Must provide:
   - Access to product codebase for semantic code indexing
   - Code repository access permissions
   - Technical review for low-confidence documentation

3. **Knowledge Management Team** - Must provide:
   - Review and approval process
   - Documentation standards and style guide
   - Feedback on generated content quality

4. **GitHub Infrastructure** - Requires:
   - GitHub Actions minutes allocation
   - Repository access permissions
   - Ability to create branches and PRs programmatically

5. **Claude/Anthropic** - Requires:
   - API access and key
   - Sufficient rate limits and token allocation

**Open Questions:**

1. **Ticket Entity API Readiness**
   - [ ] Does the custom ticketing system expose a REST/GraphQL API for querying tickets?
   - [ ] Can we filter tickets by `stage_id="Resolved"` and timestamp?
   - [ ] What authentication method will the ticket API use?
   - [ ] Are Google Meet transcripts accessible via API from the CRM?
   - [ ] What format are transcripts stored in (JSON, plain text, URL pointer)?

2. **Data Structure**
   - [ ] Confirm Ticket entity fields match specification (ticket_id, subject, conversation_id, channel, stage_id, transcript_url, recording_url, was_ai_resolved, ai_confidence)
   - [ ] Are custom_fields stored as JSON blob or separate table?
   - [ ] How are Activity associations linked (for accessing call recordings)?

3. **Customer Segment Determination**
   - [ ] How do we reliably determine if a ticket is from a Partner vs SMB customer?
   - [ ] Is this stored in ticket custom_fields or do we need to infer from other data?

4. **Documentation Routing**
   - [ ] What criteria determine if content belongs in Partner-docs vs SMB-docs?
   - [ ] Are there edge cases where content should go to both repositories?

5. **Confidence Score Calibration**
   - [ ] What confidence thresholds are appropriate for each review level?
   - [ ] How do we validate and adjust confidence scoring over time?

6. **Monitoring and Alerting**
   - [ ] How do we monitor batch processing failures?
   - [ ] What alerts are needed if documentation generation fails?
   - [ ] How do we track documentation quality metrics over time?

## 9. Test Plan and Success Criteria

**Test Plan:**

**Phase 1 Testing (Weeks 1-2):**
1. Verify CRM Ticket Entity API access and authentication
2. Test ticket querying with various filters (stage_id, date ranges)
3. Retrieve sample email and voice transcripts
4. Validate transcript formats and parsing
5. Test MCP Server connection and ticket data retrieval
6. Verify GitHub Actions workflow can run and access repositories
7. Test Claude Code installation and agent configuration

**Phase 2 Testing (Weeks 3-4):**
1. Process 10-20 sample resolved tickets manually
2. Verify artifact JSON generation for each ticket
3. Validate PII sanitization (test with tickets containing names, emails, phone numbers)
4. Test batch processing logic with date range filtering
5. Verify last run timestamp tracking
6. Validate customer segment determination logic

**Phase 3 Testing (Weeks 5-6):**
1. Test semantic documentation search against existing Docusaurus repos
2. Verify similarity scoring and action determination (CREATE_NEW vs UPDATE_EXISTING)
3. Test code verification against product codebase
4. Generate sample MDX files and validate Docusaurus compliance
5. Test PR creation in both repositories
6. Verify confidence score routing to appropriate reviewers
7. End-to-end test: Process tickets → Generate docs → Create PRs → Review → Merge

**Production Validation:**
1. Run daily batch for 1 week with manual review of all outputs
2. Compare AI-generated docs with manually written equivalents
3. Measure processing time and API usage
4. Collect feedback from Knowledge Managers on content quality
5. Monitor PR approval rates and reviewer feedback

**Success Criteria:**

1. **Automation Coverage**
   - ✅ System processes 100% of resolved tickets daily (no manual ticket selection needed)
   - ✅ Batch processing completes within 4 hours for typical daily volume (50-200 tickets)

2. **Documentation Quality**
   - ✅ 80%+ of generated documentation receives approval with minimal edits
   - ✅ PII sanitization: 0 instances of customer PII in published documentation
   - ✅ Technical accuracy: 90%+ of code-verified documentation matches actual product behavior

3. **Efficiency Gains**
   - ✅ Reduce Knowledge Manager time spent writing documentation by 60%+
   - ✅ Documentation published within 24-48 hours of ticket resolution (vs. weeks currently)
   - ✅ Support team reports improved access to current troubleshooting guides

4. **Repository Management**
   - ✅ Content correctly routed to Partner-docs vs SMB-docs (95%+ accuracy)
   - ✅ No duplicate documentation created (similarity detection working)
   - ✅ Existing documentation updated appropriately when new information available

5. **System Reliability**
   - ✅ Daily batch processing success rate: 95%+ (allows for occasional API failures)
   - ✅ Failed tickets automatically flagged for manual review
   - ✅ Monitoring and alerting in place for processing failures

**Validation Approach:**

- **Manual Review:** All generated PRs reviewed by Knowledge Managers initially
- **Automated Testing:** Unit tests for PII sanitization, MDX format validation, API integration
- **User Feedback:** Surveys to Support team and Knowledge Managers on documentation usefulness
- **Metrics Tracking:** Dashboard showing tickets processed, docs generated, approval rates, confidence scores

**Monitoring:**

- **Daily Metrics:**
  - Number of tickets processed
  - Number of documentation articles generated/updated
  - Average confidence scores
  - PR creation and approval rates
  - Processing time and API usage

- **Weekly Reviews:**
  - Content quality assessment
  - False positive/negative rates for similarity detection
  - Customer segment routing accuracy
  - Engineering review requests (low confidence items)

- **Alerts:**
  - Batch processing failures
  - API rate limit warnings
  - Unusually low confidence scores
  - PII detection in generated content

## Validation Checklist

Before submitting the RFC, verify:
- [x] All 9 sections are present and in order
- [x] Section 5 (Technical Requirements) is explicit and detailed
- [x] No AI slop ("delve", "seamlessly", "robust", "leverage")
- [x] Written for non-engineer readability
- [x] Concrete and specific (no vague statements)
- [x] Open questions and risks are called out
- [ ] Placeholders used where information is missing (Submitted by, Impact Score to be filled)
