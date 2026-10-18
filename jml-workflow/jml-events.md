# JML Events — Meridian Payments, Q4 2026

Access is modeled as Microsoft Entra ID security-group membership. Each group represents one system; a role is the set of groups it's authorized for. See `role-baseline.csv` for the standard.

---

## 1. Joiner — Dana Whitfield

- **Role:** Support Analyst (backfill)
- **Before:** none — new identity
- **Provisioned:** Admin Console, Salesforce
- **Principle:** Least privilege. Baseline only — no standing access to NetSuite, AWS, or Workday, because the role has no business need for them.

## 2. Mover — Monica Flores

- **Change:** Operations Specialist → HR Specialist
- **Before:** Admin Console, Salesforce
- **After:** Workday
- **Actions:** + Workday · − Admin Console · − Salesforce
- **Principle:** The move is incomplete until prior-role access is removed. Here, *two* old entitlements come off, not one — adding the new access and leaving either old system in place is the **privilege-creep** finding flagged in the Access Review project, prevented at the point of the move.

## 3. Leaver — Brian Hollis

- **Event:** Termination
- **Before:** Admin Console, Salesforce
- **Actions (in order):** revoke sessions → block sign-in → remove all group memberships → preserve record & review activity around termination → deprovision
- **Principle:** Close the window between termination and access removal. Offboarding is handled as an investigation — logs preserved, post-termination activity reviewed — not a cleanup task. Directly remediates the Critical offboarding finding from the Access Review project, where a terminated account remained active and was used.
