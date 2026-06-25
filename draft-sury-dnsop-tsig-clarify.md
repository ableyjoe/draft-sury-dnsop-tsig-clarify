---
title: "Handling Verification Failures of TSIG-Signed DNS Messages"
#abbrev: "TODO - Abbreviation"
category: std

docname: draft-sury-dnsop-tsig-clarify-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Operations and Management"
workgroup: "Domain Name System Operations"
keyword:
 - transaction signatures
 - tsig
 - dns
venue:
  group: "Domain Name System Operations"
  type: "Working Group"
  mail: "dnsop@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/dnsop/"
  github: "ableyjoe/draft-sury-dnsop-tsig-clarify"
  latest: "https://ableyjoe.github.io/draft-sury-dnsop-tsig-clarify/draft-sury-dnsop-tsig-clarify.html"
updates: RFC8945

author:
 -
    fullname: Ondrej Sury
    organization: ISC
    email: ondrej@isc.org
 -
    fullname: Joe Abley
    organization: Cloudflare
    email: jabley@cloudflare.com

normative:

informative:

--- abstract

Transation Signatures (TSIG) provide a standard mechanism to sign
DNS messages, so that the authenticity of messages can be verified
by the system that receives them. This document updates the required
behaviour of a system that receives a signed message that fails
verification.

--- middle

# Introduction

Transaction Signatures are specified in {{!RFC8945}} and provides
a mechanism for transaction-level authentication of DNS messages
using shared secrets and one-way hash functions. It can be used to
authenticate messages exchanged between DNS clients and servers,
e.g. in cases where message integrity and authorisation are important,
such as DNS Update {{?RFC2136}} and the DNS Zone Transfer Protocol
{{?RFC5936}}.

# Terminology

{::boilerplate bcp14-tagged}

This document assumes familiarity with terminology specific to the
Domain Name System (DNS) as described in {{!RFC9499}}.

# Processing of Signed Responses

The processing of a signed response by a DNS client is described
in section 5.4 of {{!RFC8945}}, which includes the following in the
case of signed messages that fail verification:

> Regardless of the RCODE, a message containing a TSIG RR that is
> unsigned as specified in Section 5.3.2 or that fails verification
> SHOULD NOT be considered an acceptable response, as it may have
> been spoofed or manipulated. Instead, the client SHOULD log an
> error and continue to wait for a signed response until the request
> times out.

If we assume that such a response is malicious, then the possible
attacks can be categorised as on-path or off-path.

In the case of an off-path attack, the specified behaviour is not
ideal since it provides an increased window of opportunity for an
attacker that has correctly guessed parameters such as source port
and query id to continue sending responses with different signatures.

In the case of an on-path attack, there is even less value in waiting
for a valid response.

This document updates the specification in this case to clarify
that clients that receive responses that fit the description quoted
above SHOULD log an error and MUST treat the message as corrupt,
MUST discard it immediately and MUST NOT continue to wait.

# Security Considerations

This document updates {{!RFC8945}} and provides new guidance in
order to mitigate on-path and off-path attacks on signed DNS
responses.

# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.


normative:

informative:

...

--- abstract

TODO Abstract


--- middle

# Introduction

TODO Introduction


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
