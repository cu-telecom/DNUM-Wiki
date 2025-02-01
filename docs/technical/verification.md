# Verification

To verify the source of a call is permitted to use the presented Caller ID, systems could utilise [STIR/SHAKEN](https://en.wikipedia.org/wiki/STIR/SHAKEN) - a method of cryptographically verifying the source of a number. STIR/SHAKEN is now a regulatory requirement in the US, so it's widely supported in the various SIP server offerings.

Implementing our own "private" STIR/SHAKEN implementation would require running a Certificate Authority and "chain of trust" so users can sign and validate the required identity data.

It was initially hoped that certificates would only be able to sign for numbers which they owned. This functionality is mentioned in the RFC but hasn't been implemented as part of the US regulatory implementation, so isn't well documented and hasn't been included in Asterisk. There might be a way of hacking around this by abusing the "ServiceProviderCode" to infer a prefix, but this will require testing.