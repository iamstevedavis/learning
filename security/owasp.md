### Injection
Search for syntax that makes requests to the interpreters in your environment. Pay attention to all places where input from an HTTP request could possibly make its way into any of these calls. Do we make any insertions to Redis that are directly from API input?

### XML External Entities (XXE)
Is our discovery data sanitized?

### Cross-Site Scripting (XSS)
#### Stored XSS
Storing unsanitized user input in your application is considered high risk.
Do we need to implement CSP? - https://stackoverflow.com/questions/45630376/shall-i-use-the-content-security-policy-http-header-for-a-backend-api

#### Reflected XSS
Even when user input is not stored, check your applications for HTML output that includes unvalidated and unescaped user input.

#### DOM XSS
Look for ways someone could dynamically include and deliver attacker-controllable data to us. All of our input is primitive but what about the oAuth flow?

### Insecure Deserialization
When possible, use an architectural pattern that does not accept serialized objects from untrusted sources. You could also use a serialization medium that only permits primitive data types. We have fastify to perform this for us for JSON as well as strict schema rules for primitive types. 

## Infrastructure Threats
### Sensitive Data Exposure
Apps should use secure cryptographic algorithms to safeguard data.
- How secure is your algorithm?
- How is your data transmitted?
- How is your data stored?

### Security Misconfiguration Flaws
Ensure we keep our modules up to date.

### Hardening Process
Configure separate environments (such as development, QA, and production) identically and ensure different credentials are required for each environment.

### Insufficient Logging and Monitoring Flaw

Logins, failed logins, and high-value transactions must be logged properly, logs must be monitored, response plan in place.

1. Create sufficient logs
   1. Every access control related event should be logged
   2. Attemps to access underlying resources should be logged
2. Establish audit trails
3. Monitor and respond

## ID Threats
Do we have broken authentication?

### Broken Access Control
Flaws in how access is granted and controlled throughout the system

### Session IDs
Check to see if your app exposes session IDs in URLs **or** if the app keeps session IDs static.
- If either case is true, your app is vulnerable.

Granting generalized access for a role, instead of for specific records and specific actions (i.e., view, delete, etc.) can cause vulnerabilities.
Remember to invalidate authentication tokens, such as JWTs, on the server after logout.
