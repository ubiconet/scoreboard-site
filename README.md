# ubiconet scoreboard site

Static sales site for the ubiconet scoreboard product line. Hosted on the local Mac mini behind a `cloudflared` tunnel at **https://scoreboards.ubiconet.com**.

## Pages

- `index.html` — landing page, three product cards
- `nhl.html` — NHL Scoreboard (available now)
- `mlb.html` — MLB Scoreboard (coming soon)
- `baseball-miniboard.html` — Baseball MiniBoard (coming soon)

## Editing content

Edit the HTML in place — no build step. Push to `main`, then on the Mac mini:

```bash
cd ~/codingProjects/scoreboard-site
git pull
```

The Python `http.server` is rooted at this directory and serves the working tree on every request — no restart needed.

## Adding product photos / videos

Drop image files into `assets/` (create the folder), then replace the `<div class="placeholder">…</div>` blocks in the relevant page with `<img src="assets/filename.jpg" alt="…">`. Recommended sizes:

- Hero / product photos: 1200 × 800 px (JPEG, ~200 KB)
- Demo videos: keep under 10 MB; host on the same repo in `assets/` or embed a YouTube/Vimeo link.

## Local hosting

A `launchd` plist at `~/Library/LaunchAgents/com.ubiconet.scoreboard-site.plist` runs `python3 -m http.server 8090 --bind 127.0.0.1 --directory ~/codingProjects/scoreboard-site` as a long-lived process. Logs: `~/Library/Logs/com.ubiconet.scoreboard-site.{out,err}.log`.

## External access

`cloudflared` is configured at `~/.cloudflared/config.yml` with an ingress rule mapping `scoreboards.ubiconet.com` to `http://localhost:8090`. DNS is a CNAME in Cloudflare pointing at the existing `bbcore-tunnel`. No new tunnel was created.

## Layout

```
~/codingProjects/scoreboard-site/
├── index.html
├── nhl.html
├── mlb.html
├── baseball-miniboard.html
├── css/style.css
└── assets/         (add photos/videos here when ready)
```
