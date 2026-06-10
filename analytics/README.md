# Top Sum analytics (Cloudflare free tier)

Write-only telemetry for understanding traffic and the share/challenge funnel.
Gameplay never waits on any of this: the game fires fire-and-forget
`navigator.sendBeacon()` calls at menu / end-of-flight moments, and silently
no-ops when the endpoint is unset, offline, or ad-blocked.

Privacy: no cookies, no IP addresses, no user agents, no identifiers — only
anonymous event counts plus the coarse country code Cloudflare derives anyway.

## Tier 1 — Web Analytics (traffic, referrers, devices)

1. Cloudflare dashboard → **Web Analytics** → *Add a site* → hostname `mli3w.github.io`.
2. Copy the snippet token and paste it into the commented-out
   `cloudflareinsights.com/beacon.min.js` tag near the bottom of `index.html`
   (search for `data-cf-beacon`), then uncomment the tag.

That's it — no hosting change; the game stays on GitHub Pages.

## Tier 2 — Worker + D1 (the share/challenge funnel)

One-time setup from this directory (requires `npm i -g wrangler` and
`wrangler login` with your Cloudflare account):

```sh
wrangler d1 create top-sum-analytics        # copy the printed database_id into wrangler.toml
wrangler d1 execute top-sum-analytics --remote --file schema.sql
wrangler deploy                             # prints the Worker URL
```

Then paste the Worker URL + `/e` into the `ANALYTICS_URL` constant near the
top of `index.html` (search for `ANALYTICS_URL`), e.g.
`https://top-sum-analytics.<your-subdomain>.workers.dev/e`.

### Events tracked

| event             | when                                   | extras                      |
|-------------------|----------------------------------------|-----------------------------|
| `game_start`      | flight begins                          | level                       |
| `game_over`       | flight ends                            | level, score bucket, flag = was-a-challenge |
| `share_score`     | score share button tapped              |                             |
| `challenge_share` | challenge share button tapped          | level                       |
| `challenge_open`  | page loaded with a `?c=` challenge URL | level                       |
| `challenge_accept`| "Take the challenge" tapped            | level                       |
| `challenge_skip`  | challenge banner dismissed             |                             |
| `zoom_fired`      | ZOOOM boost triggered                  |                             |

### Reading the funnel

```sh
# Daily share → open → accept funnel
wrangler d1 execute top-sum-analytics --remote --command "
  SELECT date(ts,'unixepoch') AS day, name, COUNT(*) AS n
  FROM events
  WHERE name IN ('challenge_share','challenge_open','challenge_accept','challenge_skip')
  GROUP BY day, name ORDER BY day DESC, name;"

# Challenge completions and how often the challenger was beaten
wrangler d1 execute top-sum-analytics --remote --command "
  SELECT date(ts,'unixepoch') AS day,
         SUM(CASE WHEN flag=1 THEN 1 ELSE 0 END) AS challenge_flights,
         COUNT(*) AS all_flights
  FROM events WHERE name='game_over' GROUP BY day ORDER BY day DESC;"

# Where players are
wrangler d1 execute top-sum-analytics --remote --command "
  SELECT country, COUNT(*) AS n FROM events
  WHERE name='game_start' GROUP BY country ORDER BY n DESC;"
```

### Free-tier headroom

Workers: 100k requests/day · D1: 100k writes/day, 5M reads/day — orders of
magnitude beyond plausible traffic for this game.
