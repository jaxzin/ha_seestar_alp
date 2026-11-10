# Seestar Alpaca driver (seestar_alp)

Runs [seestar_alp](https://github.com/smart-underworld/seestar_alp), the ASCOM
Alpaca driver and Simple Seestar Controller (SSC) web UI for ZWO Seestar smart
telescopes, as a Home Assistant add-on.

On its own it gives you the SSC web UI in the Home Assistant sidebar. To get
Seestar telemetry, a preview camera and controls as Home Assistant entities,
also install [ha-seestar](https://github.com/jaxzin/ha-seestar), which finds
this add-on automatically.

## Setup

1. Add this repository: **Settings → Add-ons → Add-on Store → ⋮ →
   Repositories**, then `https://github.com/jaxzin/ha_seestar_alp`.
2. Install **Seestar Alpaca driver (seestar_alp)**.
3. On the **Configuration** tab, list your telescope(s) under **Telescopes**
   and, for firmware 7.18 or newer, paste the interop key (see below).
4. Start it. The **Log** tab shows the rendered scope list, then the driver
   connecting to each scope.
5. **Open Web UI** opens the SSC.

> **One control client at a time.** A Seestar serves its command channel to one
> client. Don't run this add-on and another seestar_alp (or the Seestar phone
> app's control session) against the same scope at once.

## Options

| Option | Default | Description |
|---|---|---|
| `scopes` | `[]` | One `{name, host}` entry per telescope: a display name and the scope's LAN IP or hostname. Clients like ha-seestar name their Home Assistant device after `name`, so renaming a scope creates a new device there. |
| `interop_pem` | `""` | Firmware 7.18+ interop auth key (RSA private key). Paste the PEM, the PEM with literal `\n` for newlines (the field is single-line), or its base64. Written to a root-only file on the container's ephemeral filesystem; never logged. Blank = unauthenticated. |
| `log_level` | `info` | Driver log verbosity: `trace`, `debug`, `info`, `notice`, `warning`, `error`, `fatal`. |

### Firmware 7.18+ authentication

Newer firmware gates the scope's command channel behind a challenge-response
key. Without it the event stream (imaging telemetry) still flows, but device
state queries and every command are refused. The key is not distributed with
this add-on; see the [seestar_alp project](https://github.com/smart-underworld/seestar_alp)
and its community.

## Network

| Port | What | Reachable from |
|---|---|---|
| 5432 | SSC web UI | Home Assistant ingress (sidebar), via the built-in proxy on 8099 |
| 5555 | ASCOM Alpaca API | Other add-ons always; your LAN if you enable the port |
| 7556 | Imaging server (live view stream, and `/<device>/snapshot.jpg`: the stack in progress as one JPEG) | Other add-ons always; your LAN if you enable the port |
| 32227/udp | ASCOM Alpaca discovery | Other add-ons on the Supervisor network |

Clients on the Supervisor network (such as ha-seestar) find the driver with
standard ASCOM Alpaca discovery, so nothing needs publishing for them.

## Licensing

seestar_alp and this add-on's packaging are licensed under the GNU General
Public License v3.0. The image is built from the public source pinned in the
[Dockerfile](https://github.com/jaxzin/ha_seestar_alp/blob/main/seestar_alp/Dockerfile)
(`SEESTAR_ALP_REPO` at `SEESTAR_ALP_REF`); see the repository README.
