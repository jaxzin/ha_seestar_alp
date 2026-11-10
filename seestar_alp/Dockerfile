# syntax=docker/dockerfile:1
# seestar_alp ASCOM Alpaca driver as a Home Assistant add-on.
#
# Debian (glibc) because opencv-python ships no musllinux wheels; manylinux
# wheels cover every compiled dependency on amd64 and aarch64. The HA base
# image is multi-arch and brings s6-overlay v3 + bashio.
FROM ghcr.io/home-assistant/base-debian:trixie-2026.10.3

# seestar_alp source. jaxzin/seestar_alp at deploy-2026.11.10 is upstream main
# (092e15b, after v3.3.1) plus smart-underworld/seestar_alp#789 (mount mode
# exposed only once confirmed), #790 (serialized command ids / socket writes,
# single-flight reconnect), #791 (web UI under a reverse-proxy sub-path via
# X-Forwarded-Prefix) and the fork's cached stacked-image endpoint
# (GET /<dev>/snapshot.jpg on the imaging port, used by ha-seestar's live
# camera). Move to an upstream tag once these ship in a release.
ARG SEESTAR_ALP_REPO=https://github.com/jaxzin/seestar_alp
ARG SEESTAR_ALP_REF=deploy-2026.11.10

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Interpreter + the shared libs the manylinux wheels don't bundle: opencv needs
# libGL and libgthread (libglib2.0-0t64 on trixie). git clones the source and
# serves the pyindi git requirement. nginx is the ingress shim (see
# rootfs/etc/nginx/ingress.conf).
# hadolint ignore=DL3008
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        git \
        python3 \
        python3-venv \
        libgl1 \
        libglib2.0-0t64 \
        nginx \
    && rm -rf /var/lib/apt/lists/*

# Debian's python is PEP 668 externally-managed: install into a venv first on
# PATH, which s6 (with-contenv) passes on to the service scripts.
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:${PATH}"

RUN git clone --depth 1 --branch "${SEESTAR_ALP_REF}" "${SEESTAR_ALP_REPO}" /app/seestar_alp \
    && pip install --no-cache-dir -r /app/seestar_alp/requirements.txt

COPY rootfs /
WORKDIR /app/seestar_alp

# glibc gives each thread (the imaging server alone serves on 15) its own
# malloc arena, and freed full-resolution image buffers stay mapped there, so
# the driver's memory crept up by hundreds of MB on a 4 GB host. Two arenas
# keep it flat (measured 383-394 MB over a stacking session).
ENV MALLOC_ARENA_MAX=2
