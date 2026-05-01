# Cloudflare
This container works in combination with my domain configured through Cloudflare
to act as a Dynamic DNS (DDNS) client.
Dynamic DNS automatically updates DNS records when the non-static public home IP changes.

To function correctly, I configured a Cloudflare API key with permission to manage
my Cloudflare zones (domains).

I am not using my main domain but instead the subdomain "[vpn.nicoshl.de](http://vpn.nicoshl.de)",
since I only need to point a domain to my homelab for VPN access.
The top-level domain and remaining subdomains are reserved for local IP address routing.

```yaml
environment:
  - API_KEY=${API_KEY}
  - ZONE=nicoshl.de
  - SUBDOMAIN=vpn
  - PROXIED=false
  - RRTYPE=A
```

`RRTYPE=A` specifies the use of an A-Record, meaning we are using IPv4 addresses.
An AAAA-Record would indicate IPv6.

`PROXIED=false` is required because Cloudflare does not support tunneling UDP traffic,
which is needed for WireGuard VPN. Proxying through Cloudflare would
hide the public IP from third parties.
