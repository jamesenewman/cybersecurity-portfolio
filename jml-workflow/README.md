# Joiner / Mover / Leaver (JML) Workflow — Meridian Payments, Inc.

The identity access lifecycle for Meridian Payments, demonstrated hands-on in Microsoft Entra ID: access **provisioned** at hire, **adjusted** on a role change, and **deprovisioned** at termination.

🎥 **[Watch the walkthrough](REPLACE-WITH-YOUTUBE-LINK)** — the full process and reasoning are in the voiceover. This README is the map; the video is the walk.

---

## Why this project

Project 1 ([Access Review / IAM Audit](../access-review)) audited Meridian and found access violations that traced back to broken lifecycle events — **privilege creep** and a **terminated account left active**. This project builds the process that prevents them.

> Project 1 was the detective control. This is the preventive one.

## The model

Access = **group membership** in Entra ID. Each system is a security group; a role is a bundle of groups.
**Systems:** Admin Console · Salesforce · NetSuite · Workday · AWS Console

## The three events

| Event | User | Action | Principle |
|---|---|---|---|
| **Joiner** | Dana Whitfield — Support Analyst | Provisioned to role baseline only | Least privilege from day one |
| **Mover** | Monica Flores — Support → Finance | Added NetSuite, **removed** Salesforce | A move isn't done until old access is removed |
| **Leaver** | Brian Hollis — terminated | Revoke sessions → block sign-in → remove access → deprovision | Close the post-termination window |

## Files

| File | What it contains |
|---|---|
| `role-baseline.csv` | The access standard — what each role is authorized to access |
| `jml-events.md` | The three events: before/after access and the actions taken |

---

Part of an IAM/GRC portfolio applying 8+ years of Trust & Safety investigations to identity and access management. Actively pursuing CompTIA Security+ (SY0-701).
