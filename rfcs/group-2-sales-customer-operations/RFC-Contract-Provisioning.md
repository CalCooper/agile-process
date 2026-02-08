> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# RFC: Contract Provisioning
**Submitted by:** Tiffany Pennycook (Sales)  
**Impact Score:** 5 | **Scale:** Workflow | **Frequency:** Daily  
**Weekly Hours:** [Unknown – less about time, more about getting partners access in an automated way]

## 1. Problem Statement
When an order is signed in VMF (Vendasta Management Framework), it kicks off a VTM project with tasks. A person then manually updates pricing in the billing system and turns on the new subscription in super admin, plus other manual steps. This delays partner access to their new subscription and creates a bottleneck. The process runs daily whenever new contracts are signed.
**Who is affected:** Sales/Ops team performing provisioning, partners waiting for access, internal teams dependent on accurate billing and subscription state.
**Impact:** High impact (score 5) – automating would fundamentally improve how contracts are fulfilled. Primary pain is delay and manual handoffs, not only hours saved.

## 2. Context & Goals
**Context:** Channel contracts signed in VMF need to be reflected in billing and in the platform (subscription on in super admin) so partners can use what they bought.
**Goals:**
1. Automate the charging and provisioning of new contracts (Channel – VMF).
2. When order is signed in VMF, billing is updated and new subscription is turned on in super admin without manual steps.
3. Partners get access to their new subscription in an automated, timely way.
4. [PLACEHOLDER: Measurable goal for time from signature to provisioning.]

## 3. Personas & User Stories
- As a **Sales Ops or Billing Analyst**, I can have contract provisioning run automatically after VMF signature so that I only handle exceptions.
- As a **Partner**, I can receive access to my new subscription soon after signing so that I can start using the product.
- As a **Finance** user, I can see billing and subscription state in sync with signed contracts so that revenue and access are accurate.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
**Current state:**
1. Order signed in VMF → VTM project created with tasks.
2. Person manually updates pricing in billing system.
3. Person manually turns on new subscription in super admin.
4. Other manual steps [PLACEHOLDER: document from Loom video].
**Target state:**
1. Order signed in VMF → event or webhook triggers provisioning workflow.
2. System updates billing (pricing) and turns on subscription in super admin.
3. [PLACEHOLDER: Notifications, audit trail, exception handling.]
4. Human involvement only for exceptions or approvals where required.

## 5. Technical Requirements
**Systems Accessed:**
- VMF (contract/order signature)
- VTM (project/tasks – may trigger or be updated)
- Billing center (pricing update)
- Super admin (subscription on/off)
**Data Requirements:**
- Read: Signed order/contract from VMF (partner, products, pricing, effective date).
- Write: Billing center (pricing, charge); super admin (subscription enabled); [PLACEHOLDER: VTM task completion.]
- Transform: Contract data → billing line items and subscription entitlements.
**Permissions:**
- [PLACEHOLDER: Service account or integration credentials for VMF, billing center, super admin.]
**Input → Processing → Output:**
- Input: Order signed event from VMF (or VTM project creation); contract details.
- Processing: Map contract to billing and subscription; call billing API; call super admin API to enable subscription.
- Output: Updated billing; subscription on in super admin; [PLACEHOLDER: partner notification, audit log.]
**Integration Points:** VMF → provisioning service; provisioning service → billing center, super admin. Loom video documents current human flow and can inform integration design.
**Limits and Expectations:** [PLACEHOLDER: Volume of contracts; API rate limits; SLA from signature to live.]

## 6. Implementation
[PLACEHOLDER: High-level approach – e.g., event-driven (VMF webhook) vs polling; sequence of billing then super admin; error handling and retry; manual override for exceptions.]

## 7. Alternatives Considered
[PLACEHOLDER: Keep manual provisioning; semi-automated (system suggests, human approves); full automation with approval only for high-value or non-standard contracts.]

## 8. Risks and Dependencies
**Risks:** Billing or super admin errors could block partner access or create incorrect charges; need clear rollback or fix path. Contract edge cases (amendments, partial activation) may require rules.
**Dependencies:** VMF, billing center, and super admin integration; Loom video exists and captures current “workflow intelligence” for mapping. [PLACEHOLDER: Ownership and approval for production access.]
**Open Questions:** [PLACEHOLDER: VMF webhook or API; billing center and super admin API capabilities; which contract types are in scope.]

## 9. Test Plan and Success Criteria
**Success Criteria:** New Channel (VMF) contracts provisioned automatically; billing and subscription in sync; partners receive access without manual delay; [PLACEHOLDER: target time from signature to live.]
**Test Plan:** [PLACEHOLDER: Test with sandbox/test contracts; validate billing and subscription state; test exception paths.]
**Validation:** [PLACEHOLDER: Track time from signature to provisioning; error rate; partner feedback.]