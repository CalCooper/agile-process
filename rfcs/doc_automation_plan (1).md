# Support-Driven Documentation Automation Plan
**Vendasta Platform Documentation Pipeline**

---

## Executive Summary

This plan outlines the implementation of an automated documentation system that transforms resolved support tickets (email & voice) into verified, Docusaurus-compliant documentation across two separate repositories (Partner-facing & SMB-facing). The system runs daily batch processing to convert support knowledge into living documentation.

**Key Components:**
- Custom Ticket Entity (in development)
- Claude Code + MCP for AI-powered analysis
- Dual Docusaurus repositories (Partners & SMBs)
- GitHub Actions orchestration
- Daily batch processing

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                     SUPPORT INTERACTION LAYER                    │
├─────────────────────────────────────────────────────────────────┤
│  Email Tickets          │  Voice Calls (Google Meet)            │
│  - Partner Center       │  - Auto-transcribed in CRM            │
│  - Thread tracking      │  - Gemini-based recording             │
└──────────────┬──────────┴───────────────┬───────────────────────┘
               │                          │
               v                          v
┌──────────────────────────────────────────────────────────────────┐
│                   TICKET ENTITY (CRM)                             │
│  - ticket_id, subject, conversation_id                           │
│  - channel (EMAIL/VOICE)                                         │
│  - stage_id (Resolved triggers documentation)                    │
│  - transcript_url, recording_url                                 │
│  - was_ai_resolved, ai_confidence                                │
└──────────────────────────┬───────────────────────────────────────┘
                           │
                           v
┌──────────────────────────────────────────────────────────────────┐
│              DAILY BATCH PROCESSOR (GitHub Action)                │
│  Scheduled: 2:00 AM daily                                        │
│  Query: All tickets with stage="Resolved" && created_at > last_run│
└──────────────────────────┬───────────────────────────────────────┘
                           │
                           v
┌──────────────────────────────────────────────────────────────────┐
│                   ARTIFACT GENERATION                             │
│  Claude Code + MCP Server                                        │
│  - Fetch ticket data via CRM API/MCP                             │
│  - Retrieve transcript (email thread or voice transcript)        │
│  - Generate structured JSON/MD artifact                          │
└──────────────────────────┬───────────────────────────────────────┘
                           │
                           v
┌──────────────────────────────────────────────────────────────────┐
│                  DOCUMENTATION ANALYSIS                           │
│  Semantic Code Indexing + Repository Analysis                    │
│  - Scan both Docusaurus repos                                    │
│  - Compare ticket content with existing docs                     │
│  - Identify: New content | Updates | Corrections                 │
└──────────────────────────┬───────────────────────────────────────┘
                           │
                           v
┌──────────────────────────────────────────────────────────────────┐
│               DOCUSAURUS FILE GENERATION                          │
│  - Generate MDX files with front matter                          │
│  - Apply correct sidebar_position and routing                    │
│  - Create _category_.json if needed                              │
│  - Split updates: Partners repo vs SMB repo                      │
└──────────────────────────┬───────────────────────────────────────┘
                           │
                           v
┌──────────────────────────────────────────────────────────────────┐
│                    BRANCH & PR CREATION                           │
│  Create separate branches/PRs for each repo:                     │
│  - vendasta/partner-docs                                         │
│  - vendasta/smb-docs                                             │
└──────────────────────────┬───────────────────────────────────────┘
                           │
                           v
┌──────────────────────────────────────────────────────────────────┐
│                  HUMAN REVIEW & APPROVAL                          │
│  AI Confidence-Based Routing:                                    │
│  - 90-100%: Knowledge Manager review                             │
│  - 70-89%: Product Manager/Technical Writer review               │
│  - <70%: Knowledge Manager + Engineering review                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Phase 1: Foundation Setup (Weeks 1-2)

### 1.1 Ticket Entity API Requirements

**CRITICAL QUESTIONS TO ANSWER:**

#### Ticket Data Access
- [ ] **Question:** Does the custom ticketing system expose a REST/GraphQL API for querying tickets?
  - **Needed for:** Daily batch processor to fetch resolved tickets
  - **Alternative:** Build webhook listener if API isn't ready

- [ ] **Question:** Can we filter tickets by `stage_id="Resolved"` and `created_at` or `updated_at` timestamp?
  - **Needed for:** Incremental batch processing (only new tickets since last run)
  
- [ ] **Question:** What authentication method will the ticket API use?
  - **Options:** API key, OAuth, service account
  - **Action:** Store credentials in GitHub Secrets

#### Transcript Access
- [ ] **Question:** Are Google Meet transcripts accessible via API from the CRM?
  - **Needed for:** Programmatic transcript retrieval
  - **Fields to verify:** `transcript_url` field in Ticket entity

- [ ] **Question:** Are transcripts stored as:
  - **Structured JSON** (preferred - includes speaker labels, timestamps)
  - **Plain text** (requires additional parsing)
  - **URL pointer** to cloud storage (requires separate fetch)

- [ ] **Question:** For email tickets, is the full thread history accessible, or just individual messages?
  - **Needed for:** Context preservation in documentation

#### Data Structure Validation
- [ ] **Question:** Confirm the Ticket entity fields match the PDF specification
- [ ] **Question:** Are `custom_fields` stored as JSON blob or separate table?
- [ ] **Question:** How are Activity associations linked (for accessing call recordings)?

### 1.2 MCP Server for Ticket Data

**Objective:** Build a Model Context Protocol server to allow Claude Code to query ticket data naturally.

**Implementation Options:**

#### Option A: Custom MCP Server (Go-based)
```go
// pkg/mcp/ticket_server.go
type TicketMCPServer struct {
    crmClient *crm.Client
}

func (s *TicketMCPServer) ListTools() []Tool {
    return []Tool{
        {
            Name: "query_resolved_tickets",
            Description: "Fetch all resolved tickets since last run",
            InputSchema: {
                "since": "timestamp",
                "channel": "EMAIL or VOICE",
                "limit": "number"
            }
        },
        {
            Name: "get_ticket_details",
            Description: "Get full ticket including transcript",
            InputSchema: {
                "ticket_id": "string"
            }
        },
        {
            Name: "get_transcript",
            Description: "Fetch transcript/conversation history",
            InputSchema: {
                "ticket_id": "string"
            }
        }
    }
}
```

**Deployment:**
- Host as internal service (likely on same infrastructure as CRM)
- Expose via SSE (Server-Sent Events) for Claude Code to connect
- Configure in Claude Code's MCP settings

#### Option B: Direct API Integration (No MCP Server)
- If ticket API is simple REST, Claude Code can call directly
- Store API credentials in GitHub Secrets
- Use `web_fetch` tool within Claude Code to query endpoints

**Recommendation:** Start with Option B for MVP speed, migrate to Option A for better developer experience.

### 1.3 GitHub Repository Setup

**Partner Documentation Repo:** `vendasta/partner-docs`
**SMB Documentation Repo:** `vendasta/smb-docs`

**Required Setup for Both Repos:**

```yaml
# .github/workflows/docs-automation.yml
name: Daily Documentation Update

on:
  schedule:
    - cron: '0 6 0 * *'  # 2:00 AM daily (UTC-4 Saskatchewan time = 6 AM UTC)
  workflow_dispatch:  # Manual trigger for testing

permissions:
  contents: write
  pull-requests: write
  issues: read

jobs:
  generate-docs:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Install Claude Code
        run: |
          npm install -g @anthropic-ai/claude-code
      
      - name: Setup MCP Configuration
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
          TICKET_API_KEY: ${{ secrets.TICKET_API_KEY }}
          TICKET_API_URL: ${{ secrets.TICKET_API_URL }}
        run: |
          # Configure MCP servers for ticket access
          # See Phase 2 for full implementation
      
      - name: Run Documentation Agent
        run: |
          claude-code --agent .claude/agents/docusaurus-expert.json
      
      - name: Create Pull Request
        uses: peter-evans/create-pull-request@v5
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          branch: docs/automated-update-${{ github.run_id }}
          title: "📚 Automated Documentation Update - ${{ github.run_id }}"
          body: |
            ## Automated Documentation Update
            
            Generated from resolved support tickets processed on ${{ github.run_time }}.
            
            **Confidence Score:** [To be populated by agent]
            **Tickets Processed:** [To be populated by agent]
            **Changes:** [To be populated by agent]
            
            ---
            
            ### Review Guidelines
            - [ ] Check for PII/sensitive data
            - [ ] Verify technical accuracy
            - [ ] Confirm appropriate repo (Partner vs SMB)
            - [ ] Test Docusaurus build locally
          labels: documentation, automated
          reviewers: knowledge-manager-team
```

**Additional Files to Create:**

```
.claude/
├── agents/
│   └── docusaurus-expert.json
├── prompts/
│   ├── ticket-to-markdown.md
│   └── documentation-analysis.md
└── config/
    └── mcp-servers.json

docs/
├── CLAUDE.md              # Tier 1: Master context
├── troubleshooting/
│   └── CONTEXT.md         # Tier 2: Component context
└── api-reference/
    └── CONTEXT.md         # Tier 2: Component context
```

### 1.4 Claude Code Installation & Setup

**On Development Machine:**
```bash
# Install Claude Code
npm install -g @anthropic-ai/claude-code

# Configure API key
export ANTHROPIC_API_KEY="your-key-here"

# Initialize workspace
cd vendasta/partner-docs
claude-code init
```

**Configure MCP Servers:**
```json
// .claude/config/mcp-servers.json
{
  "mcpServers": {
    "ticket-api": {
      "type": "url",
      "url": "https://your-ticket-api.vendasta.com/mcp/sse",
      "name": "vendasta-ticket-api"
    },
    "crm-api": {
      "type": "url", 
      "url": "https://your-crm-api.vendasta.com/mcp/sse",
      "name": "vendasta-crm-api"
    }
  }
}
```

---

## Phase 2: Artifact Generation Pipeline (Weeks 3-4)

### 2.1 Ticket Data Extraction

**Goal:** Fetch all resolved tickets since last run and prepare for processing.

**Implementation:**

```javascript
// .claude/scripts/fetch-tickets.js
const LAST_RUN_TIMESTAMP = process.env.LAST_RUN || getLastRunFromGitCommit();

async function fetchResolvedTickets() {
  const response = await fetch(`${TICKET_API_URL}/tickets`, {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${TICKET_API_KEY}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      filters: {
        stage_id: 'RESOLVED',
        updated_at: { $gte: LAST_RUN_TIMESTAMP }
      },
      include: ['transcript', 'activities', 'custom_fields']
    })
  });
  
  return response.json();
}
```

**Alternative: Using MCP Server**
```
Claude Code command:
> List all resolved tickets since 2024-02-11T00:00:00Z with channel EMAIL or VOICE
```

### 2.2 Structured Artifact Generation

**Format:** JSON (for programmatic processing) + Markdown (for human review)

**Artifact Structure:**

```json
{
  "ticket_id": "TicketID-abc123",
  "created_at": "2024-02-11T10:30:00Z",
  "channel": "EMAIL",
  "subject": "Unable to connect white-label domain",
  "category": "Technical",
  "priority": "HIGH",
  "customer_segment": "partner",  // or "smb"
  "resolution_summary": "Customer needed to update DNS CNAME record...",
  "technical_context": {
    "affected_system": "White Label Manager",
    "error_codes": ["DNS_RESOLUTION_FAILED"],
    "resolution_steps": [
      "Verified domain ownership in Partner Center",
      "Instructed to add CNAME: domains.vendasta.com",
      "Waited 24h for DNS propagation"
    ]
  },
  "documentation_action": "CREATE_NEW", // or "UPDATE_EXISTING", "VERIFY_CORRECT"
  "target_repo": "partner-docs",
  "suggested_location": "docs/troubleshooting/white-label-domains.mdx",
  "confidence_score": 0.87,
  "pii_sanitized": true,
  "original_transcript": "[SANITIZED TRANSCRIPT]",
  "code_references": [
    {
      "file": "services/white-label/dns_validator.go",
      "line_range": "45-67",
      "relevance": "DNS validation logic"
    }
  ]
}
```

**Claude Code Prompt Template:**

```markdown
# Ticket to Documentation Artifact Prompt

You are a Technical Documentation Specialist analyzing resolved support tickets to generate structured documentation artifacts.

## Input Data
<ticket>
${TICKET_DATA}
</ticket>

<transcript>
${TRANSCRIPT_OR_EMAIL_THREAD}
</transcript>

## Your Task
1. **Analyze the ticket and transcript** to identify:
   - The customer's original problem (symptom)
   - The root cause identified by support
   - The resolution steps provided
   - Whether this is a recurring issue or one-off

2. **Determine customer segment:**
   - Partners: Resellers using platform to serve SMBs
   - SMBs: Direct business owner customers
   
3. **Search existing documentation** in the appropriate repo:
   - Use semantic search to find related content
   - Determine if this is NEW content or UPDATE to existing

4. **Generate the artifact JSON** with:
   - Clear resolution summary (2-3 sentences)
   - Step-by-step technical instructions
   - Code references (if applicable)
   - Confidence score (0.0-1.0) based on:
     * Clarity of resolution (0.3)
     * Technical accuracy verified against code (0.4)
     * Generalizability to other customers (0.3)

5. **Sanitize ALL PII:**
   - Remove customer names, email addresses, phone numbers
   - Remove internal employee names
   - Replace with generic placeholders: [PARTNER_NAME], [CUSTOMER_EMAIL]

## Output Format
Return ONLY valid JSON matching the artifact schema above.
```

### 2.3 Batch Processing Logic

**Daily Batch Runner:**

```python
# .claude/scripts/batch_processor.py
import json
from datetime import datetime, timedelta

def process_daily_batch():
    # 1. Fetch all resolved tickets since last run
    tickets = fetch_resolved_tickets(since=get_last_run_timestamp())
    
    artifacts = []
    for ticket in tickets:
        # 2. Generate artifact for each ticket
        artifact = generate_artifact(ticket)
        artifacts.append(artifact)
    
    # 3. Group by target repo and confidence
    partner_docs = [a for a in artifacts if a['target_repo'] == 'partner-docs']
    smb_docs = [a for a in artifacts if a['target_repo'] == 'smb-docs']
    
    # 4. Save artifacts to temp storage
    save_artifacts('partner-docs-artifacts.json', partner_docs)
    save_artifacts('smb-docs-artifacts.json', smb_docs)
    
    # 5. Update last run timestamp
    update_last_run_timestamp(datetime.now())
    
    return {
        'partner_count': len(partner_docs),
        'smb_count': len(smb_docs),
        'avg_confidence': sum(a['confidence_score'] for a in artifacts) / len(artifacts)
    }
```

---

## Phase 3: Documentation Analysis & Generation (Weeks 5-6)

### 3.1 Semantic Code Indexing

**Objective:** Link documentation updates to actual product code to ensure technical accuracy.

**Tools:**
- **claude-context** (MCP plugin for semantic code search)
- **Vector database** (optional for large repos)

**Implementation:**

```bash
# Index the Galaxy platform repository
cd /path/to/galaxy-repo
claude-context index --output .claude/code-index

# Make index available to Claude Code
export CLAUDE_CONTEXT_INDEX=/path/to/galaxy-repo/.claude/code-index
```

**Usage in Documentation Agent:**

```
Claude Code command:
> Search the Galaxy codebase for "DNS validation" and "white label domain"
> Find the functions responsible for CNAME verification
> Verify if the resolution steps match the current implementation
```

**Verification Logic:**

```markdown
## Code Verification Prompt

Given this resolution from the support ticket:
<resolution>
${ARTIFACT.resolution_summary}
</resolution>

1. Search the codebase for related functionality
2. Extract the relevant code snippet
3. Verify if the resolution steps are technically accurate
4. Flag any discrepancies between ticket resolution and code
5. Update confidence score accordingly

If code verification fails, mark artifact as requiring engineering review.
```

### 3.2 Existing Documentation Comparison

**Objective:** Determine if content already exists and whether to create new or update existing.

**Process:**

```markdown
## Documentation Analysis Prompt

You have generated an artifact for ticket ${TICKET_ID}.

Now analyze the existing Docusaurus repository:

1. **Search for similar content:**
   - Query: "${ARTIFACT.subject}"
   - Look in: docs/troubleshooting/, docs/guides/, docs/api-reference/
   
2. **For each match found:**
   - Calculate similarity score (0-1)
   - Determine if this is:
     * **Duplicate** (>0.85 similarity): Mark as VERIFY_CORRECT
     * **Related** (0.5-0.85): Mark as UPDATE_EXISTING
     * **Unique** (<0.5): Mark as CREATE_NEW

3. **If UPDATE_EXISTING:**
   - Identify specific sections to update
   - Preserve existing structure and tone
   - Add new information without duplicating

4. **If CREATE_NEW:**
   - Determine appropriate location in docs hierarchy
   - Generate sidebar_position based on priority
   - Create _category_.json if new section needed

Output updated artifact with:
- action: CREATE_NEW | UPDATE_EXISTING | VERIFY_CORRECT
- target_file: path/to/file.mdx
- update_sections: [list of sections to update] (if applicable)
```

### 3.3 Docusaurus MDX Generation

**Template for New Documentation:**

```markdown
---
id: troubleshooting-white-label-dns
title: Troubleshooting White Label Domain DNS Issues
description: Resolve common DNS configuration issues when connecting white label domains
sidebar_label: White Label DNS Issues
sidebar_position: 3
slug: /troubleshooting/white-label-dns
tags:
  - troubleshooting
  - white-label
  - dns
  - partners
---

# Troubleshooting White Label Domain DNS Issues

## Problem
Customers attempting to connect a white label domain receive a DNS resolution error or the domain fails to verify in Partner Center.

## Common Causes
1. **CNAME record not configured correctly**
   - The CNAME must point to `domains.vendasta.com`
   - Ensure there are no conflicting A records

2. **DNS propagation delay**
   - Changes can take 24-48 hours to propagate 