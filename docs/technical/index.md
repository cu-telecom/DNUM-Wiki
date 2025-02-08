# Technical Overview

To operate a telephone "network" there's a few things we need to consider.

## Numbering

Numbering makes up a big part of telephony. We propose a hierarchal approach so numbers can be split between organisations and their sub-organisation, with the potential for more granularity.

For more information, see [Numbering](numbering.md)

## Routing

To route calls between entities, we propose the use of an [ENUM](https://en.wikipedia.org/wiki/Telephone_number_mapping) like system where telephone numbers are mapped to URIs via DNS records.

Whilst ENUM will make up the core of the project, there's scope for translation services such as a SIP 302 redirect server or a HTTPS API.

For more information, see [Routing](routing.md)

## Security

Securing such a network is made up of several parts:

* Authenticating connections between entities. See [Encryption and Authentication](encryption_authentication.md)
* Encrypting the Signalling and Media. See [Encryption and Authentication](encryption_authentication.md)
* Verifying the Caller ID. See [Verification](verification.md)
