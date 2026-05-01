# Vaultwarden
Vaultwarden is an *"unofficial Bitwarden-compatible server written in Rust,
formerly known as bitwarden_rs"*.
It allows you to self-host a Bitwarden password manager server using Docker.

The configuration is very straightforward with a minimal compose file. However,
note that the Vaultwarden server is only accessible in the client app and web
interface when served over HTTPS.

**You have to set up your reverse proxy and a DNS record for Vaultwarden before
being able to use the service!**

When using a custom subdomain, you should also set your domain as an environment
variable, in my case: `DOMAIN: "https://pwd.nicoshl.de"`

[![Static Badge](https://img.shields.io/badge/Go%20back-B0B0B0?style=for-the-badge)](../../README.md)
