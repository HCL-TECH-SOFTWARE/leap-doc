# Configure Leap Role Mapping { #helm_configure_roleMapping }

There are 3 roles that must be configured for proper access to Leap: "Administrative Users", "EditApplicationUsers", and "UseApplicationUsers".

- <b>AdministrativeUsers</b> can access the admin configuration page, admin dashboard, edit existing applications, create and use applications.
- <b>SuperAdminUsers</b> can access the admin dashboard, and edit all Leap applications. They do not have access to application data. To access the data, a user must be added to a role within the application and the application must be redeployed.
- <b>EditApplicationUsers</b> can create and use application.
- <b>UseApplicationUsers</b> can use applications.

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