---

layout: col-sidebar
title: "CD-SEC-04: Sensitive Data Leakage and Handling Failures"

---

## Description

Citizen development platforms are powerful tools for connecting systems and automating processes, but these conveniences often come at the cost of security. Both platforms and their users often lack the necessary context and controls for safe data handling, resulting in two critical risks: uncontrolled data leakage and cascading operational failures.

Data leakage occurs when sensitive information is transmitted beyond its intended storage location or outside the organization's control. Most citizen development tools cannot automatically classify, secure, or track sensitive data throughout an application’s lifecycle. Designed for flexibility rather than security, these platforms lack understanding of the context or purpose of the data they process and therefore cannot identify or tag sensitive fields. As a result, citizen developers may unintentionally expose data through misconfigured permissions, unprotected connections, public storage, unsecured APIs, or AI-generated logic that transmits or logs information without encryption. The absence of proper data governance on both the platform and user sides allows sensitive information to be collected, stored, and shared without visibility, tracking, or protection.

Operational risk also increases when non-technical users connect disparate systems through citizen development workflows. These connections often create undocumented dependencies, forming a fragile web where small changes can trigger cascading effects across multiple processes. Because these operations are rarely mapped or monitored, they can cause disruptions, outages, and data integrity issues. Ultimately, these risks highlight how speed and convenience in citizen-developed applications often come at the expense of security and governance.


## Example Risk Scenarios

### Scenario #1

A sales operations analyst uses a low code citizen development platform to automatically sync customer data from the CRM into the marketing database for campaign tracking. The sync workflow includes sensitive customer PII not required for marketing use. The marketing database is hosted in a SaaS platform with weaker controls. A change in the CRM schema can trigger multiple downstream apps to mis-map fields and cause corrupted campaign data. Sensitive PII will be exposed inappropriately and data quality errors can be spread across customer-facing campaigns.

### Scenario #2

A product manager uses an AI assistant to generate a script that analyzes support tickets and sends summaries to the internal messaging platform for visibility. The manager pastes raw support logs which contain customer account IDs and occasional confidential error messages into the AI assistant prompt. The assistant may generate code that sends detailed summaries to a public Slack channel with 200+ employees. Confidential data can leave its secure support environment and be broadcast to employees who do not possess privileged access to this information, creating data leakage and compliance risks.

### Scenario #3

A citizen developer uses a low code platform to create an internal application that retrieves data from a private cloud storage bucket. To make the data available for internal dashboards, the developer creates a public facing API endpoint in the application that serves the data. The developer accidentally misconfigures the APi endpoint to return the data in a raw, un-sanitized format, which includes the access credentials for the cloud storage bucket in the response body. An attacker can discover this public API endpoint and send a curl request to retrieve the hard-coded storage creds in the response body, compromising the private cloud storage bucket. 

### Scenario #4

An application is created by a citizen developer in a low code/no code platform and connects to an internal database. For simplicity, the database connection string, which includes sensitive credentials, is stored in a  variable within the app’s environment. The platform encrypts this value and in its live runtime, giving a false sense of security to the developer. When a developer exports this component to share, the platform fails to scrub this data from the export. The connection string, containing the plaintext password, is included in the exported file. A bad actor may find this password in a shared drive or public marketplace and use the found credentials to connect to the internal database directly, bypassing the platform's security and gaining full access to the company’s data.

### Scenario #5

A citizen acting as an application developer uses an AI assistant to create a webhook listener. The AI, acting as a functional but unthinking tool, provides code that logs all incoming data without sanitizing it. Unaware of the security risk, the developer deploys this code. An attacker who has gained basic access to the logging functionality can discover a sensitive client secret from a partner’s webhook payload and use this information to impersonate the partner’s service and manipulate the application.


## Prevention

-Limit connectors to an approved services list
- Limit creation of custom connectors to dedicated personnel
- Monitor platforms for data flow outside the organizational boundary, including multi-hop paths
- Work with the business to understand the citizen development needs and provide simple alternatives that meet security requirements
- Educate business users on the compliance, privacy, and security risks related to data storage
- Monitor managed databases, environment variables, and configuration provided by citizen development  vendors for sensitive data
- Ensure security teams are involved in security reviews with applications having access to sensitive data
- Enforce secure standardized data transfer between combined citizen development workflows


## References

- [3 ways no-code developers can shoot themselves in the foot](https://www.darkreading.com/dr-tech/3-ways-no-code-developers-can-shoot-themselves-in-the-foot)
- [Hackers abuse low-code platforms and turn them against their owners](https://www.zenity.io/blog/hackers-abuse-low-code-platforms-and-turn-them-against-their-owners/)
- [Low-code security and business email compromise via email auto-forwarding](https://www.zenity.io/blog/low-code-security-and-business-email-compromise-via-email-auto-forwarding/)
- [Full operational shutdown—another cybercrime case from the Microsoft Detection and Response Team](https://www.microsoft.com/en-us/security/blog/2020/04/02/full-operational-shutdown-another-cybercrime-case-microsoft-detection-and-response-team/)
- [Implement a data policy strategy](https://learn.microsoft.com/en-us/power-platform/guidance/adoption/dlp-strategy)

