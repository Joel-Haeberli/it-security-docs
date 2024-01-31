tags: #web-security #broken-access-control

# Attacks on Broken Access Control

links: [[502 WS TOC - Broken Access Control|WS TOC - Broken Access Control]] - [[themes/000 Index|Index]]

---

## Attacks

To give an idea what is possible using HTTP to attack broken access control, we will list a few examples here: 

- Access Tax declaration
- Modifying internal keys
- Reading files
- Accessing admin pages

### Australian Taxation Office

Developers of the Australian tax portal used the account-number directly in the userinterface as parameter for the request reading the respective tax reports. A logged in user could simply change the account-number to another valid account-number and got details of this persons taxes.

### Tamper internal keys

Let's say your an attacker an see that a url used by the site you are trying to attack accesses a message from `http://vulnerab.le/messages?id=123`. You could simply try to bruteforce `id` by going through a range of id's and like this maybe read messages you are not supposed to read.

### Reading files

Assume we have a webserver which serves the ToR (Transcript of Record) for all students. The webserver therefore has implemented a webservice which reads the ToR of a student in form of a pdf. The attacker finds out that the pdf filename is the abbreviation of the respective user. With this knowledge he could easily access pdf of other students if the webserver fails to check authorization to do so: `http://vulnerab.le/tor/[ABBREVIATION].pdf`

#### Use file reading service to read interesting files

Assume we have a webserver serving an API which allows the consumer to request a file given its path: `http://vulnerab.le/files?name=[FILEPATH]`

You could now try to access interesting files like the `/etc/passwd/` listing all users of the server. Or maybe if you are a lucky attacker, you can even specify another URL to read a file from like `http://192.168.1.32/some/path/tofile.txt`. Maybe you can gain access to hosts that are not accessible directly due to networking restrictions but using the vulnerable webserver within the same network will let you do so.

### Accessing the admin page

If access control is broken on admin pages (e.g. only looked for active session but not who's session it is, or similar), this can lead to that users with normal privilege gain access to the administrator functionality of the server.

---
links: [[502 WS TOC - Broken Access Control|WS TOC - Broken Access Control]] - [[themes/000 Index|Index]]