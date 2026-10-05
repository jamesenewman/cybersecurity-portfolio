# Access Review Findings — Meridian Payments, Inc.

**Review type:** Quarterly User Access Review (UAR)
**Period:** Q3 2026
**Review date:** 2026-10-01
**Scope:** Admin Console, Salesforce, NetSuite, Workday, AWS Console
**Population reviewed:** 11 users / 17 access entries across 5 systems

## Summary

Three access violations were identified. Each is documented below with the
observed access, the authorized role baseline, the nature of the violation,
the risk it presents, and the recommended remediation. The remaining accounts
were reviewed and found consistent with their role baselines.

---

## Finding 1 — Excess Privilege

**Severity:** Medium
**User:** Kevin Brooks — Finance Analyst
**System flagged:** Admin Console (Read/Write)

**Observed:** Kevin Brooks holds Read/Write access to the Admin Console. His
NetSuite (Read/Write) access is consistent with his role.

**Baseline:** The Finance Analyst role is authorized for NetSuite (Read/Write)
only. Admin Console is not an authorized system for this role.

**Analysis:** There is no role change or transfer associated with this account.
The Admin Console access is a standalone over-grant — access beyond what the
role requires, in violation of least privilege. This is excess privilege.

**Risk:** The Admin Console is the platform's most sensitive system. A Finance
Analyst holding Read/Write access to it widens the blast radius of the account:
if it were compromised or misused, the exposure would extend to administrative
functions far outside the finance function.

**Recommendation:** Revoke Admin Console access; retain NetSuite. Confirm with
the system owner whether the grant was intentional; if a business justification
exists, document it, otherwise remove.

---

## Finding 2 — Privilege Creep

**Severity:** Medium
**User:** Monica Flores — HR Specialist
**Systems flagged:** Admin Console (Read/Write), Salesforce (Read-only)

**Observed:** Monica Flores holds Admin Console (Read/Write) and Salesforce
(Read-only) in addition to Workday (Read/Write). Her Workday access is
consistent with her role. Last logins to the flagged systems — Admin Console
2026-08-15, Salesforce 2026-08-10 — are stale relative to the review date.

**Baseline:** The HR Specialist role is authorized for Workday (Read/Write) only.

**Analysis:** The two flagged entitlements match the Operations Specialist
baseline exactly (Admin Console Read/Write, Salesforce Read-only). This pattern
indicates the user transferred from Operations to HR and the prior-role access
was never revoked. The new-role access (Workday) was granted, but the old access
was not removed — an incomplete Mover event. This is privilege creep.

**Risk:** The account retains access to a sensitive system (Admin Console) with
no current business need; the stale logins confirm the access is unused.
Dormant, unauthorized access to a sensitive system is a standing liability and
a common audit finding.

**Recommendation:** Revoke Admin Console and Salesforce access; retain Workday.
Confirm the Operations-to-HR transfer against HR records. Review the Mover
process to determine why prior-role access was not deprovisioned at the time of
the transfer.

**Investigation note:** The transfer is inferred from the baseline match.
Confirm against HR records before closing the finding.

---

## Finding 3 — Offboarding Failure

**Severity:** Critical
**User:** Brian Hollis — Operations Specialist (terminated 2026-09-12)
**Systems:** Admin Console (Read/Write), Salesforce (Read-only) — account Active

**Observed:** Brian Hollis was terminated on 2026-09-12. As of the review date
(2026-10-01), his account remains Active with its full access intact. Login
records show activity on 2026-09-20 and 2026-09-28 — 8 and 16 days after
termination.

**Baseline:** Brian's access matched the Operations Specialist baseline and was
appropriate during his employment. The violation is not the access level — it
is the continued existence of the account after termination.

**Analysis:** This is an offboarding failure: the Leaver stage of the identity
lifecycle did not execute. The account should have been disabled on the
termination date. The account was used after termination, which raises this from
a cleanup item to a security incident requiring investigation.

**Risk:** Highest of the three findings. A former employee retained post-
termination access to the platform's most sensitive system and used it. Insider
knowledge of the environment compounds the exposure. The 19-day gap also
indicates the termination-to-deprovisioning trigger is not functioning.

**Recommendation:**
1. Disable the account immediately — full deprovisioning, not entitlement
   revocation.
2. Preserve all associated logs before further action, to maintain evidence
   integrity.
3. Open an investigation into the 2026-09-20 and 2026-09-28 sessions to
   determine what was accessed or changed.
4. Review the termination process and implement an automated deprovisioning
   trigger tied to the HR termination event, so Leaver deprovisioning fires on
   the termination date.

---

## Cross-Cutting Observation

Two of the three findings (Monica Flores, Brian Hollis) trace to incomplete
identity-lifecycle events — a Mover and a Leaver that did not fully execute.
This points to a process gap in the Joiner-Mover-Leaver workflow, specifically
the deprovisioning step during role changes and terminations, rather than
isolated individual error. Recommend reviewing JML automation so that access
changes are triggered by HR events rather than handled manually.
