# Encryption

Encryption *could* be optional, but highly encouraged.

## SIP Signalling

to encrypt the SIP signalling it's up for discussion if we use standard certificates from the likes of Let's Encrypt, or operate a CA to issue our own certificates. We will need to sign certificates for the [Verification](verification.md)) part, so it might be more sensible to issue our own. Running our own CA would help protect against bots and scanners, although scanning over TLS is minimal.

## Media

For the media streams the default encryption will be SDES, but DTLS / ZRTP etc could also be used.
