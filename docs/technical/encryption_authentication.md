# Encryption and Authentication

As we're building something new it makes sense to drag telephony into the 21st century and mandate encryption. As well as preventing eavesdropping, the built-in authentication of mutual TLS will massively improve security, removing some of the concern of leaving a SIP server open to the world.

## SIP Signalling

As we will need to manage a Certificate Authority for the [Verification](verification.md)) part, it makes sense to also issue TLS certificates for Client / Server authentication.

## Media

For the media streams the default encryption will be SDES, but experiments with DTLS / ZRTP would also be permitted.
