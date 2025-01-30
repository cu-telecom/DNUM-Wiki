# Encryption

Encryption *could* be optional, but highly encouraged.

## SIP Signalling

to encrpy the SIP signalling it's up for discussion if we use standard certificates from the likes of Let's Encrypt, or operate a CA to issue our own certificates. We will need to sign certificates for the [Verification](verification.md)) part, so it might be more sensible to issue our own.

## Media

For the media streams the default encryption will be SDES, but DTLS / ZRTP etc could also be used.
