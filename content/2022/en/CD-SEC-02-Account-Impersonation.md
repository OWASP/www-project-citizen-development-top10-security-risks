---

layout: col-sidebar
title: "CD-SEC-02: Account Impersonation"

---

## Description

Citizen developed applications often blur the line between an application’s own identity and identities of the people or services it connects with. Instead of using unique, well-governed application accounts, creators may embed personal credentials, shared service accounts, or database connections to enable quick access to data and services. These embedded identities might belong to the developer, a team, or an external system and are then implicitly used by anyone interacting with the application. 

Because the application operates under these embedded identities, security and monitoring systems typically see all activity originate from the same user, making every action to be from the creator or shared account. This allows any user of the application to impersonate its creator, concealing the true actor and creating a direct path for privilege escalation. This risk is amplified when a single application spans across multiple environments or platforms. 

Code agents can produce authentication or session logic that appears functional but lacks secure mechanisms such as unencrypted cookies or weak credential storage. They may even create or reuse service accounts without proper governance leading to inconsistent role enforcement unmonitored credentials. In such environments, organizations face hidden actions, broken audit trails, and increased liability as malicious actors or even unknowing users can impersonate others, bypass security controls, escalate privileges undetected. 


## Example Risk Scenarios

### Scenario #1

A citizen developer creates a simple application to view records from a database to accomplish a business task. They use their identity to log into the database, creating a connection embedded within the application. Every action that any user performs in this application ends up querying the database using the developer’s identity. A malicious user takes advantage of this and uses the application to view, modify or delete records they should not have access to. Database logs indicate that all queries were made by a single user, the trusted developer.

### Scenario #2

A developer creates a business application that allows employees to fill out forms with their personal information. To store form responses, the developer uses their personal email account. Users have no way of knowing that the app is storing their data on the developer’s personal account.

### Scenario #3

A developer creates a business application and shares it with an administrator. The developer configures the app to use its user’s identity. Aside from its stated purpose, the app also uses its user’s identity to elevate the privileges of the developer. Once the admin uses the app, they inadvertently elevate the developer’s privileges.


## How to Prevent

- Adhere to the principle of least privilege when provisioning connections to databases/services/SaaS
- Leverage OAuth for access control with user’s consent to the resource server
- Restrict the use of "creators identity" when an application is designed to be shared. Use a dedicated service account instead and apply dedicated behavior monitoring to those service accounts.
- Monitor for apps that request highly privileged OAuth scopes unrelated to the apps purpose
- Ensure a proper audit trail is maintained to identify the actor behind actions performed through the shared connection, whether those connections are shared by virtue of users using the application or by granting users access to that connection directly


## References

- [Watch out for user impersonation in low-code/no-code apps](https://www.darkreading.com/cyber-risk/watch-out-for-user-impersonation-in-low-code-no-code-apps)
- [Credential sharing as a service: The hidden risk of low-code/no-code](https://www.darkreading.com/cyber-risk/credential-sharing-as-a-service-hidden-risk-of-low-code-no-code)
- [Do low-code/no-code platforms pose a security risk?](https://sdtimes.com/lowcode/do-low-code-no-code-platforms-pose-a-security-risk/)
- [Watch out for user impersonation in low-code/no-code apps](https://www.youtube.com/watch?v=D3A62Rzozq)

