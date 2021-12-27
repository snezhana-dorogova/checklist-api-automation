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

*Input parameters properties:*
- Required or optional.
- Data types.
- Dependency on data in the database.
- Equivalence and boundary values (min, min+1, internal, max, max-1).
- Query parameters: filter, sort, limit, offset, ...
- HTTP Headers.

## Negative inputs:
- Empty payloads.
- Missing required parameter(s).
- Only optional fields.
- Invalid value for endpoint parameters.
- Create a resource with a unique property value that already exists.
- Delete a resource that doesn’t exist.
- Update a resource with illegal data.
- Additional fields in request bodies besides those you included in your API definition.
- Outside the limitations to confirm that they result in a `400 Bad Request` error (min-1, max+1).
- Database malicious queries or commands (cross-site scripting (XSS), SQL injections, and template injections).
- Invalid values in HTTP headers.

*Steps:*
1. Execute API calls: 
  - with valid required parameters.
  - with valid required parameters and valid optional parameters.
2. The request should return 2XX HTTP status code.
3. The response structure is according to the data model:
  - schema validation: field names and field types are as expected, including nested objects.
  - field values are as expected.
  - non-nullable fields are not null.
4. For GET requests, verify there is NO STATE CHANGE in the system (idempotence).
5. For POST, DELETE, PATCH, PUT operations ensure action has been performed correctly in the system.
6. Verify that HTTP headers are as expected: Content-Type, Connection, Expires, ...
7. Verify that information is NOT leaked via headers.

# Rate limits

> To prevent overloads and brute-force attacks.

*Steps:*
1. Check that all endpoints reject requests beyond rate limits with `500 Internal Server Error` (or other errors from the 500 range).
2. Make sure they don’t include things like stack traces, internal network topology, or other private information.

# Performance

*Steps:*
1. Check API response time, latency, TTFB/TTLB in various scenarios (in isolation and under load).

# Load Tests (positive), Stress Tests (negative)

*Steps:*
1. Find capacity limit points and ensure the system performs as expected under load, and fails gracefully under stress.
