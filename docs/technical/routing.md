# Number Routing

To route calls between platforms we propose utilisiing an ENUM like platform, defined in [RFC6116](https://datatracker.ietf.org/doc/html/rfc6116)

ENUM uses simple DNS lookups to resolve the URI for a particular number. Wildcards are supported, allowing a single record to route an entire prefix and delegation is also built in to allow a particular prefix, e.g a country code, to be redirected to another DNS server.

It's hoped that users will host secondary DNS servers to reduce load and increase resilience.

To secure the DNS records its envisioned we'll use DNSSEC, but this is a topic we don't currently know much about. If you do, please get in touch.