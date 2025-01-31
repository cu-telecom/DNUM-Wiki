# Number Routing

To route calls between platforms we propose utilising an ENUM like service, defined in [RFC6116](https://datatracker.ietf.org/doc/html/rfc6116)

ENUM performs DNS lookups for a number to resolve a Uniform Resource Identifier (URI) to route the call to. A URI might look something like `sip:441632556789@example.com`, which indicates a call should be sent via SIP to the number `441632556789`, on the server that reached at `example.com`

ENUM also supports wildcards, allowing a single record to route an entire prefix, and delegation is also built in to allow a particular prefix, e.g a country code, to be redirected to another DNS server.

## ENUM Overview

[Name Authority Pointer (NAPTR)](https://en.wikipedia.org/wiki/NAPTR_record) records are created on a DNS server, with the full number including country code reversed. e.g for the number 441632556789 you would create the a record for `9.8.7.6.5.5.2.3.6.1.4.4.e164.example.com` that looks something like:

`100 10 "u" "E2U+sip" "!^.*$!sip:441632556789@example.com!" .`

The record has a specific syntax, described below:

| **Field**       | **Value**  | **Explanation** |
|----------------|-----------|----------------|
| **Order**      | `100`     | Defines the processing order. Lower values have higher priority. |
| **Preference** | `10`      | Determines priority among records with the same `ORDER`. Lower values are preferred. |
| **Flags**      | `"u"`     | Specifies the record type: `"u"` (URI), `"s"` (SRV lookup), `"p"` (non-terminal processing). |
| **Service**    | `"E2U+sip"` | Defines the ENUM service `"E2U+sip"` (ENUM to SIP mapping). |
| **Regex**      | `"!^.*$!sip:441632556789@example.com!"` |  A regular expression for rewriting the ENUM query into a target URI. Rewrites any match (`^.*$`) to `sip:441632556789@example.com`. |
| **Replacement** | `.`       | Alternative domain (usually `.` for ENUM records using `REGEX`). No alternative domain; use the result of the Regex directly. |

You can test an example ENUM record for 441632556789 by running the following command. Note the URI doesn't route anywhere:

`dig NAPTR 9.8.7.6.5.5.2.3.6.1.4.4.dnum.cutel.net`

```
; <<>> DiG 9.16.1-Ubuntu <<>> NAPTR 9.8.7.6.5.5.2.3.6.1.4.4.dnum.cutel.net
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 53739
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;9.8.7.6.5.5.2.3.6.1.4.4.dnum.cutel.net.        IN NAPTR

;; ANSWER SECTION:
9.8.7.6.5.5.2.3.6.1.4.4.dnum.cutel.net. 0 IN NAPTR 100 10 "u" "E2U+sip" "!^.*$!sip:441632556789@example.com!" .

;; Query time: 10 msec
;; SERVER: 172.31.48.1#53(172.31.48.1)
;; WHEN: Thu Jan 30 23:51:40 GMT 2025
;; MSG SIZE  rcvd: 157
```

## Secondary DNS servers

It's hoped that users will host secondary DNS servers to reduce load and increase resilience. And for fun!

## Security 

To secure the DNS records its envisioned we'll use DNSSEC, but this is a topic we don't currently know much about. If you do, please get in touch.