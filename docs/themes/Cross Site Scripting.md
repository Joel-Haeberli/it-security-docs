tags: #web-security #xss

# Cross Site Scripting

links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[themes/000 Index|Index]]

---

- Problem on websites that allow uncontrolled content uploads by users
	- Forum, guest-book, etc. $\rightarrow$ [[Stored XSS]]
- XSS is generally a problem if a website allows uncontrolled / unsanitized content provided by users / attackers $\rightarrow$ [[DOM-based XSS]], [[Reflective XSS]]
- Javascript can be hidden in <\script> tags, external js files, eventhandlers and URLs

[Good explanation of Same Origin Policy](https://security.stackexchange.com/questions/8264/why-is-the-same-origin-policy-so-important)
[Another good explanation](https://security.stackexchange.com/questions/225228/same-origin-policy-and-xss)

### Testing

The following scripts can be used to test if website is protected against XSS

```javascript

// Display alert
’’;!−−"<XSS>=&{()}

// Load xss.js
<script src=link-to-js.js</script>

// False image loading
<img src="javascript:alert('XSS');">

// The same but using UTF-8 encoding
<IMG SRC=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;...>

```

### Protection

- Data and input validation / sanitation
- Appropriate encoding of output data
	- `&lt;`stays `&lt;`and doesn't turn into `<`
	- Specify character encoding for each page
- "Accept known good" validation
	- Reject invalid input
	- Do not attempt to sanitize potentially hostile data
	- Error messages might also include invalid data
- Java
	- Use `Struts` or `JSF` output validation and output mechanisms
	- Use `JSTL`
	- Do not use `<%= %>`
- .NET
	- use the Microsoft Anti-XSS lib
- PHP
	- Ensure output is passed through `htmlentities()` or `htmlspecialchars()`
	- Content is first validated, then `canonicalize()` to be stored and then the output is encoded using `encodeForHTML()`
- DOM based XSS
	- Use the right output method (sink)
		- `innerText` and `textContent` instead of `innerHTML`
	- Don't use `eval` with user input
- Use `X-XSS-Protection`header which instructs the browser to check for XSS attacks and block the script if one is detected
	- Attacks are identified using patterns in the code that are commonly associated with XSS attacks
- Use `Content-Security-Policy` HTTP header
	- Whitelist of sources from where the browser can load resources
	- Can define default-, script-, object-, style- and img-src
	- Without this setting a website can always call any source
- Be careful with advertisement brokers
	- Websites include scripts provided by ad brokers to show ads
	- Brokers could potentially run any code on the website including the script

---
links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[themes/000 Index|Index]]
