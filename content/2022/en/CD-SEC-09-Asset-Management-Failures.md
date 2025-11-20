---

layout: col-sidebar
title: "CD-SEC-09: Asset Management Failures"

--- 

## Description

The core principle of citizen development platforms is to enable rapid application with seemingly low maintenance overhead. This ease of development combined with the volume and custom configuration of citizen developed solutions, leads to ungoverned, unpatched, and ultimately orphaned solutions. Because citizen developed applications are easy to create and often rely on SaaS services for management, organizations quickly see the number of active solutions grow. This agility contributes to the critical risk of asset management failures. Citizen developed applications are prone to being forgotten or abandoned while remaining active and functional. Furthermore, useful internal applications become widely shared within the organization, scaling rapidly in usage and dependency without the necessary business continuity measure expected of more standardized and essential systems such as having designated owners, IT monitoring, or a Service Level Agreement (SLA). The challenge of maintaining a clear inventory becomes nearly impossible due to the sheer volume.

The uniqueness and variety of these citizen developed solutions and workflows create a significant problem for version control and security patching. Since citizen development solutions are often widely shared or custom configured, they are not patched easily when a flaw is discovered in an underlying component. This leaves the process of securing existing, at-risk applications highly manual and unreliable. Moreover, the lack of central tracking or version control for these applications means security flaws are often undetectable. Without proper channels for mitigation, an organization has decreased visibility into its solutions, increasing its attack surface and maintenance debt.    


## Example Attack Scenarios

### Scenario #1

A highly used low code/no code application becomes orphaned. This app is outside of IT’s monitoring and patching schedule. An attacker can easily exploit a known vulnerability in this application since it is unpatched. This foothold can be used to access and steal sensitive data from the connected services, leveraging the application's established but unreviewed permissions. Since the application is unmonitored, this data leakage could go undetected for an extended period of time.

### Scenario #2

A citizen developer uses AI-assisted coding to build a critical business workflow deploying it as shadow IT without a security review. The developer inadvertently incorporates a malicious dependency from a compromised public code source suggested by the AI. This malicious code is deployed undetected, bypassing all governance. When activated, it exploits the workflow’s permissions and its implicit coupling to inject data-stealing routines into other connected, popular applications and successfully can exfiltrate information because the solution lacks proper version control and central oversight.

### Scenario #3

A citizen developer browser through the platform marketplace for a low code / no code solution and explores application templates. Each click creates an app with an external-facing URL. The developer forgets about these apps, even though they might expose business data. This scenario multiplies by the number of developers, resulting in an ever-growing number of stale apps.


## Prevention

- Establish a centralized governance center
- Enforce application ownership and lifecycle
- Implement tiered risk classification
- Mandate version control and secure deployment
- Maintain a comprehensive inventory that lists applications, components, and users
- Remove or disable unused dependencies, unnecessary features, components, files, and documentation


## References

- [3 Ways No-Code Developers Can Shoot Themselves in the Foot](https://www.darkreading.com/dr-tech/3-ways-no-code-developers-can-shoot-themselves-in-the-foot)
- [Why So Many Security Experts Are Concerned About Low-Code/No-Code Apps](https://www.darkreading.com/dr-tech/why-so-many-security-experts-are-concerned-about-low-code-no-code-apps)
- [You Can't Opt Out of Citizen Development](https://www.darkreading.com/edge-articles/you-can-t-opt-out-of-citizen-development)

