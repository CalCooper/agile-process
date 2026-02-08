> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# RFC: Local Development Microservice Testing
**Submitted by:** Chelsea Greenwald (R&D)  
**Impact Score:** 3 | **Scale:** Task | **Frequency:** Daily | **Weekly Hours:** 10 | **Annual Hours Savings:** 520

## 1. Problem Statement
Local testing is valuable to confirm code changes before they reach production, but local test setups for backend microservices are limited. A lot of testing is done by deploying a feature branch to the demo environment on Mission Control instead of vetting changes locally first. Local setups tend to be repo/team-dependent and are usually limited to the service being changed – for example, it’s hard to run a local business app instance that depends on a local conversation instance with feature changes. So changes are not fully vetted before deploying to demo or prod on Mission Control.
**Who is affected:** R&D engineers (backend/microservice teams), QA, release process.
**Impact:** 10 hours/week (520 hours/year) spent on workarounds and deployment-to-demo for testing. Daily frequency. Risk of bugs reaching demo/prod that could have been caught locally. Scale: Task – focused on “deploy feature branch to test/dev environment for end-to-end testing.”

## 2. Context & Goals
**Context:** Fast, reliable feedback loops depend on being able to run and test services locally. Today the gap is in local multi-service and dependency setup, not just single-service unit tests.
**Goals:**
1. Deploy feature branch to a test/dev environment for end-to-end testing (or equivalent: run a representative stack locally).
2. Enable local runs that include dependent services (e.g., local business app + local conversation instance with feature changes) so that integration is tested before demo/prod.
3. Reduce reliance on “deploy to demo to test”; shorten feedback loop and free Mission Control for higher-order testing. Annual savings: 520 hours.
4. [PLACEHOLDER: Optional – standardize local setup across repos/teams.]

## 3. Personas & User Stories
- As an **Engineer**, I can run my feature branch in a local (or dev) environment with dependent services so that I verify behavior before pushing to demo/prod.
- As an **Engineer**, I can get a consistent local test setup (or one-command dev stack) so that I don’t spend hours on repo-specific wiring.
- As a **Release owner**, I can have more changes validated locally or in dev so that demo/prod deploys are less risky.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
**Current state:** Engineer changes a microservice; local run is limited to that service or a minimal set; to test with dependent services (e.g., business app + conversation), they deploy the feature branch to demo on Mission Control. Local setups vary by repo/team.
**Target state:**
1. Engineer pushes feature branch (or runs a command).
2. [PLACEHOLDER: Option A – deploy feature branch to a dedicated test/dev environment (e.g., ephemeral or shared dev). Option B – local stack (e.g., docker-compose or script) that brings up the service + key dependencies.]
3. Engineer (or CI) runs end-to-end or integration tests against that environment.
4. Results inform “ready for demo/prod” without blocking on Mission Control for first-level testing.
[PLACEHOLDER: Choose primary path – “deploy to dev env” vs “better local stack” – and document steps.]

## 5. Technical Requirements
**Systems Accessed:**
- IDEs (developer machines)
- Mission Control (deploy to demo)
- VStore, Temporal, Firestore (backend/dependency services)
- [PLACEHOLDER: Source control and CI; container or runtime for local/dev.]
**Data Requirements:**
- Read: Feature branch and dependent repos/configs; test data or fixtures.
- Write: [PLACEHOLDER: Test results; dev environment state; no production data.]
- Transform: Branch + config → runnable stack (local or dev).
**Permissions:**
- [PLACEHOLDER: Access to Mission Control for dev environment if used; access to VStore, Temporal, Firestore for local/dev; network or sandbox constraints.]
**Input → Processing → Output:**
- Input: Feature branch (and optionally list of dependent services); trigger (manual or CI).
- Processing: Build and deploy to test/dev environment (or start local stack); run tests; collect results.
- Output: Deployed test/dev environment (or local stack) ready for E2E testing; test results; [PLACEHOLDER: link or artifact for reviewer.]
**Integration Points:** Source control → CI or local script; Mission Control (if dev env); VStore, Temporal, Firestore for service dependencies. Knowledge gap: current local setup is in people’s heads – document and/or codify in repo.
**Limits and Expectations:** [PLACEHOLDER: Resource limits for local/dev; max parallel dev envs; test run timeout.]

## 6. Implementation
[PLACEHOLDER: High-level approach – e.g., docker-compose or similar for local stack; or Mission Control pipeline for “deploy this branch to dev”; document current local setup and add runbook; optional: standardize one template across repos.]

## 7. Alternatives Considered
[PLACEHOLDER: Keep deploy-to-demo as primary test path; invest only in better docs for existing local setups; use external hosted dev environments.]

## 8. Risks and Dependencies
**Risks:** Local or dev environment may not match prod (data, config, scale); maintenance burden if many services need to be in the stack. Knowledge is currently in people’s heads – documentation is required.
**Dependencies:** Mission Control and dependency services (VStore, Temporal, Firestore) access; agreement on “test/dev environment” vs “local only.” Knowledge gap: document current local and demo deploy steps before automating further.
**Open Questions:** [PLACEHOLDER: Mission Control API for deploying branch to dev; which dependencies must be included for “representative” E2E; ownership of shared dev environment.]

## 9. Test Plan and Success Criteria
**Success Criteria:** Feature branch can be deployed to test/dev (or equivalent local stack) for E2E testing; 520 hours/year saved; fewer “only found in demo” bugs; [PLACEHOLDER: target time from branch push to test-ready.]
**Test Plan:** [PLACEHOLDER: Pilot with one team or one service; validate that key dependencies run and tests pass; measure time to test-ready before/after.]
**Validation:** [PLACEHOLDER: Usage of local/dev path; reduction in demo deploys for first-level testing; engineer satisfaction.]