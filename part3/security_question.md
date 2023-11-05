# Security audit

Using the OWASP Top 10 we have ten different categories to look into when making our case system secure:

## Broken Access Control

First, we need to be careful about access control and make sure we are preventing users from acting outside of their intended permissions. This is because unauthorized access to data can lead to disclosure, modification, or destruction of information. Therefore we need to ensure:

- Not violation of the principle of least privilege and implementation of deny by default. 
- Implementation of access control mechanisms.
- Web server directory listing is disabled and backup files are not present within web roots
- Logging of access control failures
- Stateful session identifiers will be invalidated on the server after logout

## Cryptographic Failures

Next, we need to make sure we are meeting the protection needs of data in transit and at rest. Making sure:

- We are not using legacy protocols for transporting sensitive data.
- We are classifying our data and identifying which data is sensitive (e.g. passwords, costumer information).
- We are not storing sensitive data unnecessarilly.
- That the service we are using is encrypting data at rest and in transit, and how much control we have over encryption checking the general configuration and settings (In this case, we need to explore our AWS Key Management Service (KMS)).

## Injection

Injections like SQL, NoSQL, OS command, and so on are an exploit of security vulnerability that we need to take care of too. We'll need to review our source code looking for vulnerabilities and in general we need to make sure:

- We are using SQL controls within queries to prevent mass disclosure of records in case of SQL injection.
- We are escaping special characters using the specific escape syntax for that interpreter in any residual dynamic query.
- User data is validated, filtered or sanitized by our application.

## Insecure design

Next we need to look for security failures in the design of the system that are not meeting the security requeriments laid down by the organization. Therefore we need to:

- Ensure our development lifecycle met all the security and privacy-related controls
- Established that secure design patterns were used
- Ensure that unit and integration tests were passed.

## Security Misconfiguration

Next we need to make sure the security controls in our system are well configured:

- Unnecessary features are disabled.
- There are no accounts with default passwords.
- Error messages are not overly informative
- The security settings in the application server, frameworks (e.g., Next.js), libraries, and databases are set to secure values.

## Vulnerable and Outdated Components

Also, we need to be careful about the components we are using in our system, and their vulnerabilities. In order to avoid hackers exploiting these, we need to: 

- Make sure unused dependencies, unnecessary features, components, files, and documentation are removed.
- Continuosly inventory of versions of both client-side and server-side components and their dependencies. 
- Make sure components have been obtained from official sources over secure links
- Continuosly monitor libraries and components to determine if the versions we are using are maintained and if there is any newly discovered security vulnerability related to them.

## Identification and Authentication Failures

Next we need to take look into protection against authentication-related attacks, for both our Mobile App and our web. For this we need to make sure:

- We are implementing multi-factor authentication.
- We are not deploying with any default credentials.
- Our passwords checks are not weak, and password length, complexity and rotation policies are aligned with the NIST guidelines.
- There are policies for failed login attempts, and we collect logs when this happens.

## Software and Data Integrity Failures

In order to protect against integrity violation, we need to ensure that:

- We are using digital signatures to verify that the different components used are from an expected source and have not been altered.
- Libraries and dependencies are consuming trusted repositories.
- Our code has passed a review process to minimize the chance that malicious code could be introduced.
- All serialized objects received from the network are validated.

## Security Logging and Monitoring Failures

In order to keep our system secure we need to constantly monitor for possible breaches. Therefore, we need to ensure that our system:

- Logs all login, access control, and server-side input validation failures with sufficient user context to identify suspicious accounts.
- Encodes log data correctly to prevent injections.
- Does not log sensitive data, such as passwords or any personal information.

## Server-Side Request Forgery

Finally we need to be careful about SSRF in which an attacker abuses applications to interact with the internal/external network or the machine itself. As we expect our application to only send requests to identified and trusted applications we need to do the following:

- Make sure our application does not accept URLs from the user, and only accepts valid IP addresses or domain names.
- Make sure that only allowed routes are available for the application.
- Sanitize and validate all client-supplied input data.
