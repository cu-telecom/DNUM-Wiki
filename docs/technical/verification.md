# Verification

To verify the source of a call is permitted to use the presented Caller ID, systems could utilise [STIR/SHAKEN](https://en.wikipedia.org/wiki/STIR/SHAKEN) - a method of cryptographically verify ownership of a number.

This would require a CA to sign certificates with specific extensions, and then issuing them to users.

STIR/SHAKEN is mandated in the US, so it has become well adopted within the standard software SIP server offerings.