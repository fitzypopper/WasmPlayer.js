# WasmPlayer.js

Offline backup of the Roblox **WebClient (browser player) build**
`version-f4a4dba57f874ad0-RobloxWebClient` (`0.745.0.7451142`, LIVE channel).

The live CDN (`setup.rbxcdn.com/webclient/…`) started returning **403 Forbidden**
for the whole version directory, so the assets were recovered from two sources:
the local Brave browser cache (Chromium blockfile carver) and Wayback Machine
snapshots captured on **2026-10-28**, before the files went dead.

## Files

| File | Size | SHA-256 (first 12) | Recovery source |
|---|---|---|---|
| `WebClient.wasm` | 101,275,588 B | `ffeb536af6b5` | archive.org `20261028031147` (`id_` raw, was ~34 MB gzipped) |
| `WebClient.js` | 125,172 B | `099dc43095d6` | Brave cache block `f_000d1d` (26,327 B gzip on wire) |
| `WasmPlayer.js` | 76,099 B | `a99c299feb2e` | Brave cache block `f_000d1b` (26,327 B gzip on wire) |
| `WebFlags.json` | 156 B | — | archive.org `20261028094936` |
| `WebClient.metadata.json` | 3,295,454 B | `64a25c194035` | archive.org `20261028022835` (gzip → decompressed) |
| `clientsettings_user-channel.json` | 22 B | — | live API snapshot |
| `clientsettings_client-version.json` | 103 B | — | live API snapshot |
| `clientsettingscdn_settings.json` | 1,339,485 B | — | live API snapshot |
| `har_summary.txt` | 5.5 KB | — | URL census from the capture |

## Why this exists

The LIVE client-settings channel still pins exactly this version:

```json
{"version":"0.745.0.7451142","clientVersionUpload":"version-f4a4dba57f874ad0"}
```

…but `setup.rbxcdn.com` serves `403` for every file under the version directory
(`WasmPlayer.js`, `WebClient.js`, `WebClient.wasm`, `WebFlags.json`,
`WebClient.metadata.json`), so pages referencing these assets can't boot without
a local substitute. `WebClient.wasm` was never stored in any browser cache —
it only survives in the Oct 28 archive.org crawl.

## CDN status (2026-10-29)

```
https://setup.rbxcdn.com/webclient/version-f4a4dba57f874ad0-RobloxWebClient/
  WasmPlayer.js            403
  WebClient.js             403
  WebClient.wasm           403
  WebFlags.json            403
  WebClient.metadata.json  403
```

Only one Wayback entry exists for `WasmPlayer.js` and it is a 403 snapshot;
`WebClient.js` was never archived — both are covered here from the cache recovery.
(The CDN filenames are mirrored directly in this repo; `WasmPlayer.js` SHA-256
`a99c299f…` predates the outage and is verified intact.)

## Notes

- `WebClient.wasm` is a valid WebAssembly module: `00 61 73 6d 01 00 00 00`
  (`\0asm` v1) at offset 0.
- The recovered JS files are **decompressed plaintext** (the cache stored them
  gzip-encoded). Do not send them with `content-encoding: gzip`.
- For local serving, see the classic mitmproxy-interception setup: put a
  MITM CA in Chromium's NSS store (`~/.pki/nssdb`), run a response-rewriting
  addon on the proxy, and launch `brave --proxy-server="http://127.0.0.1:8080"`.
