# Public No Track Service Server Configuration

The configuration documented here is intended to reflect the configuration
used in the Public No Track Service servers. It should be kept up to date
as the configuration of the server changes. At the moment, there isn't any
automated deployment configured so this is all done manually via the terminal.

The configuration documented here is presented in roughly the same order as
how the server would be configured from scratch.

## Operating System

An Ubuntu 16.04 LTS image from binary lane is used as the base system.
The system is kept up to date using `apt update && apt upgrade`.

## Users and SSH

Suitable non-root user(s) and SSH access is set up.

## Firewall

Firewall is configured using `ufw`:

```
apt install ufw
ufw default deny incoming
ufw default allow outgoing
ufw allow ssh
ufw allow http
ufw allow https
ufw enable
```

## No Track Installation

No Track is installed using the instructions provided by No Track.

```
wget https://raw.githubusercontent.com/quidsup/notrack/master/install.sh  
bash install.sh
bash create-ssl-cert.sh
```

A username and password is set on `/admin` immediately, with a `30` second retry
time. Https is explicitly used when doing this.

## Enforce HTTPS for /admin

Append the following configuration to the lighttpd configuration file at
`/etc/lighttpd/lighttpd.conf`:

```
$HTTP["scheme"] == "http" {
    $HTTP["host"] =~ ".*" {
        url.redirect = ("^/admin/.*" => "https://%0$0")
    }
}
```

Check configuration and restart lighttpd:

```
lighttpd -t -f /etc/lighttpd/lighttpd.conf
systemctl restart lighttpd
```

## Bind9 Installation

Install the Bind9 DNS server:

```
apt install bind9
```

## Dnsmasq Configuration

Change the port number to `5353`. In `/etc/dnsmasq.conf`, modify the line
declaring the port number to:

```
port=5353
```

Restart dnsmasq:

```
systemctl restart dnsmasq
```

## Bind9 Configuration

Modify the configuration at `/etc/bind/named.conf.options` to:

```
options {
        directory "/var/cache/bind";

        recursion yes;
        allow-query { any; };

        rate-limit {
                responses-per-second 5;
                window 5;
        };

        forwarders {
                127.0.0.1 port 5353;
        };
        forward only;

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        dnssec-enable yes;
        dnssec-validation yes;

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
```

Check the configuration and restart bind:

```
named-checkconf
service bind9 restart
```

## Open DNS port in the firewall

```
ufw allow 53
```
