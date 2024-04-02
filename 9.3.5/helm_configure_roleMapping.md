# Configure Leap Role Mapping

There are 3 roles that must be configured for proper access to Leap: "Administrative Users", "EditApplicationUsers", and "UseApplicationUsers".

- Administrative Users can access the admin UI, create and use applications.
- EditApplicationUsers can create and use application.
- UseApplicationUsers can use applications.

The Edit and Use roles support an extra property that adds all authenticated users to the role. Valid values are true and false.

These properties are defined in the .yaml file.  Below is a basic example of mapping users to the roles.

```
configuration:
  leap:
    roleMapping:
       AdministrativeUsers:
         MappedUsers:
          - leapadmin
       EditApplicationsUsers:
         AllAuthenticated: false
         MappedUsers:
          - leapadmin
       UseApplicationsUsers:
         AllAuthenticated: true
```

## Reference a User/Group from LDAP
To reference a specific user or group from a connected LDAP requires specific syntax, "realmName/userOrGroupId".  The realmName referenced here is the property from the ldapRegistry object, refer to [Connect Leap to LDAP](helm_configure_ldap.md).

### Mapping a user from LDAP
```
configuration:
  leap:
    roleMapping:
       AdministrativeUsers:
         MappedUsersAccessIDs:
          - acmeRealm/cn=Admin,o=Acme
```

### Mapping a group from LDAP
```
configuration:
  leap:
    roleMapping:
       AdministrativeUsers:
         MappedGroupsAccessIDs:
          - acmeRealm/cn=Sales,o=Acme
```
