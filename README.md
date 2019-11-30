
# GONU

GONU is a simple permission-based auth system based on abstractions like User, Role, Resource, and Permission.

## What GONU does 

The typical authorization is defined as follows:

1. Identify a user.
2. Identify the roles assigned to the user.  
3. Identify the resource that the user tries to access. 
4. Identify the action that the user is trying to do. 
5. decide whether the action is allowed or not.

For the step 5, you can conceptually think the process will be like a function.

GetPermission(role, resource identifier, action) -> boolean

The boolean value represents whether the actions is ALLOW or DENIED. By default, the returned will be false.

Actually GONU covers step 3 to 5 in the above authorization process, and the GONU works in the following authz configuration as an input. This can be stored within a file or can be created on-the-fly from memory. GONU provides objects good enough to represent this configuration. 

```
{
  # List of permission definitions
  permissions: [
    {
      # The resource to identify
      resource: {
        uri: "/resource/path/*/like/this"
      },
      # authorizations
      grants: [
        {
          # For this given set of roles
          roles: [ 
            "DEVELOPER"
          ],
          # You can do the following actions. 
          action: {
            allow: "*",
            deny: "POST" . # deny takes precedence always
          }
        },
        ...
      ]
    },
    ...
  ]
}
```

