# Configure Leap Role Mapping { #helm_configure_roleMapping }

There are 3 roles that must be configured for proper access to Leap: "Administrative Users", "EditApplicationUsers", and "UseApplicationUsers".

For detailed information about the available roles, refer to [Understanding Leap roles](in_leap_roles.md).

The Edit and Use roles support an extra property that adds all authenticated users to the role. Valid values are true and false.

These properties are defined in the .yaml file.  Below is a basic example of mapping users to the roles.

```yaml
configuration:
  leap:
    . . .
    roleMapping:
       AdministrativeUsers:
         MappedUsers:
          - leapadmin
       SuperAdminUsers:
         MappedUsers:
          - appsuper
       EditApplicationsUsers:
         AllAuthenticated: false
         MappedUsers:
          - leapadmin
       UseApplicationsUsers:
         AllAuthenticated: true
```

## Reference a User/Group from LDAP { #ref_usergroup_ldap .section }

To reference a specific user or group from a connected LDAP requires specific syntax, "realmName/userOrGroupId".  The realmName referenced here is the property from the ldapRegistry object, refer to [Connect Leap to LDAP](helm_configure_ldap.md).

### Mapping a user from LDAP { #map_user_ldap .section }

```yaml
configuration:
  leap:
    . . .
    roleMapping:
       AdministrativeUsers:
         MappedUsersAccessIDs:
          - acmeRealm/cn=Admin,o=Acme
```

### Mapping a group from LDAP { #map_group_ldap .section }

```yaml
configuration:
  leap:
    . . .
    roleMapping:
       AdministrativeUsers:
         MappedGroupsAccessIDs:
          - acmeRealm/cn=Sales,o=Acme
```

**Parent topic:** [Preparation](helm_preparation.md)