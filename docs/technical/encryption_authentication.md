# Encryption and Authentication

Where possible Mutual TLS should be used to encrypt and authenticate the SIP signalling between SIP servers. This both prevents eavesdropping and reduces the risk of leaving a SIP server open to the world, as only servers with a signed client certificate will be able to connect. For encrypting the media streams, SDES, DTLS or ZRTP could be utilised.

As we will need to manage a Certificate Authority for the [Verification](verification.md)) part, it makes sense to also issue TLS certificates for Client / Server authentication.

On older more obscure systems this might not be supported, so whether encryption/authentication is mandatory will be decided by local policy.