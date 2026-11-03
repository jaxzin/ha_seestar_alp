# Changelog

## 0.1.3 (unreleased)

- Prebuilt image: Home Assistant now pulls `ghcr.io/jaxzin/ha_seestar_alp`
  (amd64 and aarch64, Cosign-signed) instead of building the add-on on the
  device. No functional change from 0.1.2.

## 0.1.2 (unreleased)

- seestar_alp `deploy-2026.11.03.3`: the URL prefix is applied exactly once,
  when a page is rendered, so a prefix that looks like a page path (for
  example `/1`) no longer drops a path segment.

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
