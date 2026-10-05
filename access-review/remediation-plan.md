# Remediation Plan — Meridian Payments, Inc.

**Source:** Q3 2026 Quarterly User Access Review (see findings.md)
**Prepared:** 2026-10-01
**Items:** 3 access violations + 1 systemic process gap

Actions are ordered by severity. Immediate items are addressed first; process
improvements follow once the active exposures are closed.

---

## Priority 1 — Immediate (Critical)

### Brian Hollis — terminated employee, account still active

| | |
|---|---|
| **Finding** | Offboarding failure (Finding 3) |
| **Risk** | Former employee retained and used access to the most sensitive system 19 days after termination |
| **Owner** | IT Security + IAM |
| **Target** | Same day |

**Actions:**
1. Preserve all logs associated with the account before making changes
   (evidence integrity).
2. Disable the account in full — complete deprovisioning across all systems.
3. Open an investigation into the 2026-09-20 and 2026-09-28 sessions to
   determine what was accessed or changed.
4. Report findings of the investigation to Security leadership.

---

## Priority 2 — This review cycle (Medium)

### Kevin Brooks — excess privilege

| | |
|---|---|
| **Finding** | Excess privilege (Finding 1) |
| **Risk** | Finance Analyst holding Read/Write on the Admin Console — access outside the role, widening blast radius |
| **Owner** | Admin Console system owner + IAM |
| **Target** | Within the review cycle |

**Actions:**
1. Confirm with the system owner whether the Admin Console grant had a business
   justification.
2. If justified, document the exception. If not, revoke Admin Console access.
3. Retain NetSuite access (consistent with role).

### Monica Flores — privilege creep

| | |
|---|---|
| **Finding** | Privilege creep from an incomplete Mover event (Finding 2) |
| **Risk** | Retained Operations-role access after transfer to HR; unused and unauthorized access to a sensitive system |
| **Owner** | HR + IAM |
| **Target** | Within the review cycle |

**Actions:**
1. Confirm the Operations-to-HR transfer against HR records.
2. Revoke Admin Console and Salesforce access.
3. Retain Workday access (consistent with current role).

---

## Priority 3 — Systemic (Process)

### Joiner-Mover-Leaver (JML) deprovisioning gap

Two of the three findings (Monica, Brian) trace to identity-lifecycle events
that did not fully execute — a Mover and a Leaver where deprovisioning was
missed. This is a process gap, not isolated error.

**Recommended actions:**
1. Implement automated deprovisioning triggered by the HR termination event, so
   Leaver deprovisioning fires on the termination date rather than relying on a
   manual step.
2. Add a deprovisioning checkpoint to the Mover process, so prior-role access is
   revoked at the point of transfer, not left standing.
3. Reduce the access review cycle from quarterly to monthly for privileged
   systems (Admin Console, AWS Console) until the JML automation is in place and
   verified.

---

## Tracking

| Item | Severity | Owner | Status |
|---|---|---|---|
| Brian Hollis — disable + investigate | Critical | IT Security + IAM | Open |
| Kevin Brooks — revoke Admin Console | Medium | System owner + IAM | Open |
| Monica Flores — revoke Ops access | Medium | HR + IAM | Open |
| JML deprovisioning automation | Process | IAM + IT leadership | Open |
