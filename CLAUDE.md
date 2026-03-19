# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repo supports on-site testing and development work for the Schneider customer engagement. It houses configuration, scripts, and documentation for running demo applications and providing remote access to field hardware (Advantech boxes) via Tailscale + Docker tunnels.

## Infrastructure

### Advantech Box SSH Tunnel

A Docker container (`advantech-tunnel`) bridges the Tailscale network to the Advantech box on the local LAN:

- **Container**: `alpine:latest` running `socat`
- **Listens**: `100.101.195.62:2222` (Jeremy's MacBook Tailscale IP)
- **Forwards to**: `192.168.8.250:22` (Advantech box on local network)
- **Access from Tailnet**: `ssh -p 2222 <user>@100.101.195.62` or `ssh -p 2222 <user>@jeremys-macbook-pro-1`

### Running Demo Containers

| Container | Image | Port | Purpose |
|-----------|-------|------|---------|
| `mwc-demo-ui-app-lan-1` | `mwc-demo-ui:local` | 3004 | MWC demo UI |
| `mwc-demo-ui-mediamtx-1` | `mwc-demo-mediamtx:local` | 8554 (RTSP) | Media streaming relay |
| `forklift-demo-app-1` | `forklift-demo:local` | 6006 | Forklift demo app |
| `forklift-demo-test-app-1` | `forklift-demo-test:local` | 6007 | Forklift demo test instance |

### Tailscale Nodes

| Node | IP | OS | Notes |
|------|----|----|-------|
| jeremys-macbook-pro-1 | 100.101.195.62 | macOS | Primary dev/test machine, runs tunnel |
| atai-office | 100.85.136.38 | linux | Tagged device |
| desktop-bpc1ufq | 100.96.109.74 | windows | NVI5G lab |
| toulouse | 100.93.58.17 | linux | Tagged device |
