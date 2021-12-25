# checklist-api-automation

# Authentication
> Test an authentication mechanisms like HTTP Basic Authentication with a username and password, OAuth 2.0 Bearer Access Token, etc.

*Steps:*
1. The first straightforward test case is accessing API endpoints that require such a credential with `no credential` or `an invalid one` to check a status code `401 Unauthorized`.

# Authorization
> Role-Based Access Control

*Steps:*
1. To test `role-based access control (RBAC)`, you need a list of different roles for your API users.
2. Create a user for each role with an appropriately scoped credential.
3. Then design positive tests to ensure that users can do what they’re allowed to do.
4. Design negative tests to check a status code `403 Forbidden`.

> Resource-Level Access Control

*Steps:*
1. If you have private resources in your API that are only available to their creators or share targets. Make sure that only those with the proper permissions can access them.

> Field-Level Access Control

*Steps:*
1. 

# Input Validation
