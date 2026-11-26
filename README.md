# Charity Ticker 1920 x 56 (OBS / GitHub Pages)

One scrolling line: raised total pinned on the left; next milestone, goal progress and lists rotate past.

## Put it online

1. Upload `index.html` to this repo, replacing the old one. Keep `FSSinclair-Medium.otf` beside it.
2. Repo **Settings > Pages**: Source "Deploy from a branch", branch `main`, folder `/ (root)`.
3. In OBS add a **Browser** source with your address, width **1920**, height **56**.

Address: `https://adeafblindman.github.io/Heros2026/`

## Pick what it shows (event feed, no keys needed)

Data comes from `hd2clans.com/api/public/heroes26`.

| Add to the address | Result |
|---|---|
| (nothing) | Event total and all lists |
| `?campaign=@user/campaign-slug` | That campaign's total (full `https://tiltify.com/...` address also works) |
| `?team=+team-slug` | That team's total (team name also works) |
| `?demo` | Sample data, labelled DEMO DATA |

Only campaigns and teams that appear in the feed can be selected.

## Live Tiltify data (milestones, donations, targets, polls)

Tiltify needs a client secret, and everything on GitHub Pages is public, so a small free
Cloudflare Worker holds the secret.

1. At https://app.tiltify.com/developers create an application. Note the Client ID and Client Secret.
2. At https://dash.cloudflare.com create a Worker, choose **Edit code**, paste in `worker.js`, and deploy.
3. In the Worker's **Settings > Variables and Secrets** add two secrets:
   `TILTIFY_CLIENT_ID` and `TILTIFY_CLIENT_SECRET`.
4. Add your Worker address to the ticker address:

```
?proxy=https://NAME.YOURNAME.workers.dev&campaign=@user/campaign-slug
?proxy=https://NAME.YOURNAME.workers.dev&team=+team-slug/team-campaign-slug
```

To leave `proxy=` off, paste the Worker address into `DEFAULT_PROXY` near the top of the script in
`index.html`. With that set, **all** data comes from Tiltify, so `campaign=` or `team=` is required.
In this mode `team=` means a **team campaign** (`+team/campaign`), not just the team.

If your pages are served from a different domain, set an `ALLOWED_ORIGIN` variable on the Worker.

## All address options

Join with `&`. Use `%20` for spaces.

| Option | Default | Meaning |
|---|---|---|
| `campaign` | | Campaign address or ID (`fundraisers` still works as an alias) |
| `team` | | Team to show |
| `proxy` | | Your Worker address; switches to live Tiltify data |
| `panels` | all | Feed sections and order: `campaign,next,donations,milestones,targets,polls,fundraisers,campaigns,donors,teams` |
| `milestones` | | Your own list: `2500:Costume%20stream\|5000:Hot%20sauce` |
| `maxitems` | 5 | Entries per list |
| `speed` | 90 | Scroll speed, pixels per second |
| `refresh` | 30 (15 with proxy) | Seconds between updates |
| `name` | Heroes 26 | Event name in the feed |
| `api` | hd2clans heroes26 | Different event feed address |
| `accent` `bar` `text` `subtext` `track` `bg` | | Colors, hex without `#` |
| `font` | FSSinclair | Font family |
| `position` | bottom | `top`, `center`, `bottom` if the source is taller than 56 |

The older `w`, `h`, `rotate`, `entry` and `title_*` options no longer do anything.
