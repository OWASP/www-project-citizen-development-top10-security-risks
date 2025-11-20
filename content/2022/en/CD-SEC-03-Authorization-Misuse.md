---

layout: col-sidebar
title: "CD-SEC-03: Authorization Misuse"

---

## Description

Applications rarely operate in isolation, and this remains true for those built by citizen development platforms. It is standard for these applications to integrate across an organization’s technology stack, connecting to SaaS, PaaS, cloud, or on-premise systems. To enable this ability, these technologies typically rely on pre-built connectors, API wrappers, or embedded authentication methods to allow quick setup and reuse of credentials. 

The risk arises when authentication and authorization are handled in an overly permissive, opaque or overly complicated way. Due to these perceived blockers, citizen developers may unknowingly or carelessly embed personal credentials or use access tokens to speed up integration. OAuth flows, refresh tokens, and API keys are often stored or shared across applications and persist well beyond their intended lifecycle. A quickly established credential may remain active indefinitely, accessible to other users or applications, and used for purposes outside of the original intent. 

Additionally, authorization scopes are frequently defined too broadly. Instead of restricting access to only the minimum required resources, applications are granted expansive permissions for the sake of flexibility or convenience, meanwhile exposing sensitive assets to unnecessary risk. Gradually, this leads to an ecosystem of abandoned, or “zombie” connections. These connections are long-lived, broadly scoped, and challenging to monitor or revoke, making them primed for malicious activity or unintentional data exposures. 

In summary, authorization misuse in citizen-developed technologies stems from a combination of ease-of-use features, poor credential hygiene, and a preference for broad persistent access. This risk applies equally to low code/no-code builders, AI-driven application generation, and other rapid development approaches where speed takes precedence over security. 


## Example Risk Scenarios

### Scenario #1

A citizen developer uses a low-code platform to quickly build an app that pulls sales data from their customer management system and pushes updates into a spread sheet shared across their team. To simplify setup, the analyst grants the app “read and write all data” access in the customer management system rather than limiting it to just sales reports. The platform stores their OAuth refresh token indefinitely, and the connection is reused when another team member clones the app for a different purpose. Months later, when the analyst changes roles, their Salesforce account is still the one powering several workflows, meaning others can still use their credentials. An attacker finds this exploit and uses the broad authorization to modify or exfiltrate sensitive Salesforce records, well beyond what the analyst ever intended.

### Scenario #2

A citizen developer asks an AI coding assistant to generate a script that automates uploading customer leads from emails into the company’s CRM. The developer provides their personal API key to the AI assistant, which hardcodes it directly into the generated script. The script requests “admin” access to the CRM API because it was the quickest way to avoid permission errors. The script is then shared with the broader team. The hardcoded admin key is copied, stored, and reused by multiple employees. A rogue employee eventually finds this key and uses it to gain full administrative access to the CRM.

### Scenario #3

Admin connects an application to their source code management system (e.g., Bitbucket) using a service or application account. The provisioned service or application account has unrestricted access to all repositories to enable seamless integration. Any internal user can abuse this connection to access restricted repositories they usually don’t have access to.

## Prevention

- Disable or monitor the use of implicitly shared connections
- Adhere to the principle of least privilege when providing access to environments that can contain shared connections
- Monitor citizen development platforms for over-shared connections
- Educate business users on the risks of connection sharing and its relation to credential sharing
- Explicitly refresh OAuth tokens on a regular basis by re-authenticating connections.
- Carefully review the scope an application requires and adhere to the principle of least privilege


## References

- [Credential sharing as a service: The hidden risk of low-code/no-code](https://www.darkreading.com/cyber-risk/credential-sharing-as-a-service-hidden-risk-of-low-code-no-code)
- [Why are low-code platforms becoming the new holy grail of cyberattackers?](https://www.zenity.io/blog/why-are-low-code-platforms-becoming-the-new-holy-grail-of-cyberattackers/)
