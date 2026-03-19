# schneider-support

Test and support environment for the Schneider customer engagement. This machine runs demo applications and provides remote access to field hardware (Advantech boxes) over Tailscale.

## Advantech Box — Remote SSH Access

A Docker container on Jeremy's MacBook bridges the Tailscale network to the Advantech box on the local LAN using `socat`.

**From any machine on the Tailnet:**

```bash
ssh -p 2222 <advantech-user>@100.101.195.62
# or by hostname:
ssh -p 2222 <advantech-user>@jeremys-macbook-pro-1
```

**Requirements:**
- Connected to the same Tailnet
- Jeremy's MacBook must be online with the `advantech-tunnel` container running
- MacBook must have local network access to the Advantech box (`192.168.8.250`)

**How it works:**

```
Tailnet peer ──► 100.101.195.62:2222 (socat in Docker) ──► 192.168.8.250:22 (Advantech box)
```

## Running Demo Apps

| App | URL | Purpose |
|-----|-----|---------|
| MWC Demo UI | `http://localhost:3004` | MWC demo interface |
| MWC MediaMTX | `rtsp://localhost:8554` | RTSP media relay |
| Forklift Demo | `http://localhost:6006` | Forklift demo app |
| Forklift Demo (test) | `http://localhost:6007` | Forklift demo test instance |
