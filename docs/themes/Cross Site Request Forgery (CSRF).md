tags: #web-security

# Cross Site Request Forgery (CSRF)

links: [[506 WS TOC - OWASP & CSRF|WS TOC - OWASP & CSRF]] - [[themes/000 Index|Index]]

---

### Overview of CSRF

- CSRF is a type of attack that forces a victim's browser to send a pre-authenticated request to a vulnerable web application, effectively performing actions with the user's privileges. This can include actions like changing passwords or logging out.

### How CSRF Works

- The attack exploits the automatic inclusion of user credentials (like session cookies) in requests made by browsers. The success of CSRF depends on the victim being logged into the attacked system. Attackers typically use means like [[505 WS TOC - XSS|XSS]] to modify content on a page the victim visits, triggering unauthorised requests.

### Example of CSRF Attack

- An example is provided where an attacker inserts an image tag `<img src="changepassword.php?newpassword=1234">` in a web page. If the victim has an active session, their password could be changed without their knowledge.

### Protection Strategies

1. **Use of Custom Tokens (CSRF Tokens)**: Applications should use custom tokens that are not automatically submitted by browsers. These tokens should be included in every form and URL.
2. **Validation of Tokens**: The application should verify these tokens, which can be unique for each session or even each page.
3. **Handling Sensitive Transactions**: For sensitive data or transactions, additional measures like re-authentication or transaction signing should be used.
4. **Post Requests**: Use POST methods for sensitive data and avoid using GET requests for these purposes.
5. **Protecting the Token**: Be cautious if including the CSRF token in GET requests, as it can be exposed through browser history, HTTP log files, and URL referrers.
6. **Double Submit Cookies**: This involves sending a random value in both a cookie and as a request parameter, which the server verifies.
7. **Encrypted Token Pattern**: This involves creating a token with user’s ID, timestamp, and nonce, encrypted with a symmetric key, and including it in all requests.
8. **Checking the Referer Header**: While referer headers can be spoofed, they offer some level of protection against CSRF, particularly with unauthenticated requests.
9. **Challenge-Response Techniques**: Using CAPTCHA or re-authentication (like a password) for sensitive actions.

### User-Side Mitigation

- Users can reduce their risk by logging off web applications immediately after use, not saving passwords in browsers, and using different browsers for sensitive applications and general web surfing.

---
links: [[506 WS TOC - OWASP & CSRF|WS TOC - OWASP & CSRF]] - [[themes/000 Index|Index]]