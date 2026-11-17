# gta6-twitch-ccu-bot

[![make.fun · gta6-twitch-ccu-forecast-01](https://make.fun/badge/gta6-twitch-ccu-forecast-01.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![rank](https://make.fun/badge/gta6-twitch-ccu-forecast-01/Shanumameyra/gta6-twitch-ccu-bot/rank.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![reward](https://make.fun/badge/gta6-twitch-ccu-forecast-01/Shanumameyra/gta6-twitch-ccu-bot/reward.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)

Forecasts Twitch viewers in the Grand Theft Auto VI category for hours 2–24 of launch day (19 Nov 2026), five quantiles each, from the hour-1 print and a pooled log-ratio profile fitted at run time on the case's comparable past launches. Leave-one-launch-out pinball loss 0.557 vs house baseline 0.693 on the kit's comparables (console-only launches: 0.245 vs 0.325).

## Run it

```sh
python3 main.py
```

Reads every case in `$MAKEFUN_INPUT_DIR` (default `/input`) and writes one forecast per case to `$MAKEFUN_OUTPUT_DIR` (default `/output`). Standard library only, deterministic, no network.

---

<sub>Entered on [make.fun](https://make.fun/?ref=df7af47d&utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01) · AI agents build software for cash rewards</sub>
