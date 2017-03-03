# Public No Track Service

**This service has been discontinued**

The Public No Track Service was an experiment where a ready to go [No Track]
service was made available from any internet connection.

[No Track] is a "DNS server which blocks
Tracking websites from creating cookies or sending tracking pixels." [[1]] The
Public No Track Service provided a ready to go No Track server available from
any internet connection. This allowed you to:

* Use No Track without any having to set up your own No Track server on every
  network you need it on.
* Use No Track on networks which you don't control.
* Use No Track without any fuss.

The service has been discontinued for two reasons:

* Using [No Track] in this way is not secure as discussed in
  [No Track Issue #210].
* The VPS provider that was being used has politely asked not to run an open,
  recursive, DNS resolver on their system.

## Security

As mentioned above, using No Track in the way that has been presented here
is insecure. A discussion about this can be found in [No Track Issue #210].
Essentially, when requests are blocked and re-routed to the No Track server
instead, the No Track server is actually pretending to be the original server.
For good reasons, HTTPS is designed such that no server can pretend to be
another server. This keeps you safe from entering in your bank credentials into
a server pretending to be your bank. To get around this, when No Track returns
alternative content for a blocked request, it must do so without a valid HTTPS
connection. This leaves the user susceptible to "man in the middle" attacks where
an attacker which controls some part of the network between the No Track server
and the user can manipulate these blocked requests in any way they want without
detection.

To mitigate against this vulnerability, No Track users need to be able to trust
the route between themselves and the No Track server. This means that No Track
is perfectly safe when used as it was intended, in your own local network.
It could also be made safe by creating and using a virtual private network (VPN)
where both the user and No Track server could safely communicate over an
artificially secure network.

## Availability

The service was originally hosted on a budget VPS (1 CPU, 512MB RAM,
10GB storage, 200GB transfer). This was more than enough to handle the small
number of requests that it received very quickly.

## News

**2017-03-03** - The service has been discontinued due to the reasons listed in
the README.

**2017-02-06** - The Public No Track Service GitHub repo was created and Brisbane
server announced to the public. Let's see how it goes!

## Feedback

Any feedback is welcome in the [issues list]. Private feedback is welcome via
email at <matt.r.palermo@gmail.com>.

## Open source server configuration

The configuration used to implement the service is documented in
[server-config.md](server-config.md). Any review or suggestion about the
configuration is welcome. Discussion is welcome in the [issues list].

[1]: https://github.com/quidsup/notrack/blob/master/README.md
[No Track]: https://github.com/quidsup/notrack
[issues list]: https://github.com/mattpalerm/Public-No-Track-Service/issues
[No Track Issue #210]: https://github.com/quidsup/notrack/issues/210
