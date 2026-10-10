# Access Review / IAM Audit — Meridian Payments, Inc.

A quarterly user access review (UAR) of a fictional mid-size fintech,
identifying access that violates least-privilege and documenting the
remediation. Built to demonstrate access-governance judgment: reviewing
entitlements against role baselines, flagging violations, and driving them to
remediation.

🎥 **[Watch the video walkthrough](https://www.youtube.com/watch?v=ZodRge2-OR8)** — a narrated walk through the review: identifying over-provisioned and stale access, flagging least-privilege violations, and documenting remediation.

---

## Overview

An access review answers one question: **does every person have exactly the
access their role requires — no more, no less?** Over time, access drifts.
People change roles and keep old permissions, accounts get over-granted, and
terminated employees aren't always deprovisioned. Left unchecked, this drift is
both a security risk and an audit failure — frameworks like SOC 2 and PCI-DSS
require organizations to periodically prove that access is justified.

This project is a complete review of **Meridian Payments**, a fictional payment
processor subject to SOC 2 and PCI-DSS. It reviews 11 users across 5 systems,
identifies 3 access violations, and documents the fixes.

## Scope

- **Systems reviewed:** Admin Console, Salesforce, NetSuite, Workday, AWS Console
- **Population:** 11 users / 17 access entries
- **Period:** Q3 2026 (review date 2026-10-01)

## Method

Every access entry was compared against an authorized **role baseline** — a
documented standard of what each role is permitted to access. Access that
appears in a user's actual permissions but not in their role's baseline is
flagged as a finding. This baseline-first approach keeps findings objective:
each one points to a specific, documented gap rather than a judgment call.

## Files in this project

| File | What it contains |
|---|---|
| `role-access-matrix.csv` | The baseline — what each role is authorized to access |
| `user-access-data.csv` | The actual access data under review |
| `findings.md` | The 3 violations, with analysis, risk, and recommendation |
| `remediation-plan.md` | The fixes, prioritized by severity, with owners |

## Summary of findings

| # | User | Finding | Severity |
|---|---|---|---|
| 1 | Kevin Brooks | Excess privilege — access beyond role | Medium |
| 2 | Monica Flores | Privilege creep — access retained after a role change | Medium |
| 3 | Brian Hollis | Offboarding failure — terminated account still active and used | Critical |

Two of the three findings trace to incomplete identity-lifecycle (Joiner-Mover-
Leaver) events, pointing to a systemic deprovisioning gap rather than isolated
error — addressed in the remediation plan.

---

## About this project

This review applies 8+ years of Trust & Safety and investigations experience —
timeline reconstruction, evidence-based analysis, and documentation discipline
— to an identity and access management context. The offboarding finding in
particular is treated as an investigation, not a cleanup task: the recommended
actions include log preservation and a review of post-termination activity.

Part of an IAM/GRC portfolio. Actively pursuing CompTIA Security+ (SY0-701).
