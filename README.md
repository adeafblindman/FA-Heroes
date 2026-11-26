# Charity Ticker 1920 x 56 (OBS / GitHub Pages)

One scrolling line: raised total pinned on the left; next milestone, goal progress and lists rotate past.

Address: `https://adeafblindman.github.io/FA-Heroes/`

## Pick what it shows (event feed, no keys needed)

Data comes from `hd2clans.com/api/public/heroes26`.

| Add to the address | Result |
|---|---|
| (nothing) | Event total and all lists |
| `?campaign=@user/campaign-slug` | That campaign's total (full `https://tiltify.com/...` address also works) |
| `?team=+team-slug` | That team's total (team name also works) |
| `?demo` | Sample data, labelled DEMO DATA |

Only campaigns and teams that appear in the feed can be selected.



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

## Linked events

With live Tiltify data, a campaign that belongs to a fundraising event also shows the event's total
and goal, plus its top fundraisers, teams and donors. The Worker must run the current `worker.js`.

## Donation alerts

With live Tiltify data, each new donation slides a "New donation by" banner over the feed.
Donations already made when the ticker loads do not alert. Allow up to about 20 seconds.
Use the current `worker.js` in your Worker.

| Option | Default | Meaning |
|---|---|---|
| `audio=1` | off | Play a chime with each alert |
| `sound=alert.mp3` | built-in chime | Your own sound file (upload it beside `index.html`); turns audio on |
| `volume` | 60 | 0 to 100 |
| `alerttime` | 7 | Seconds each alert stays up |
| `alertcolor` | `5b7cf5` | Banner color, hex without `#` |
| `alerts=off` | on | Turn alerts off |
| `testalert` | | Repeat a test alert for setup. Remove before going live |

In OBS, tick **Control audio via OBS** on the browser source to get a mixer slider for the sound.

