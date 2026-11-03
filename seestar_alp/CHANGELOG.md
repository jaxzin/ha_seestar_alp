# Changelog

## 0.1.1 (unreleased)

- Fix the SSC web UI in the Home Assistant sidebar: it loaded without its CSS
  and scripts, and its links left the ingress path. seestar_alp now honours the
  standard `X-Forwarded-Prefix` header (`jaxzin/seestar_alp` tag
  `deploy-2026.11.03.2`, proposed upstream), and a small nginx proxy in the
  add-on (ingress port 8099, Supervisor-only) passes Home Assistant's
  `X-Ingress-Path` to it under that name. Live view goes through the same port.

## 0.1.0 (unreleased)

- First version: seestar_alp as a standalone Home Assistant add-on, split out of
  ha-seestar's bundled mode. Built from `jaxzin/seestar_alp` tag
  `deploy-2026.11.03` (upstream v3.3.1 plus smart-underworld/seestar_alp#789 and
  #790). Options: `scopes`, `interop_pem`, `log_level`. SSC web UI via ingress;
  Alpaca (5555) and imaging (7556) ports optional for LAN clients.
