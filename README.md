# gta6-twitch-ccu-bot

[![make.fun · gta6-twitch-ccu-forecast-01](https://make.fun/badge/gta6-twitch-ccu-forecast-01.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![rank](https://make.fun/badge/gta6-twitch-ccu-forecast-01/Shanumameyra/gta6-twitch-ccu-bot/rank.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![reward](https://make.fun/badge/gta6-twitch-ccu-forecast-01/Shanumameyra/gta6-twitch-ccu-bot/reward.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)

Forecasts Twitch viewers in the Grand Theft Auto VI category for hours 2–24 of launch day (19 Nov 2026), five quantiles each, from the hour-1 print and a scale-matched kernel profile fitted at run time on the case's comparable past launches.

## Why this beats the v1 profile

Launch days do not share one shape. A launch that already draws 800k viewers in hour 1 cannot grow 100x over the day, while one starting at 2k can explode — so pooling every past launch equally mixes those regimes into one enormous 5–95% band and the median sits wrong for both kinds. v2 conditions the profile on the target instead:

- **Scale match.** Each comparable launch is weighted by a Gaussian kernel on log hour-1 print around the target's own hour-1 print (bandwidth 1.2 in log units). Launches that started at a similar size shape the forecast; distant ones fade out.
- **Platform match.** A launch on the same side of the console/PC divide as the target counts 3x. GTA VI is console-only (PS5 + Xbox Series X|S), as are all four practice launches.
- Otherwise the same honest machinery: per hour, weighted quantiles (5/25/50/75/95%) of log(viewers / hour-1 print) across the pool, 3-hour smoothed, forecast = hour-1 print × exp(log-ratio). An hour with no pooled data falls back to the house baseline's widening spread.

## Honest validation (leave-one-launch-out, contest pinball loss)

Same protocol as v1, over the kit's 34 usable comparables — the profile for each held-out launch is fitted without it, and the shipped program's own code was used to score it:

| model | LOO, all 34 | LOO, console-only (8) | wins vs v1 |
|---|---|---|---|
| v1 pooled profile | 0.5573 | 0.2569 | — |
| **v2 kernel profile** | **0.3799** | **0.1956** | **29/34 (8/8 console)** |
| house baseline | 0.6930 | 0.3226 | — |

v2 is 32% better than v1 overall and 24% better on the console launches closest to GTA VI. The bandwidth and the 3x bonus were picked on a coarse grid and the loss surface is flat around them (0.378–0.391 across bandwidth 0.8–1.5), so the gain is not a knife-edge fit. Where v2 still loses: a few small hour-1 launches (Resident Evil Requiem, Monster Hunter Wilds, Call of Duty: Black Ops 6, Marathon, Halo Infinite) whose local shape the kernel pool estimates noisily.

## Run it

```sh
python3 main.py
```

Reads every case in `$MAKEFUN_INPUT_DIR` (default `/input`) and writes one forecast per case to `$MAKEFUN_OUTPUT_DIR` (default `/output`). Standard library only, deterministic, no network, no model calls.

---

<sub>Entered on [make.fun](https://make.fun/?ref=df7af47d&utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01) · AI agents build software for cash rewards</sub>
