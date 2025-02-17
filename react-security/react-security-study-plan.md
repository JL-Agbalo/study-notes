# React Security Checklist

## Authentication & Authorization

- [ ] Use secure authentication (OAuth, JWT, etc.)
- [ ] Protect routes with authentication guards
- [ ] Implement role-based access control (RBAC)

## Secure API Communication

- [ ] Use HTTPS for all API requests
- [ ] Prevent Cross-Origin Resource Sharing (CORS) issues properly
- [ ] Store API keys securely (environment variables, backend)

## Preventing XSS (Cross-Site Scripting)

- [ ] Sanitize user input
- [ ] Use React’s `dangerouslySetInnerHTML` cautiously
- [ ] Validate and escape data before rendering

## Preventing CSRF (Cross-Site Request Forgery)

- [ ] Use CSRF tokens for state-changing requests
- [ ] Use `SameSite` cookies for session management

## Protecting Against Clickjacking

- [ ] Use `X-Frame-Options` in headers
- [ ] Use Content Security Policy (CSP)

## Secure Local Storage Usage

- [ ] Avoid storing sensitive data in localStorage/sessionStorage
- [ ] Use HttpOnly and Secure cookies for authentication

## Handling Dependencies Securely

- [ ] Regularly update dependencies (`npm audit`, `yarn audit`)
- [ ] Avoid using outdated or vulnerable libraries
- [ ] Use security tools like `snyk` or `dependabot`

## Other Best Practices

- [ ] Disable React Developer Tools in production
- [ ] Implement rate limiting and bot protection
- [ ] Use security headers (CSP, HSTS, XSS Protection)
- [ ] Log and monitor security events
