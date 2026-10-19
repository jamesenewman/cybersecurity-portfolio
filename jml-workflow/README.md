# Joiner / Mover / Leaver (JML) Workflow — Meridian Payments, Inc.

A hands-on simulation of the Joiner, Mover, and Leaver identity lifecycle for the fictional Meridian Payments, Inc., using Microsoft Entra ID to demonstrate manual access provisioning, role changes, and account deprovisioning.

🎥 **[Watch the walkthrough](https://www.youtube.com/watch?v=qy1seE6QAAo)** — the full process and reasoning are in the voiceover. This README is the map; the video is the walk.

---

## Why this project

Project 1 ([Access Review / IAM Audit](../access-review)) identified several access violations at the fictional Meridian Payments, including privilege creep and a terminated account left active.

This project builds on those findings by demonstrating the manual Joiner, Mover, and Leaver processes in Microsoft Entra ID. The focus is on assigning appropriate access, removing permissions when employees change roles, and properly deprovisioning accounts when employees leave.

> Project 1 identified the problems. Project 2 demonstrates how those problems can be addressed.

## The model

For this simulation, access is represented through security-group memberships in Microsoft Entra ID. Each group represents a business system, and each role has a defined set of authorized groups.

Adding or removing group memberships demonstrates how access would be managed throughout an employee's lifecycle. This lab does not include live integrations with the underlying business applications.

**Systems:** Admin Console · Salesforce · NetSuite · Workday · AWS Console

## The three events

| Event | User | Action | Principle |
|---|---|---|---|
| **Joiner** | Dana Whitfield — Support Analyst | Provisioned to role baseline only | Least privilege from day one |
| **Mover** | Monica Flores — Operations → HR | **Removed** Admin Console + Salesforce (Workday retained) | A move isn't done until old access is removed |
| **Leaver** | Brian Hollis — terminated | Revoke sessions → block sign-in → remove access → deprovision | Close the post-termination window |

## Files

| File | What it contains |
|---|---|
| `role-baseline.csv` | The access standard — what each role is authorized to access |
| `jml-events.md` | The three events: before/after access and the actions taken |

---

Part of an IAM/GRC portfolio applying 8+ years of Trust & Safety investigations to identity and access management. Actively pursuing CompTIA Security+ (SY0-701).
