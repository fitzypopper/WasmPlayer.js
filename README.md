Brave Cache Recovery — Hosted Files
==================================

Two recovered assets from Brave browser cache. Extracted from gzip-compressed cache blocks and decompressed to plaintext JavaScript.

Files
-----
- WasmPlayer.recovered.js — 76,099 B
  Substitutes: https://setup.rbxcdn.com/webclient/version-f4a4dba57f874ad0-RobloxWebClient/WasmPlayer.js (now 403)
- WebClient.recovered.js   — 125,172 B
  Substitutes: https://setup.rbxcdn.com/webclient/version-f4a4dba57f874ad0-RobloxWebClient/WebClient.js (now 403)

Origin
------
Recovered from Brave's Chromium blockfile cache at:
/mnt/windows/Users/Sigge/AppData/Local/BraveSoftware/Brave-Browser/User Data/Default/Cache/Cache_Data
- Block f_000d1b → WasmPlayer (76,099 B gzip → 26,327 B cached)
- Block f_000d1d → WebClient (125,172 B gzip → cached)

Usage
-----
These two files can be hosted anywhere (GitHub Pages, Netlify, etc.) or served locally.
No mitmproxy or CA trust required for static serving — they are plaintext JS, already decompressed.

HAR Summary (~/Documents/har_summary.txt)
- WasmPlayer.js: 200 / 76,099 B
- WebClient.js:   200 / 125,172 B
- WebClient.wasm: 403 / 263 B  (no local cache copy)
- WebFlags.json:  403 / 263 B
- WebClient.metadata.json: 403 / 243 B

Location
--------
~/Documents/
- WasmPlayer.recovered.js
- WebClient.recovered.js
- har_summary.txt
- brave_all.har (full capture)
- brave_cache_recovery_README.txt