---

layout: col-sidebar
title: "CD-SEC-06: Vulnerable and Untrusted Components"

---

## Description

When dealing with complex workflows in citizen development solutions, there's a significant risk that nested logic will obscure security vulnerabilities. For example, a main workflow may rely on sub-workflows or pre-built components to perform specific actions. These sub-processes may have different or entirely missing security controls compared to the main workflow, and the citizen development platform often lacks the tools to provide a clear, unified view into these security gaps, inherently trusting that the underlying functionality is safe.

This risk is compounded when developers use a marketplace to share and reuse these components. An insecure sub-workflow or component, once created and uploaded to the marketplace, can be easily downloaded and integrated by other developers, causing a single security flaw to be replicated and propagated throughout the entire organization's applications. This creates a supply chain vulnerability, where the platform solutions are subject to the trust of unvetted components from the developer community or organization.

AI coding assistants, in an effort to provide consistency, may suggest or reuse a previously generated code block that contains a security flaw. If a developer accepts and deploys this flawed code in multiple parts of an application, the single vulnerability becomes a widespread issue throughout the codebase. This practice, often a result of over-reliance on AI, can introduce a consistent and pervasive weakness that is difficult to remediate, as every instance of the reused code must be identified and patched.

Crucially, AI assistants may also "hallucinate"packages, libraries, or APIs that do not actually exist or that reference outdated/insecure versions. If a citizen developer includes one of these non-existent or flawed dependencies in their application based on the AI's suggestion, it can lead to build failures, runtime errors, or the introduction of a critical, unverified security weakness that is extremely difficult to trace back to a legitimate source. This inherent risk of AI-generated misinformation adds a new, complex layer to the existing supply chain security problem.


## Example Risk Scenarios

### Scenario #1

A citizen developer creates a simple subflow to publish a status update to a webhook for Business Intelligence ingestion. One solution publishes business relevant status updates, while another one unknowingly includes user PII which is propagated outside of the system.

### Scenario #2

A citizen developer integrates a highly rated component from a low code / no code platform marketplace into a critical, customer facing application. This widely used component contains a hidden server side request forgery vulnerability within its data filtering logic. An attacker can recognize this component's ubiquity and exploit this flaw across multiple applications. The popularity of a flawed component utilized for convenience would become a widespread security crisis.

### Scenario #3

A citizen developer using an AI Assistant to code to build an application, receives a hallucinated reference to a non-existent package. Due to the blind trust in the AI’s output, the developer searches for the suggested component and finds an unknown package with the exact name. The developer installs the phantom package which contains a preinstalled malicious script. The attacker who owns this package may now exfiltrate sensitive information from the developers application. 

### Scenario #4

A citizen developer asked their AI code assistant to generate the repetitive boilerplate for form input validation across an application. The AI, however, created a code block containing an exploitable Cross-Site Scripting vulnerability. Driven by a desire for consistency, the developer reused this exact, insecure code for every form in the application. This action scaled a single oversight into a systemic flaw, offering an attacker numerous XSS attack vectors and effectively turning the application's uniform architecture into a flawed blueprint for widespread compromise.

## Prevention

- Ensure each component adheres to the dedicated security controls utilized by the core application
- Clearly document what the sub workflow expects as input and output, and what data should be validated beforehand.
- Create standardized and secure subcomponents for common/redundant functionality to facilitate easy access and usage


## References

- [Incident 8j5043my610c](https://status.mendix.com/incidents/8j5043my610c)
- [Vulnerable and Outdated Components](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/)
- [Why are low-code platforms becoming the new holy grail of cyberattackers?](https://www.zenity.io/blog/why-are-low-code-platforms-becoming-the-new-holy-grail-of-cyberattackers/)

