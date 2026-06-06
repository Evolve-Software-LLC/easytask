---
title: Web Authentication and LDAP - EasyTask Documentation
description: Configure LDAP Federation in EasyTask for corporate directory integration with Keycloak, including connection settings, user mapping, and TLS security.
keywords:
  - LDAP authentication
  - easytask
  - keycloak
  - LDAP federation
  - user directory
---

### 🌐 Manage LDAP

This interface allows administrators to configure **LDAP Federation** within the EasyTask system. LDAP (Lightweight Directory Access Protocol) is widely used for centralized user authentication and directory management. Enabling LDAP Federation replaces existing Keycloak user data with users from an external LDAP directory.

- **Warning Message**  
  Highlights that enabling LDAP Federation will permanently delete all existing Keycloak users and groups.

- **Existing Keycloak Users & Groups Detection**  
  Notifies the user about detected Keycloak accounts and provides an option to delete them before proceeding.

- **LDAP Configuration Fields Explained**  

  - ``LDAP Connection URL``  
    → The full LDAP server address (e.g., `ldap://ldap.example.com:389` or `ldaps://ldap.example.com:636` for secure connection).  
    _Defines where the system will connect to pull user data._

  - ``Bind DN``
    → The distinguished name used to bind to the LDAP server (e.g., `cn=admin,dc=example,dc=com`).  
    _This is typically the admin account used to authenticate and perform directory lookups._

  -  ``Bind Credentials``  
    → The password for the Bind DN user.  
    _Allows the system to authenticate the bind user on the LDAP server._

  - ``User DN``  
    → The base DN under which user accounts are located (e.g., `ou=users,dc=example,dc=com`).  
    _This tells EasyTask where to start searching for user entries._

  - ``UUID Attribute``
    → The LDAP attribute used as the unique identifier (commonly `entryUUID` or `uidNumber`).  
    _Ensures each user record is uniquely identified across systems._

  - ``Username Attribute``  
    → The LDAP attribute to be used as the username in EasyTask (e.g., `uid` or `sAMAccountName`).  
    _This will become the username for logging in._

  - ``User Object Classes``
    → Defines which object classes represent user entries (e.g., `inetOrgPerson`, `posixAccount`).  
    _Used to filter and identify valid user records._

  - ``Custom Search Filter``  
    → An optional LDAP filter to further narrow down users (e.g., `(memberOf=cn=easytask-users,ou=groups,dc=example,dc=com)`).  
    _Adds flexibility to control which users get imported._

  - ``Enable TLS``
    → Checkbox to use secure LDAPS connection.  
    _Ensures data is encrypted over the network._

- **Action Buttons**
  - ``Create LDAP Federation`` → Saves and applies the LDAP configuration.
  - ``Test LDAP Connection`` → Verifies that the provided LDAP settings are correct before saving.

💡 **Example:**  
```
LDAP URL: ldap://ldap.company.com
Bind DN: cn=admin,dc=company,dc=com
User DN: ou=users,dc=company,dc=com
UUID Attr: uid
Username Attr: sAMAccountName
```

---

## Frequently Asked Questions

**Q: What happens to existing Keycloak users when I enable LDAP Federation?**
A: Enabling LDAP Federation will permanently delete all existing Keycloak users and groups. The system will detect existing accounts and provide a warning before proceeding. Make sure to back up or note any local accounts before enabling LDAP.

**Q: How do I test my LDAP configuration before applying it?**
A: Use the "Test LDAP Connection" button on the LDAP configuration page. This verifies that the provided LDAP settings (URL, Bind DN, credentials, User DN) are correct and that the system can connect to the LDAP server before saving the configuration.

**Q: Should I enable TLS for LDAP connections?**
A: Yes, it is strongly recommended to enable TLS for LDAP connections to ensure data is encrypted over the network. Use `ldaps://` URLs (port 636) instead of plain `ldap://` (port 389) when TLS is enabled.

## Next Steps

- [Web Administration](./web_administration.md)
- [Web Component Overview](./web_component.md)
- [Web Management](./web_management.md)
