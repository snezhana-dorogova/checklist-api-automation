# checklist-api-automation

# Authentication

> Test authentication mechanisms like HTTP Basic Authentication with a username and password, OAuth 2.0 Bearer Access Token, etc.

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
1. If you have private resources in your API that is only available to their creators or share targets, make sure that only those with the proper permissions can access them.

> Field-Level Access Control

*Steps:*
1. If you have fields that your API only wants to reveal to users with a particular role, then inspect the JSON structure of the response for a particular role.

# Input Validation (Sending data to the API)

## Positive:
- Data types.
- Equivalence and boundary values (min, min+1, internal, max, max-1).
- 

## Negative:
- Additional fields in request bodies besides those you included in your API definition.
- Outside the limitations to confirm that they result in a `400 Bad Request` error (min-1, max+1).
- Database malicious queries or commands (cross-site scripting (XSS), SQL injections, and template injections).

# Rate limits
> To prevent overloads and brute-force attacks.

*Steps:*
1. Check that all endpoints reject requests beyond rate limits with `500 Internal Server Error` (or other errors from the 500 range).
2. Make sure they don’t include things like stack traces, internal network topology, or other private information.
