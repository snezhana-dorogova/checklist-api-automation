# checklist-api-automation

|Type of tests|Positive|Negative|
|---|---|---|
|**Authentication** <br> Test authentication mechanisms like HTTP Basic Authentication with a username and password, OAuth 2.0 Bearer Access Token, etc.||The first straightforward test case is accessing API endpoints that require such a credential with no credential or an invalid one to check a status code `401 Unauthorized`.|
|**Authorization - Role-Based Access Control** <br> 1. To test role-based access control (RBAC), you need a list of different roles for your API users.<br>2.Create a user for each role with an appropriately scoped credential.|Design positive tests to ensure that users can do what they’re allowed to do.|Design negative tests to check a status code `403 Forbidden`.|
|**Authorization - Resource-Level Access Control**<br>If you have private resources in your API that is only available to their creators or share targets.|Make sure that only those with the proper permissions can access them.|Others should see the `404 Not Found` error.|
|**Authorization - Field-Level Access Control** <br> If you have fields that your API only wants to reveal to users with a particular role.|Inspect the JSON structure of the response for a particular role.|Others should not see these fields. Note these the displaying hidden fields in filters and data exports.|
|**Input Validation - Method**|Check the supported HTTP method.|Check the not supported HTTP method.|
|**Input Validation - Payload**<br>Determine values for each sending data parameter:<br>-Necessity: required or optional.<br>-Data type.<br>-Format.<br>-Symbols.<br>-Supported values.<br>-Dependency on data in the database.<br>-Equivalence and boundary values (min, min+1, internal, max, max-1).<br>-Query parameters limits: limit, offset, page, ...<br>-Filter by fields: combination or intersection.<br>-Sort by fields: asc, desc, …|1. Execute API calls: <br>- with valid required parameters.<br> - with valid required parameters and valid optional parameters. <br>- The request should return 2XX HTTP status code. <br>- The response structure is according to the data model: <br>-schema validation: field names and field types are as expected, including nested objects. <br>-field values are as expected. <br>-non-nullable fields are not null. <br>2. For GET requests, verify there is NO STATE CHANGE in the system (idempotence). <br>3. For POST, DELETE, PATCH, PUT operations ensure action has been performed correctly in the system.|1. Empty payloads. <br>2. Missing required parameter(s). <br>3. Only optional fields. Invalid value for endpoint parameters. <br>4.Create a resource with a unique property value that already exists. <br>5. Delete a resource that doesn’t exist. <br>6. Update a resource with illegal data. <br>7. Additional fields in request bodies besides those you included in your API definition. <br>8. Outside the limitations to confirm that they result in a `400 Bad Request` error (min-1, max+1). <br>9. Database malicious queries or commands (cross-site scripting (XSS), SQL injections, and template injections).|
|**Input Validation - Headers**<br>|1. Verify that HTTP headers are as expected: Content-Type, Connection, Expires, ...<br>2. Verify that information is NOT leaked via headers.|Invalid values in HTTP headers.|
|**Load Tests (positive)<br>Stress Tests (negative)**<br>Find capacity limit points.|Ensure the system performs as expected under load.|Fails gracefully under stress.|
|**Performance**|Check API performs as expected: <br>- response time <br>- latency <br>- TTFB/TTLB in various scenarios (in isolation and under load).||
|**Rate limits** <br> To prevent overloads and brute-force attacks.||1. Check that all endpoints reject requests beyond rate limits with `500 Internal Server` Error (or other errors from the 500 range). <br> 2. Make sure they don’t include things like stack traces, internal network topology, or other private information.|
