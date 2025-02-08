# Numbering

Initially it was assumed that for the UK at least, we'd stick with the existing national numbering scheme, area codes etc. As the idea of DNUM being made up of a hierarchy of autonomous groups has matured, it's become apparent that this might not be the best approach.

Instead something like the following might be more practical:

`+44-1234-12345`

Which could be broken down as:

| Organisation  | Sub-organisation | Subscriber  |
|----------|----------|----------|
| +44 | 1234 | 12345 |

The numbers could be potentially split down further if more granularity is required.

The proposed scheme might result in long numbers that are unpleasant to dial from a rotary phone, but it's assumed that most dialling will take place within your "sub-group" - meaning the prefixes can be omitted.

## Number lengths

One challenge is deciding how long numbers should be, which is largely driven by demand and hard to predict. Too short and they might become quickly exhausted. Too long and they're tedious to dial.

As a work around, a version number could be added to the ENUM record, e.g 5.2.3.6.1.4.4.**v0**.dnum.org. Then as number exhaustion approaches, existing numbers could be prefixed with a 1 and the version incremented - our very own [PhONEday](https://en.wikipedia.org/wiki/PhONEday)! 

To minimise disruption, existing DNS records could be prefixed and copied over to the new version but the previous records would be retained. If systems haven't updated their lookup version, they will still be able to call the same numbers as before, but won't have access to any new numbers issued after the migration. Some thought still needs to be given on how this is handled from the answering side. URIs could be mapped to UUIDs to avoid having to update them, or systems could be configured to route calls based on the last X digits so they continue to function once prefixed. This will likely be decided by what systems can support.
