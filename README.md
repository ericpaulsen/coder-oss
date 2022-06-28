# Deploying Coder OSS

This repo includes the setup for my [Coder OSS](https://github.com/coder/coder) deployment. Makes use of an external PostgreSQL DB, a Caddy service, and a GitHub OAuth application.

## Dependencies

- [Coder](https://github.com/coder/coder/releases/)
- A [PostgreSQL](https://www.postgresql.org/download/) instance
  - Coder ships with a built-in PostgreSQL DB, so creating a separate one is optional
- [Caddy](https://caddyserver.com/docs/) server

## Setup Notes

You can deploy Coder on any compute method of your choosing (local, VM, etc.).
I provisioned Coder on a dedicated VM in GCP with a static IP that resolves to my domain name. A compute instance of 2CPU & 2GB of RAM should hold up just fine for an small deploy with 10-15 concurrent users.

Additionally, I recommend running the above binaries as system services, so they can be automatically started by the host upon boot.

## Steps

1. [Set up PostgreSQL](https://github.com/coder/coder/blob/main/docs/install/postgres.md#postgresql)

1. Install Coder via: `curl -L https://coder.com/install.sh | sh`

1. [Install Caddy](https://caddyserver.com/docs/install) and create a `Caddyfile` similar to the one in this repo

1. [Set up OAuth](https://github.com/coder/coder/blob/main/docs/install/oauth.md) to enable login via GitHub

1. Copy over my `coder.env` from this repo into `/etc/coder.d/coder.env` and replace with your respective values

1. Run `sudo systemctl enable --now coder` to start Coder now and upon reboot.

**Note:** You can view the logs via: `journalctl -u coder.service -b`
