# LazyWigle
Used to bulk upload Wigle files using the API.
# WiGLE Bulk Uploader

A single-file, no-install HTML tool for bulk-uploading WigleWifi CSV files to [WiGLE.net](https://wigle.net) using their API — built to fill the gap left by the discontinued WiGLEuploader desktop app.

Drop in multiple wardriving CSVs, hit one button, and they upload sequentially with live status per file.

## Why

WiGLE's web UI only accepts one file at a time. This tool lets you queue up a whole folder of captures (e.g. from a wardriver.uk device, WiGLE WiFi Wardriving app, or Kismet exports converted to WigleWifi format) and send them all with a single click, using your WiGLE API credentials instead of a browser session login.

## Features

- Drag-and-drop or file-picker selection of multiple `.csv` files
- Sequential upload with a short delay between files to respect WiGLE's rate limits
- Per-file live status (pending / uploading / success / error) with the raw API response shown inline
- Failed uploads stay in the queue so you can retry just those
- No backend, no build step, no dependencies — just open the HTML file in a browser

## Requirements

- A WiGLE account
- A WiGLE **API Name** and **API Token** (not your website login) — generate these from your [WiGLE account page](https://wigle.net/account)
- Any modern desktop browser (Chrome, Firefox, Edge)

## Usage

1. Download `LazyWigle.html` from this repo.
2. Open it directly in your browser (double-click the file — no server required).
3. Enter your **API Name** and **API Token**.
4. Optionally enter your **observer** name (your WiGLE username, for upload credit).
5. Drag in your CSV files, or click the dropzone to browse.
6. Click **Upload all**.
7. Watch each row update to `success` or `error`. Retry failed files by clicking **Upload all** again — completed files are skipped.

## Security notes

- Credentials are held only in page memory (a JS variable in the DOM) — nothing is written to localStorage, cookies, or disk.
- Requests go directly from your browser to `api.wigle.net` over HTTPS. There is no intermediary server.
- Refreshing or closing the page clears everything.
- Review the source yourself before running it — it's plain, unminified HTML/JS, easy to audit in a few minutes.

## Known limitations

- **CORS**: this calls WiGLE's API directly from the browser. If your browser or a security extension blocks the cross-origin request, uploads will fail with a network error rather than a WiGLE response. Try a different browser, or run the upload from a local script instead (see below).
- WiGLE enforces daily rate limits on API uploads; if you hit them, you'll see the error surfaced in that file's status row.
- Only `.csv` files are accepted; the WigleWifi header format is not validated client-side, so malformed files will fail on WiGLE's end.


## License

MIT — do whatever you want with it.
