# Verification

To verify the source of a call is permitted to use the presented Caller ID, systems could utilise [STIR/SHAKEN](https://en.wikipedia.org/wiki/STIR/SHAKEN) - a method of cryptographically verifying the source of a number. STIR/SHAKEN is now a regulatory requirement in the US, so it's widely supported in the various SIP server offerings.

Implementing our own "private" STIR/SHAKEN implementation would require running a Certificate Authority and "chain of trust" so users can sign and validate the required identity data.

It was initially hoped/assumed that certificates would only be able to sign for numbers which they owned. This functionality is mentioned in the RFC but hasn't been implemented as part of the US regulatory implementation. Instead the certificates verify the "Service Provider Code" of the service provider that originated the call.

After some discussion, it was pointed out that certificates limited to signing the identity of certain numbers probably wouldn't work on the PSTN due to things like number porting, and scenarios where subscribers aren't signing their own calls, but are presenting the same CLI via multiple outbound carriers.

One possible idea would be to use DNS TXT records to define the "Service Provide Codes" permitted to originate a particular Caller ID, much like the [Sender Policy Network](https://en.wikipedia.org/wiki/Sender_Policy_Framework) used with email. 