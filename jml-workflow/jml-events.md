# JML Events — Meridian Payments, Q4 2026

Access is modeled as Microsoft Entra ID security-group membership. Each group represents one system; a role is the set of groups it's authorized for. See `role-baseline.csv` for the standard.

---

## 1. Joiner — Dana Whitfield

- **Role:** Support Analyst (backfill)
- **Before:** none — new identity
- **Provisioned:** Admin Console, Salesforce
- **Principle:** Least privilege. Baseline only — no standing access to NetSuite, AWS, or Workday, because the role has no business need for them.

## 2. Mover — Monica Flores

- **Change:** Support Analyst → Finance Analyst
- **Before:** Admin Console, Salesforce
- **After:** Admin Console, NetSuite
- **Actions:** + NetSuite · − Salesforce (Admin Console retained — required by both roles)
- **Principle:** The move is incomplete until prior-role access is removed. Adding the new and keeping the old is the **privilege-creep** finding flagged in the Access Review project — prevented here by removing Salesforce at the point of the move.

## 3. Leaver — Brian Hollis

- **Event:** Termination
- **Before:** Admin Console, Salesforce
- **Actions (in order):** revoke sessions → block sign-in → remove all group memberships → preserve record & review activity around termination → deprovision
- **Principle:** Close the window between termination and access removal. Offboarding is handled as an investigation — logs preserved, post-termination activity reviewed — not a cleanup task. Directly remediates the Critical offboarding finding from the Access Review project, where a terminated account remained active and was used.
