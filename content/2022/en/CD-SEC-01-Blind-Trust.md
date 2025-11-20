---

layout: col-sidebar
title: "CD-SEC-01: Blind Trust"

---

## Description

Blind trust refers to the uncritical acceptance of outputs, recommendations, or artifacts produced by an automated system, platform, or model without independent verification of their accuracy, integrity, or security. In software development contexts—particularly AI-assisted and low-code/no-code environments—blind trust manifests when developers assume that system-generated code, templates, or components are inherently safe or correct, leading to overlooked vulnerabilities and systemic security risks.

Blind Trust in AI-assisted and low-code/no-code development should be treated as a fundamental operating assumption by security teams because it defines a critical risk profile. Citizen developers often lack security training and experience several cognitive biases during their development process. The first is automation bias where citizen developers treat platform generated code and pre-built components as inherently secure since they are readily available. Similarly, the second bias is the availability heuristic where easily accessible code is chosen over optimal code. Third, anchoring bias causes citizen developers to favor the template or design they are originally presented with for their solution, leading to the widespread adoption of insecure defaults and vulnerable marketplace templates. This unchecked development model, driven by psychological biases, leads to the widespread adoption of insecure defaults and vulnerable marketplace templates, which attackers can leverage to hide malicious code beneath the LCNC or AI-Assisted platform’s abstraction. The lack of visibility and the ease of use create an environment where vulnerabilities accumulate undetected. 


## Example Risk Scenarios


### Scenario #1

An attacker uploads a seemingly benign login template to a low-code/no-code platform’s marketplace, disguised as a common and trusted solution. Unbeknownst to the platform or its users, this template contains a hidden, malicious script in a nested component or a custom code block. A citizen developer may trust the simplicity and appearance of the template and import the solution to build their own login page. When a user authenticates, the hidden script will be triggered. The script will quietly capture the user’s credentials and send them to the attacker’s server without disrupting the normal login process. The citizen developer having blindly trusted the marketplace template and the platform’s UI, would be completely unaware their solution is leaking credentials.

### Scenario #2

A citizen developer is tasked with provisioning a new cloud storage resource, which requires defining a highly restricted Cloud IAM Policy adhering to the principle of least privilege. The developer asks the AI-assisted coding tool to generate the Infrastructure-as-Code (IaC) script (e.g., using YAML or HCL), explicitly requesting that the associated service account be granted read-only access to the resource.
The AI, attempting to apply complex conditional logic for security segmentation, hallucinates a syntax or module reference within the IaC script. The resulting configuration is syntactically correct and appears functional, but contains a logical security error: the generated Cloud IAM Policy defaults to an overly permissive permission set  due to the failure of the hallucinated restrictive variables. The developer deploys the solution operating under blind trust, assuming the IaC script is secure simply because security controls were requested from the trusted AI source. An attacker can exploit this misconfiguration by compromising the service account, which, instead of being limited to read-only access, is granted full administrative control over the entire storage environment, leading to massive data exfiltration, modification, or deletion.


### Scenario #3

A citizen developer, prioritizing speed, imports a seemingly professional solution from a company’s marketplace in order to implement a login feature. Lacking the technical expertise to audit the code, the developer relies solely on the component’s professional appearance and high user ratings . However, the solution may contain a hidden, malicious crypto-miner script nested deep within its logic. This script can secretly consume the company’s backend server CPU/GPU cycles to generate cryptocurrency for the attacker. Because the login functionality works perfectly and is not visible through the low code / no code platforms user interface, it would go unnoticed for weeks.

### Scenario #4

A citizen developer uses an AI assistant or low code / no code platform to build a solution that must interact with a third-party API. The generated code is syntactically secure, but lacks the necessary defensive programming to sanitize or validate incoming API responses and blindly trust the data received from the third-party. An attacker can exploit this flaw by injecting malicious data into the third party API response, compromising user data or system integrity.

## Prevention – Blind Trust Secure Framework

OWASP’s Top 10 Citizen Development project has created the “Blind Trust” Secure Framework, a strategic approach to the concept of blind trust structured around three core actions. Blind Trust is considered a unique and foundational risk category because it embodies and amplifies the consequences of all other security risks within the citizen development environment, such as insecure design, authentication failures, and logging issues. Due to this comprehensive nature, it has been given a designated risk framework that the other listed risks do not have. Security teams can incorporate this specialized framework into their risk assessment to effectively address developer bias and turn it into a security asset.

### Enforce Secure Defaults

This prevention strategy addresses the fundamental behavioral biases of Citizen Developers towards simplicity, speed, and immediate access. This aims to recognize that developers often choose the path of least resistance, and design workflows that make the secure option the easiest and most convenient choice.

- Design platforms with secure-by-default configurations, ensuring that default settings are inherently safe and difficult to disable.
- Establish a standardized and vetted component library so developers can safely reuse trusted code and templates.

### Extend the Scope of Governance

This strategy addresses the disconnect between our classifications of citizen developed apps. We extend the scope of security by treating citizen development apps as governed extensions of our official environment, moving beyond the core platform's API to ensure security controls and continuous, real-time oversight extend into the configuration and data access of every single application. 

- Integrate these controls into a governance framework that enforces compliance and ensures consistent application of security policies across all AI-assisted and low-code/no-code projects.


### Secure Innovation Through Trust

We secure the innovation through trust at every stage by shifting security into an integrated component of application quality throughout the entire development lifecycle.

- Provide just-in-time security guidance embedded directly within the development environment to reinforce secure decision-making during coding and configuration.
- Offer structured training resources and reference guides to improve citizen developers’ understanding of common vulnerabilities and secure development practices.
- Implement a pre-deployment security auditing and validation system to automatically review all generated or modified code before release.


## References

- [The privacy and security risks of “citizen development](https://www.technologyfirst.org/Tech-News/13284443#:~:text=Ensure%20that%20citizen%20developed%20applications,to%20design%20security%20into%20applications)
- [The perils of blind trust in AI – why human accountability must not be automated away](https://oliverwight-eame.com/news/the-perils-of-blind-trust-in-ai-why-human-accountability-must-not-be-automated-away)
- [Blind trust in enhancement technologies encourages risk-taking even if the tech is a sham](https://www.aalto.fi/en/news/blind-trust-in-enhancement-technologies-encourages-risk-taking-even-if-the-tech-is-a-sham)
- [Training alone can't fix the citizen developer security gaps](https://www.technewsworld.com/story/why-training-wont-solve-the-citizen-developer-security-problem-179877.html)

