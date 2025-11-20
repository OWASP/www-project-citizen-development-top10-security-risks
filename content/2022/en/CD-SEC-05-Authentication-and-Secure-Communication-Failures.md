---

layout: col-sidebar
title: "CD-SEC-05: Authentication and Secure Communication Failures"

---

## Description

Citizen-developed technologies frequently handle connections to sensitive systems and data. These connections rely on authentication methods and secure communication protocols to protect data in transit and ensure only authorized users or applications gain access.

However, because citizen developers are often more focused on functionality than security, authentication, and communication are commonly misconfigured. Common security flaws include the use of weak or personal credentials, storing secrets or tokens in plaintext, disabling TLS/SSL certificate validation, and selecting insecure communication protocols (e.g., HTTP instead of HTTPS). In some cases, authentication flows are only partially implemented or improperly applied. A few examples of this include omitting multi-factor authentication (MFA), embedding long-lived bearer tokens directly in source code, or reusing static credentials across multiple applications or environments.

Misconfigured or insecure integrations can enable unauthorized access, facilitate credential compromise, and allow interception or manipulation of data in transit. Over time, this leads to an accumulation of ungoverned, weakly secured connections that violate corporate security policies and remain difficult to detect or remediate. Ultimately, authentication and secure communication failures occur when citizen-developed technologies fail to generate or enforce secure-by-default configurations, allowing insecure connection practices to persist.


## Example Risk Scenarios

### Scenario #1

A customer support manager builds an LCNC app to pull ticket data from a customer support service and push summaries into a dashboard. The connection is set up using the manager’s personal username/password instead of an API key with scoped permissions. TLS validation is disabled to avoid repeated connection errors. The same connection is reused by multiple apps across the team. If the manager’s password is compromised, attackers gain broad access to Zendesk. Additionally, disabling TLS exposes data in transit to interception.

### Scenario #2

A citizen developer asks an AI coding assistant to generate a script that connects a financial system API to an internal reporting tool. The assistant generates code that hardcodes API keys directly into the script without encryption or secret management. It defaults to HTTP instead of HTTPS for the API endpoint. The developer copies the script into a shared GitHub repo visible to contractors. The exposed API keys and insecure transport channel create both authentication and communication risks, allowing unauthorized third parties to access sensitive financial data.

### Scenario #3

A developer creates an application that uses an FTP connection but does not check the box that turns on encryption. Users of that app have no way to know that their data is being transferred unencrypted since the communication between the app and its users is encrypted.

### Scenario #4

A developer uses administrator credentials to create a database connection. They build an application that uses that connection to show data to its users. Even though they intended to allow read-only operations through the app, users can use the over-privileged connection to write or delete records from the database.

## Prevention

- In production environments, limit the creation of any new connections to dedicated and authorized personnel or teams. 
- Monitor platforms for connections that do not comply with best practices
- Create secure authentication framework code and configuration settings or solution component templates for easy implementation of secure authentication, authorization, and communication
- Provide training for citizen developers on the risk of insecure communication


## References

- [CISO View Insights: Securely scaling RPA initiatives](https://www.cyberark.com/resources/blog/ciso-view-insights-securely-scaling-rpa-initiatives)

