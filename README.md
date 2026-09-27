# Bridge Protocol Planner — Offline PWA

4 files, all in this folder:
- `index.html` — the app
- `manifest.json` — makes it installable
- `service-worker.js` — caches everything for offline use
- `icon-192.png` / `icon-512.png` — home screen icons

## Why you can't just double-tap index.html
Service workers (what makes offline mode work) are blocked by every browser on the `file://` protocol. The folder needs to be served over `http://` or `https://` at least once — after that first load, it works with zero connection.

## Fastest way to get it running (no coding, ~1 minute)
1. Go to **netlify.com/drop** in a browser (desktop is easiest for the drag-and-drop).
2. Drag this whole `bridge-protocol-pwa` folder onto the page.
3. It gives you a live `https://...netlify.app` link instantly — open that link on your phone.
4. On iPhone: Share → **Add to Home Screen**. On Android: browser menu → **Install app** / **Add to Home Screen**.
5. Turn on airplane mode and reopen it from the home screen icon — it still works.

## Alternative: run it locally first to test
If you have Python on a computer, from inside this folder:
```
python3 -m http.server 8000
```
Then visit `http://localhost:8000` on that same computer to test it in a browser. To test on your *phone* this way, your phone and computer need to be on the same Wi-Fi, and you'd visit `http://<computer's-local-IP>:8000` instead of localhost — Netlify Drop above is simpler if you just want it on your phone.

## Notes
- Editing the schedule: open `index.html` and edit the `SCHEDULE` array near the top of the `<script>` block — it's plain text, no build step.
- If you ever change `index.html`, bump `CACHE_NAME` in `service-worker.js` (e.g. `v1` → `v2`) so the cache refreshes instead of serving the old version.
