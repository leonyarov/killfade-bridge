# killfade-bridge

Settings storage for the KillFade Deadlock addon.

Deadlock addons have no storage that survives a game restart. The game's embedded
browser (`CitadelHTMLPanel`) does, though: it keeps `localStorage` on disk in Steam's
htmlcache. KillFade loads `bridge.html` from GitHub Pages into a hidden 2px panel and
reads and writes its config through it:

- **request:** the URL fragment, `#encodeURIComponent(JSON.stringify({ q, f, k, v }))`, where `f` is `get` or `set`
- **reply:** `document.title = "KF_RES:" + JSON.stringify({ q, ok, v, e })`

The page only touches `killfade_*` keys, because every page under `leonyarov.github.io`
shares the same `localStorage`. It sends nothing anywhere, and the fragment never
reaches the server.

Since the 2026-10-01 Deadlock patch the panel only loads `https://` URLs, which is why
this page has to be hosted instead of shipped inside the addon's VPK.
