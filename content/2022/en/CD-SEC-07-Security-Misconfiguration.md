---

layout: col-sidebar
title: "CD-SEC-07: Security Misconfiguration"

---

## Description

Low-code/no-code development platforms provide a wide range of features, some of which control the balance between security and support of specific use cases. However, AI-assisted coding, in its pursuit of functional and complete code, can disrupt this balance by generating or suggesting code that lacks critical security features. 

A citizen developer who relies on this AI-generated code without sufficient security expertise may unwittingly introduce security misconfigurations. This can result in anonymous user access to sensitive data, unprotected public endpoints, exposed secrets, and oversharing. This risk is compounded by the fact that many configurations are set at the application level rather than the tenant level, giving business users themselves, rather than administrators, the authority to implement these insecure defaults.

AI-generated code may lack critical security features because of a fundamental conflict between the AI's design and the citizen developer's needs. An AI coding assistant's primary goal is to provide a functional and direct response to a prompt. It excels at literal interpretation and aiming for exactness. If a citizen developer asks for a function like "create a login form that checks a password," the AI will provide a solution that does exactly that. It won't, however, automatically include security best practices that weren't explicitly requested.

The risk is that the AI acts as a skilled but unthinking tool. It prioritizes delivering a "working" solution over a "secure" one, and it lacks the security context to know that its literal output could introduce a vulnerability. This is especially dangerous when a developer assumes the AI's code is safe by default, leading to the deployment of insecure code that is functionally correct but easily exploited.


## Example Risk Scenarios

### Scenario #1

A citizen developer uses a low code / no code platform to build a public facing web form. The platform automatically generates a REST API endpoint to process the form data. For developer convenience, the platform’s default configuration for this API is “publicly accessible without authentication". An attacker can discover the API endpoint of this application through a network scan. Given the endpoint's default configuration, the attacker can send malicious requests to the API  and cause the server to expose sensitive customer data all without authentication.

### Scenario #2

A citizen developer uses an AI assistant to generate code for a logging function. The AI provides code that is correct for storing logs but includes a default setting that makes the storage location publicly accessible on the internet. The citizen developer, not being a security expert, deploys this code without recognizing the insecure default. An attacker can discover these public logs and steal sensitive information, including API keys or user tokens. This can occur not because the code was broken, but because the AI output was insecure by default.

### Scenario #3

A citizen developer builds a new application using a low code/no code platform that requires a password to be set by a user. The “rules” configured for this new application are less secure than the company’s password policy. The less secure password policy can make it easier for an attacker to guess the user’s password and access the system. 

### Scenario #4

An application is created by a citizen developer that allows users to upload documents to a server. The upload process has not been configured to scan the document upon upload for security risks. A malicious user can use this process to upload a document containing malware and lock all computers in the company unless payment is made resulting in a ransomware attack.


## How to Prevent

- Build tools for checking generated code for hard coded and insecure configurations
- Create securely configured templates to encourage best practices while adhering to customization
- Build validation functionality for solutions to detect issues before deployment
- Monitor configuration for drifts from secure patterns
- Read citizen development platform vendor documentation and follow recommendations
- Ensure configurations align with industry best practices
- Implement a change management system for tenant-level configuration


## References

- [By design: How default permissions on Microsoft Power Apps exposed millions](https://www.upguard.com/breaches/power-apps)
- [Why are low-code platforms becoming the new holy grail of cyberattackers?](https://www.zenity.io/blog/why-are-low-code-platforms-becoming-the-new-holy-grail-of-cyberattackers/)
- [Why are low-code platforms becoming the new holy grail of cyberattackers?](https://www.youtube.com/watch?v=e8PEIOa6W9M)
- [Reference architecture and landing zones for Power Platform](https://github.com/microsoft/industry/blob/main/foundations/powerPlatform/referenceImplementation/readme.md#power-platform-landing-zones-reference-implementation)

