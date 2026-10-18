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
- **Before:** Admin Console, Salesforce, Workday
- **After:** Workday
- **Actions:** − Admin Console · − Salesforce (Workday retained — her HR access)
- **Principle:** Her new HR access (Workday) was granted, but her old Operations access was never removed — Admin Console and Salesforce sat on the account with no business need. That's the **privilege-creep** finding from the Access Review project. The move isn't complete when the new access is added; it's complete when the old access comes off. Here, both old systems are removed and the account is brought back to least privilege.

## 3. Leaver — Brian Hollis

- **Event:** Termination
- **Before:** Admin Console, Salesforce
- **Actions (in order):** revoke sessions → block sign-in → remove all group memberships → preserve record & review activity around termination → deprovision
- **Principle:** Proper offboarding requires promptly disabling access, removing unnecessary permissions, and addressing potential security concerns. Because Brian's account was used after termination in the simulated audit, a real-world investigation would also require preserving relevant logs and reviewing post-termination activity according to established incident-response procedures.
