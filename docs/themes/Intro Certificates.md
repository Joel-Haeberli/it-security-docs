tags: #SPA #certificates
 
# Intro Certificates

links: [[611 SPA TOC - Certificates and PKI|SPA TOC - Certificates and PKI]] - [[themes/000 Index|Index]]

---

This topic was already handled in [[207 AC2 TOC - X.509|AC2 X509]]. This document adds some redundancy but summarizes the talking points discussed in the module SPA. 

## Key assignment

A cryptographic key consist of a pair of numbers. One number should be huge. Example RSA:

- Exponent 65537 (Ox100001)
- Modulus:

```
00:9b:44:c9:46:b6:a5:0e:05:82:b3:f1:c5:06:cf:
e6:91:3b:52:37:6a:35:0e:9b:91:5a:b4:91:16:1b:
90:32:a8:2f:67:53:62:2e:74:84:1a:77:ba:77:ff:
54:a9:36:7c:c3:d3:e1:9b:b7:49:7c:28:b5:fe:b2:
07:b6:bb:ba:38:05:be:f9:6d:de:f9:d6:93:94:88:
80:a0:4e:7d:8f:5c:21:81:01:60:82:2e:49:82:72:
e5:38:f3:e1:7d:85:11:63:07:74:cf:42:a9:2c:4c:
6e:75:39:dc:a7:82:cf:6d:44:eb:ac:2a:d0:7b:75:
5d:7b:a1:3b:77:81:7d:eb:e3:12:33:5b:4a:35:e1:
b4:90:bf:0d:00:67:6e:78:0f:a5:e1:ff:d8:45:a6:
58:47:4a:21:80:33:c2:3b:fe:c2:cb:2f:f4:d1:c7:
ab:be:6a:bf:c0:70:64:ab:eb:19:a4:89:7c:16:f3:
9a:32:77:c8:52:2e:e6:d1:78:bc:e8:4e:0e:f6:9d:
28:c0:9f:4b:c5:11:ff:43:1b:d9:d7:f8:5e:33:b3:
45:56:3f:fc:c7:69:eb:71:f6:f5:6f:1a:9c:bb:0c:
75:12:58:e9:02:30:40:60:b9:5a:4b:2f:4c:3d:97:
e1:65:f2:e3:7c:e5:d0:8e:42:8f:c1:4c:91:79:8b:
```

## Man-In-The-Middle

![[Man-in-the-middle-swap-keys.png]]

As you can see in the image, an attacker (Eve) may distribute forged public keys to do a man-in-the-middle attack.

- Eve manipulates Alice's Key --> It is important to preserve the integrity of the key
- Eve swaps Alice's key with her own key --> It is important to tag identity information
- The identity information can be faked --> It must be possible to attest the signed information

## Digital Identity

A digital certificate establishes a link between identity and cryptographic key

It contains:

- Identity (hostname, organization, individual) of the protected subject
- Identity of the issuer
- Attributes of the key, the subject, issuer and the certificate itself
- Public key of the subject
- Signature form the issuer covering all certificate contents

If the issuer (signer) and the subject are the same entity we talk of "self-signed" certificates. The subject is self-signing its certificate.

---
links: [[611 SPA TOC - Certificates and PKI|SPA TOC - Certificates and PKI]] - [[themes/000 Index|Index]]