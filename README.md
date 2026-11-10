# seestar_alp for Home Assistant

A Home Assistant add-on repository with one add-on: **Seestar Alpaca driver
(seestar_alp)**, which runs the [seestar_alp](https://github.com/smart-underworld/seestar_alp)
ASCOM Alpaca driver and Simple Seestar Controller web UI for ZWO Seestar
telescopes.

> **Status: experimental, pre-release.** Home Assistant pulls a prebuilt
> multi-arch image, `ghcr.io/jaxzin/ha_seestar_alp`, published by CI from
> `main` for each `version` in `seestar_alp/config.yaml`.

Pair it with [ha-seestar](https://github.com/jaxzin/ha-seestar) for Seestar
telemetry, a preview camera and controls as Home Assistant entities. ha-seestar
finds this driver automatically via ASCOM Alpaca discovery.

> **Setting up the whole Seestar stack?** Start at
> [ha-seestar → Quick Start](https://github.com/jaxzin/ha-seestar#quick-start-home-assistant-os--supervised):
> it installs this driver, the bridge add-on, the dashboard card and the
> optional Seestar Sync archiver in one pass.

## Install

**Settings → Add-ons → Add-on Store → ⋮ → Repositories**, add
`https://github.com/jaxzin/ha_seestar_alp`, then install **Seestar Alpaca
driver (seestar_alp)**. Setup and options: [seestar_alp/DOCS.md](seestar_alp/DOCS.md).

[![Open your Home Assistant instance and show the add add-on repository dialog with this repository pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fjaxzin%2Fha_seestar_alp)

The badge opens the add-repository dialog in your own Home Assistant with that
URL pre-filled. It applies to Home Assistant OS and Supervised installs, the
ones with an Add-on Store.

## Source and license

Licensed under the [GNU General Public License v3.0](LICENSE), like seestar_alp
itself.

The add-on image is built from:

- this repository (the add-on packaging: `seestar_alp/`), and
- seestar_alp source at the repository and tag pinned in
  [`seestar_alp/Dockerfile`](seestar_alp/Dockerfile) (`SEESTAR_ALP_REPO`,
  `SEESTAR_ALP_REF`), currently `jaxzin/seestar_alp` at `deploy-2026.11.10`:
  upstream main plus three changes submitted upstream
  ([#789](https://github.com/smart-underworld/seestar_alp/pull/789),
  [#790](https://github.com/smart-underworld/seestar_alp/pull/790),
  [#791](https://github.com/smart-underworld/seestar_alp/pull/791)) and a cached
  stacked-image endpoint (`feat/stack-snapshot`).

seestar_alp is © Kai Yung and the smart-underworld contributors. Its own license
files are preserved in the image under `/app/seestar_alp/`.
