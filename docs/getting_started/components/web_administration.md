---
title: Web Administration - EasyTask Documentation
description: Manage EasyTask users, holiday calendars, and LDAP federation for access control, scheduling, and corporate directory integration.
keywords:
  - administration
  - easytask
  - user management
  - holiday calendar
  - LDAP federation
---

# 🛡️ Administration

The Administration section provides tools for managing system access, calendars, and external directory integrations.

## 👥 Manage Users

The **Manage Users** page is the comprehensive interface for system access control. Detailed user management ensures that every team member has the appropriate level of access.

### Features
- **View Users:** Audit system access by filtering users by name, role, or team.
- **Create/Update Users:** Onboard new members or update details for existing ones.
- **Delete Users:** Remove access for departures (ensure task ownership is reassigned first).

### User Roles
Access is governed by four distinct roles, ensuring the principle of least privilege:

- **Admin:** Complete access to all system features and configurations.
- **Operator:** operational access to manage tasks and executions, but cannot modify system-wide configurations.
- **User:** Standard access for viewing tasks and basic interactions.
- **Viewer:** Read-only access, ideal for monitoring and reporting purposes.

---

## 📅 Manage Holiday Calendar

The **Holiday Calendar** module allows administrators to define non-working days that the scheduler must respect.

### Features
- **Block Dates:** Define single dates or date ranges as holidays.
- **Calendar Grouping:** Organize holidays by "Calendar Name" (e.g., "US_Holidays", "EU_Holidays") to support different regional teams.
- **Automatic Refresh:** Updates to the holiday calendar trigger an immediate scheduler refresh, ensuring task execution plans are updated instantly.

---

## 🔌 LDAP Federation
> **Note:** This feature is available for **On-Premises Deployments** only.

The LDAP Federation module facilitates the seamless integration of corporate directories with the EasyTask system.

- **Migration & Sync:** Automatically migrate users from existing LDAP/Active Directory setups into the system's Keycloak authentication provider.
- **Group Mapping:** Map LDAP groups to the system's specific Roles (Admin, Operator, etc.) to automate access control.

---

## Frequently Asked Questions

**Q: What user roles are available in EasyTask?**
A: EasyTask supports four roles: **Admin** (complete access to all features), **Operator** (manage tasks and executions, no system config changes), **User** (standard access for viewing and basic interactions), and **Viewer** (read-only access for monitoring and reporting).

**Q: How do holiday calendars affect task execution?**
A: When a holiday calendar is assigned to a task, the scheduler checks it before executing. If the current day is marked as a holiday, the task is automatically skipped. Changes to the holiday calendar trigger an immediate scheduler refresh so updates take effect instantly.

**Q: Is LDAP Federation available for cloud deployments?**
A: No. LDAP Federation is currently available only for **on-premises deployments**. It integrates with Keycloak to migrate and sync users from existing LDAP/Active Directory setups and map LDAP groups to EasyTask roles.

## Next Steps

- [Web Authentication and LDAP](./web_authentication.md)
- [Holiday Calendar Management](./web_calendars.md)
- [Web Component Overview](./web_component.md)
