# Atrium hello-go

Minimal Atrium web app using Go stdlib (`net/http`, `crypto/hmac`). It is the
second-language Hosting proof after the Node birthday agent.

Default port: **5102** (`PORT` env override).

## Run

```bash
go run .
```

`ATRIUM_SETUP_SECRET` is required. Set `ATRIUM_DATA_DIR` to persist connection
secrets and config across restarts. The hosted container mounts its per-app EFS
access point there. Set `ATRIUM_FRAME_ANCESTORS` to the COHO origin allowed to
embed `/ui`, and set `ATRIUM_PARENT_ORIGIN` to that exact origin for the close
message (for example `http://localhost:4200` in local development).

## Endpoints

Same runtime contract as the Node kit:

- `/health`
- signed `/webhooks/atrium/*`
- signed native config at `/config/schema` and `/config`
- signed iframe quick view at `/ui`
- external app-owned page at `/configure`

For local Store registration, use [`manifest.example.json`](./manifest.example.json).
For Labs, `scripts/provision-atrium-hello-go-labs.sh` builds the image, creates
runtime resources through the generic provisioner, and lists it at
`https://atrium-go-labs.coho.life`.
