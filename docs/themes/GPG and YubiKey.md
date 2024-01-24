tags: #yubikey #GPG

# GPG and YubiKey

links: [[615 SPA TOC - YubiKey|SPA TOC - YubiKey]] - [[themes/000 Index|Index]]

---

- [[GnuPG|GnuPG]] is the de-facto way to use OpenPGP compliant smart cards. `gpg` will access the keys via the `gpg-agent`.
- Analog to the `ssh-agent` gpg is using the `gpg-agent` to access keys. The `gpg-agent` is an integral component of the gpg package.
- The `scdaemon` manages the access to OpenPGP compliant smart cards such as the YubiKey. The low-level communication is via APDU’s.
- The token needs an app installed, which is compliant to OpenPGP smart cards.

![[Pasted image 20240124125054.png]]

## Some usage details

1. **Key Generation for YubiKey**: It's recommended to generate GPG keys on an offline computer. For YubiKey NEO, only 2048-bit RSA key pairs are supported, whereas YubiKey 4 or 5 can support 4096-bit RSA key pairs​​.
2. **SSH Authentication Key**: To use a key for SSH authentication, it should have the authentication capability. This can be added using the `gpg --expert --edit-key` command and selecting the appropriate options​​.
3. **Transferring Keys to Token**: The `keytocard` command is used to transfer key pairs to the token. You can choose to store the key as either a signature key or an authentication key​​.
4. **Token Management with GPG**: Token operations, including setting the PIN, PUK, and labels, are performed using the `gpg --card-edit` command. This command provides various details about the token including application ID, version, manufacturer, and key attributes​​.
5. **Setting PIN/PUK**: In admin mode, you can reset the OpenPGP app, unblock the PIN, or set the PIN/PUK using the `gpg --card-edit` and then `passwd` commands​​.
6. **GPG for SSH Access**: To provide SSH access to GPG keys, point SSH to the gpg-agent using specific commands. You can also pre-specify keys for SSH to avoid using `ssh-add` for loading keys​​.
7. **Extracting and Authorizing Public Key**: To use a GPG authentication key pair for SSH, extract the public key using the `gpg --export-ssh-key` command and authorize it by adding it to the `/.ssh/authorized_keys` file​​.

---
links: [[615 SPA TOC - YubiKey|SPA TOC - YubiKey]] - [[themes/000 Index|Index]]