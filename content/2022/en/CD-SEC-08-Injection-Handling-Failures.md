---

layout: col-sidebar
title: "CD-SEC-08: Injection Handling Failures"

---

## Description

The risk of injection handling failures is a critical security concern in low-code/no-code and AI-assisted solutions. This risk arises when an application ingests user-provided data from various sources, but fails to properly sanitize or validate it before using it in a command or query. This is a significant problem because many citizen development applications are designed to dynamically query data based on user input. As a result, they are highly exposed to injection attacks. The risk is compounded by a lack of security context: neither the AI nor the average citizen developer understands what makes data sensitive or dangerous. This can lead to code that is functionally correct but easily exploited.

The AI, in its pursuit of a "working" solution, may not always parameterize queries, which allows attackers to inject malicious code. Many citizen development platforms also lack the ability to vet input schemas for possible injection, making them vulnerable by default. Ultimately, this can lead to the deployment of insecure solutions that are functionally correct but easily exploited.  Low-code/no-code platforms often use a specific, non-standard syntax to reference variables and platform data within a solution. This creates a unique form of injection vulnerability. The risk arises when an LCNC application ingests user-provided data but fails to properly sanitize it for this special syntax. An attacker can then inject a string that is interpreted as a command to retrieve sensitive, internal platform data, such as a company's organization ID, even if they are not authenticated. The attack succeeds not because of a flaw in the developer's code, but because of a vulnerability in the platform's own core engine. The platform's lack of input sanitization for its custom syntax creates an injection vulnerability that bypasses all of the developer's security controls.


## Example Risk Scenarios

### Scenario #1

A citizen developer uses a low code / no code platform to create a simple online form. The form is designed to take a user’s input and simply show it back to them on the screen. The platform contains its own special internal development syntax for easy data reference within the application and is used to easily reference the form’s data and output it. Because this syntax is specific to the platform, it is not accounted for in common security input sanitization mechanisms. An attacker can discover this form and enter a command using the platform’s internal development syntax to reveal company information stored within the application and other sensitive data. 

### Scenario #2

A citizen developer sets up an automation script using an AI assistant that triggers every time a new publication is made to an RSS feed and stores it into a SQL database. An attacker controlling the feed can use this flow to inject commands into the database and delete important records.

### Scenario #3

A citizen developer creates an application that allows users to fill out forms. The app encodes form data as CSV files and stores them on a shared drive. Even though the platform sanitizes form inputs for SQL injection attacks, it does not sanitize for Office macro attacks. An attacker can take advantage of this oversight and input a macro that gets written into the CSV file and executes when a user opens the file.


## Prevention

- Sanitize user input, taking into account the operations that will be performed on that input by the application
- For database interaction via SQL, also use query parameterization, stored procedures, or escaping
- Educate business users on the risk of unsanitized user input. Platforms cannot make this problem go away on their own
- Ensure platform syntax is accounted for in sanitization efforts on a platform level
- Sanitize platform specific syntax to avoid targeted injections
- Use rules and system prompts to instruct code agents to generate input validation logics for form and user input processing, and manually validate generated code.


## References

- [Security vulnerabilities in robotic process automation (RPA) / low code technology: SQL injection & the return of Bobby Tables](https://aabashkin.github.io/posts/rf_sqli#a-modern-example-with-a-low-code--rpa-platform)
- [A03:2021 – Injection](https://owasp.org/Top10/A03_2021-Injection/)
- [SOQL injection security tips](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/pages_security_tips_soql_injection.htm)

