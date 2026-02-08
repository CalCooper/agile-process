> **Note:** The first draft of this documentation was created with AI from the workflow submission your team created. Please delete this callout after human review from workflow owner(s).

# RFC: TASK / Appointments Confirmations/ Reminders
**Submitted by:** Siuly Balza (Sales)  
**Impact Score:** 5 | **Scale:** Workflow | **Frequency:** Per Transaction | **Weekly Hours:** 40 | **Annual Hours Savings:** 2,080

## 1. Problem Statement
Scheduling agents spend 40 hours/week manually reminding and confirming appointments. The flow today: BookMeNow schedules the appointment and syncs to Google Calendar and CRM, but the CRM cannot update meeting status. The team manually creates a new meeting record just to enable status updates. Then agents call customers at 24 hours and 1 hour before the appointment using Kixie, leave voicemails, and send email/SMS via the CRM. Fifteen minutes before the appointment, agents call again. This is repetitive, time-consuming, and does not scale.
**Who is affected:** Scheduling department, AEs/AMs, customers waiting for confirmation.
**Impact:** 40 hours/week (2,080 hours/year). Per-transaction workload; every appointment triggers multiple manual touchpoints. Customer experience suffers when replies are slow or status is unclear.

## 2. Context & Goals
**Context:** Reliable appointment confirmation reduces no-shows and improves sales efficiency. Customers expect email/SMS reminders and easy ways to confirm or reschedule.
**Goals:**
1. CRM sends email and SMS 24 hours before the appointment to remind the customer.
2. One hour before the appointment, system sends another email and SMS to confirm attendance for the call with the AE/AM.
3. If customer replies "1" to confirm, status automatically updates to CONFIRMED (no scheduling call needed). If "2" to reschedule, status updates to NO SHOW and agents contact customer to reschedule.
4. At end of day (5:00 PM / 6:00 PM), all NO SHOW appointments receive email and SMS inviting them to reply to get a new appointment.
5. Reduce scheduling team manual calls; free agents for higher-value work. Annual savings: 2,080 hours.

## 3. Personas & User Stories
- As a **scheduling agent**, I can rely on automated reminders and confirmation messages so that I only call when the customer has not replied or needs to reschedule.
- As an **AE/AM**, I can see CONFIRMED vs NO SHOW status in the CRM so that I know whether to join the call or follow up.
- As a **customer**, I can reply "1" or "2" to an SMS/email to confirm or reschedule so that I don’t have to answer a call.
[PLACEHOLDER: Additional user stories as needed.]

## 4. User Flows
**Current state:**
1. Scheduling: BookMeNow → syncs to Google Calendar and creates meeting in CRM (status not updateable).
2. Status update: Team manually creates a new meeting to enable status updates.
3. 24-hour reminder: Agent calls via Kixie; if no answer, voicemail + email/SMS via CRM.
4. 1-hour confirmation: Agent calls again via Kixie; if no answer, voicemail + email/SMS.
5. 15-minute follow-up: Agent calls again via Kixie.
**Target state:**
1. Scheduling: BookMeNow → Google Calendar → CRM (with updateable status).
2. 24 hours before: CRM sends email + SMS reminder automatically.
3. 1 hour before: CRM sends email + SMS confirmation request (reply 1 = confirm, 2 = reschedule).
4. Customer replies 1 → status = CONFIRMED; replies 2 → status = NO SHOW; no reply → [PLACEHOLDER: default or agent follow-up after 30–45 min].
5. End of day: All NO SHOW get email + SMS to rebook. Agents focus on outbound follow-up only when needed.

## 5. Technical Requirements
**Systems Accessed:**
- BookMeNow (scheduling)
- Google Calendar (sync)
- CRM (meetings, status, email/SMS)
- Kixie (calling – may remain for exceptions or be reduced)
**Data Requirements:**
- Read: Appointments from BookMeNow/Calendar/CRM; customer contact info; meeting time.
- Write: Meeting status (CONFIRMED, NO SHOW, etc.) in CRM; send email/SMS; [PLACEHOLDER: log replies.]
- Transform: Reply "1"/"2" (and possibly other keywords) → status update.
**Permissions:**
- [PLACEHOLDER: CRM API or integration for status write and messaging; BookMeNow/Calendar read or webhook.]
**Input → Processing → Output:**
- Input: Appointment record (time, customer, contact details); schedule triggers (24h, 1h, EOD).
- Processing: Send reminder/confirmation messages; ingest replies; map reply to status; update CRM.
- Output: Updated meeting status in CRM; sent emails/SMS; optional agent task for NO SHOW follow-up.
**Integration Points:** BookMeNow ↔ Calendar ↔ CRM; CRM ↔ email/SMS provider; [PLACEHOLDER: reply handling (SMS/email webhook or poll).]
**Limits and Expectations:** [PLACEHOLDER: Volume of appointments; SMS/email quotas; response time for status update.]

## 6. Implementation
[PLACEHOLDER: High-level approach – e.g., CRM-native automation vs middleware; how reply "1"/"2" is captured (SMS webhook, email parsing); scheduling (cron vs CRM scheduler); fallback to Kixie for no-reply cases.]

## 7. Alternatives Considered
[PLACEHOLDER: Keep full manual calling; automate only reminders but not confirmation replies; use third-party appointment reminder product.]

## 8. Risks and Dependencies
**Risks:** CRM may not support status updates or programmable messaging; reply parsing must be reliable; customers may reply in unexpected ways.
**Dependencies:** CRM and BookMeNow/Calendar integration; SOP exists (step-by-step guide) and can inform automation design. [PLACEHOLDER: Vendor or IT support for API/integration.]
**Open Questions:** [PLACEHOLDER: Exact CRM fields for status; how SMS replies are delivered to the system; compliance for automated SMS.]

## 9. Test Plan and Success Criteria
**Success Criteria:** Reminders and confirmation messages sent automatically; reply "1"/"2" updates status; reduction in manual confirmation calls; 2,080 hours/year saved; no increase in no-shows.
**Test Plan:** [PLACEHOLDER: Pilot with one scheduling queue; test reply parsing and status update; measure agent time before/after.]
**Validation:** [PLACEHOLDER: Weekly review of automation coverage and agent hours; quarterly savings validation.]