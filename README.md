# Public No Track Service

A ready to go [No Track] service
available from any internet connection.

[No Track] is a "DNS server which blocks
Tracking websites from creating cookies or sending tracking pixels." [[1]] The
Public No Track Service provides a ready to go No Track server available from
any internet connection. This allows you to:

* Use No Track without any having to set up your own No Track server on every
  network you need it on.
* Use No Track on networks which you don't control.
* Use No Track without any fuss.

## Getting Started

To use the Public No Track Service, configure your device or network to use the
Public No Track DNS Server.

**Public No Track DNS IP v4 --** `103.16.128.210`  
**Public No Track DNS IP v6 --** `2404:9400:1:0:216:3eff:fef0:971f`

## Reliability

The Public No Track Service hasn't seen any action yet and users like you are
needed to test it out! Feedback is welcome in the
[issues list].

It is recommended that you set a secondary DNS server in your device or network
configuration, just in case the Public No Track Service is not available at
some time. The OpenDNS server may be a good secondary server:

**OpenDNS IP v4 --** `208.67.222.222`

## Privacy

The intention is not to invade user's privacy.

At the moment, all DNS queries logged in No Track are reported as originating
from `127.0.0.1`, instead of the user's actual IP address. However
IP addresses for HTTP requests for blocked domains are still logged.

To review the privacy of the service, the server configuration is documented
in [server-config.md](server-config.md).

## Availability

Currently there is only one Public No Track Service DNS Server hosted in
Brisbane, Australia. It works great here in Australia but for users elsewhere in
the world, ping times may be an issue. Please express your interest for a server
in your part of the world in the [issues list]. A suitable funding model will
have to be implemented to support this.

The server doesn't have much resources (1 CPU, 512MB RAM, 10GB storage, 200GB
transfer). It will be interesting to see how much traffic this can handle. If
the server becomes overwhelmed by traffic, it may need to be upgraded. Again, to
do this, a suitable funding model will have to be implemented.

## News

**2017-02-06** - The Public No Track Service GitHub repo was created and Brisbane
server announced to the public. Let's see how it goes!

## Feedback

Any feedback is welcome in the [issues list]. Private feedback is welcome via
email at <matt.r.palermo@gmail.com>.

## Open source server configuration

The configuration used to implement the service is documented in
[server-config.md](server-config.md). Any review or suggestion about the
configuration is welcome. Discussion is welcome in the [issues list]. White-hat
pen testing is also welcome as long as it is not too disruptive.

For responsible disclosure of sensitive security vulnerabilities please email
me at <matt.r.palermo@gmail.com> so I can fix the issue before publishing
the issue.

[1]: https://github.com/quidsup/notrack/blob/master/README.md
[No Track]: https://github.com/quidsup/notrack
[issues list]: https://github.com/mattpalerm/Public-No-Track-Service/issues
