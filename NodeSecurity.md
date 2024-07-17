# OWASP

**Minimize DoS Attacks:**

- Inputs and Forms are sanitized and validated
- Mechanisms to prevent looping/creating of data
- Use validator.js or safe-regex package for regex

**Minimize Injections:**

- Always validate and sanitize inputs
- Don't use eval(), setTimeout(), setInterval() to parse input
- Use safer JSON.parse or parseXxx like parseInt()
- Use strict code

## Packages Security

- `npm audit`
  to check audit information of installed dependencies showing vulnerabilities.

- `npm outdated`
  to check if there's any outdated packages. If there's any, then update them to the latest version.

## Data Security

- Handle data with proper validation and sanitization
- Use prepared statements for SQL/NoSQL
- Set proper HTTP headers with Helmet
- Encrypt user data and session management (crypto)

## Server Level Security

- Use HTTPs protocol (SSL certificate)
- Rate limiting against DoS attacks (express-rate-limit, rate-limiter with redis dependency)
- Prevent CSRF attacks (csurf)
- Cookie attributes (cookie-session)

## Tools for Testing

- OWASP dependency check
- Snyk (to find vulnerabilities)
- Burp (for penetration testing)
