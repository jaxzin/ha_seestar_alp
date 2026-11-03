# seestar_alp for Home Assistant

A Home Assistant add-on repository with one add-on: **Seestar Alpaca driver
(seestar_alp)**, which runs the [seestar_alp](https://github.com/smart-underworld/seestar_alp)
ASCOM Alpaca driver and Simple Seestar Controller web UI for ZWO Seestar
telescopes.

> **Status: experimental, pre-release.** Not yet published as a prebuilt image;
> Home Assistant builds it on the device when you install it.

Pair it with [ha-seestar](https://github.com/jaxzin/ha-seestar) for Seestar
telemetry, a preview camera and controls as Home Assistant entities. ha-seestar
finds this driver automatically via ASCOM Alpaca discovery.

## Install

**Settings → Add-ons → Add-on Store → ⋮ → Repositories**, add
`https://github.com/jaxzin/ha_seestar_alp`, then install **Seestar Alpaca
driver (seestar_alp)**. Setup and options: [seestar_alp/DOCS.md](seestar_alp/DOCS.md).

## Source and license

Licensed under the [GNU General Public License v3.0](LICENSE), like seestar_alp
itself.

The add-on image is built from:

- this repository (the add-on packaging: `seestar_alp/`), and
- seestar_alp source at the repository and tag pinned in
  [`seestar_alp/Dockerfile`](seestar_alp/Dockerfile) (`SEESTAR_ALP_REPO`,
  `SEESTAR_ALP_REF`), currently `jaxzin/seestar_alp` at `deploy-2026.11.03`:
  upstream v3.3.1 plus two changes submitted upstream
  ([#789](https://github.com/smart-underworld/seestar_alp/pull/789),
  [#790](https://github.com/smart-underworld/seestar_alp/pull/790)).

seestar_alp is © Kai Yung and the smart-underworld contributors. Its own license
files are preserved in the image under `/app/seestar_alp/`.
