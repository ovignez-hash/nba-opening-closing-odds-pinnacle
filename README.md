# 🏀 NBA Opening & Closing Odds — 9 US Books + Pinnacle (2018–2026)

**20 games — every season from 2018-19, every stage: regular season, play-in, playoffs, NBA Finals and NBA Cup finals**

Most NBA odds archives give you one book, or one closing number per game.

The full dataset puts **up to 13 sources side by side on each game**: FanDuel, DraftKings, BetMGM, Caesars, BetRivers,
Fanatics, Hard Rock, theScore and BetOnline, next to Pinnacle, Bet365, Kalshi and Polymarket. Moneyline, spread and
total, **the opening and the closing price, each with the time it was recorded**, plus Pinnacle's team totals for
both teams.

→ **[Get the full archive](https://sportsdataolivier.gumroad.com/l/degjxu?utm_source=github&utm_medium=readme&utm_campaign=nba_oc&utm_content=hero)** — 10,323 games, October 2018 to 1 November 2026

This sample is cut from the full file: the same 284 columns, the rows copied byte for byte, at 0.2% scale.

---

## One game, every source

Celtics at Magic, 1 November 2026, moneyline. All 13 closing prices were recorded at the same second, 29 seconds
before the scheduled tip-off, and every source closed the Celtics shorter than it opened them.

| Source | Open, Magic / Celtics | Close, Magic / Celtics |
|---|---|---|
| Pinnacle | +224 / -265 | +232 / -267 |
| Bet365 | +215 / -265 | +240 / -300 |
| FanDuel | +205 / -250 | +245 / -300 |
| DraftKings | +210 / -263 | +230 / -286 |
| BetMGM | +220 / -275 | +230 / -295 |
| Caesars | +210 / -260 | +222 / -278 |
| BetRivers | +200 / -265 | +240 / -315 |
| BetOnline | +207 / -250 | +230 / -280 |
| theScore | +215 / -260 | +230 / -280 |
| Fanatics | +210 / -260 | +230 / -285 |
| Hard Rock | +210 / -260 | +225 / -275 |
| Kalshi | +186 / -203 | +245 / -257 |
| Polymarket | +194 / -203 | +233 / -245 |

---

## What's in this sample

| | |
|---|---|
| Games | 20 — two or three per season, 2018-19 to 2026-27 |
| Stages | 10 regular season · 2 play-in · 5 playoffs (3 NBA Finals) · 3 NBA Cup finals |
| Overtime | 2 games |
| Prices | 1,846 |
| Sources | 13 — 9 US books, Pinnacle, Bet365, Kalshi, Polymarket |
| Columns | 284 |
| File | `NBA_Opening_Closing_Odds_2018-2026_SAMPLE.csv`, plus the README of the full product |

| Date (ET) | Game | Stage | Final, away–home | Sources, closing / opening ML |
|---|---|---|---|---:|
| 16 Oct 2018 | 76ers @ Celtics | Regular Season | 87–105 | 2 / 2 |
| 13 Jun 2019 | Raptors @ Warriors | Playoffs | 114–110 | 4 / 2 |
| 1 Mar 2020 | Lakers @ Pelicans | Regular Season | 122–114 | 6 / 2 |
| 15 Aug 2020 | Grizzlies @ Trail Blazers | Play-In | 122–126 | 8 / 6 |
| 30 Jan 2021 | Lakers @ Celtics | Regular Season | 96–95 | 8 / 7 |
| 21 May 2021 | Grizzlies @ Warriors | Play-In | 117–112 OT | 8 / 7 |
| 25 Dec 2021 | Nets @ Lakers | Regular Season | 122–115 | 8 / 6 |
| 18 Apr 2022 | Nuggets @ Warriors | Playoffs | 106–126 | 8 / 7 |
| 8 Feb 2023 | 76ers @ Celtics | Regular Season | 99–106 | 8 / 7 |
| 26 Apr 2023 | Heat @ Bucks | Playoffs | 128–126 OT | 8 / 7 |
| 15 Nov 2023 | Celtics @ 76ers | Regular Season | 117–107 | 9 / 8 |
| 9 Dec 2023 | Pacers @ Lakers | NBA Cup Final | 109–123 | 9 / 8 |
| 17 Dec 2024 | Bucks @ Thunder | NBA Cup Final | 97–81 | 8 / 8 |
| 15 Mar 2025 | Knicks @ Warriors | Regular Season | 94–97 | 10 / 8 |
| 22 Jun 2025 | Pacers @ Thunder | Playoffs | 91–103 | 10 / 2 |
| 7 Nov 2025 | Cavaliers @ Wizards | Regular Season | 148–115 | 9 / 7 |
| 16 Dec 2025 | Spurs @ Knicks | NBA Cup Final | 113–124 | 10 / 8 |
| 13 Jun 2026 | Knicks @ Spurs | Playoffs | 94–90 | 13 / 2 |
| 28 Oct 2026 | Lakers @ Clippers | Regular Season | 103–87 | 13 / 13 |
| 1 Nov 2026 | Celtics @ Magic | Regular Season | 108–97 | 13 / 13 |

*Sources* counts, out of 13, the sources with a closing / opening moneyline for that game. Why each game is
here, game by game: `sample/README.md`.

---

## In this repository

| File | Content |
|---|---|
| `sample/NBA_Opening_Closing_Odds_2018-2026_SAMPLE.csv` | the 20 games, 284 columns |
| `sample/README.md` | why each game is here, then the README of the full product |
| `NBA_Verify_Before_You_Buy.ipynb` | the figures of the listing and of its README recomputed from the full file, results shown |

---

## Columns

| Block | Columns | Content |
|---|---:|---|
| Game | 14 | `League`, `Game_ID` (`YYYYMMDD_AWAY_HOME`, US Eastern date), `Season`, `Stage`, `Kickoff_UTC`, `Epoch`, teams, final score, `Winner`, `Total_Score`, `Margin`, `Match_Ending` |
| Each of the 11 books | 22 | moneyline, spread and total, opening then closing, with the time of each |
| Pinnacle team totals | 16 | line, over and under for both teams, opening and closing, with their times |
| Kalshi, Polymarket | 6 each | moneyline only |

`{Book}_ML_Home_Open` · `{Book}_ML_Home_Close` · `{Book}_ML_Close_Time` · `{Book}_Spread_Home_Line_Close` · `{Book}_Total_Line_Close` · `Pinnacle_Team_Total_Away_Line_Close` — Hard Rock's columns start with `HardRock_`.

### How to read it

**Prices are American odds, as integers:** `-150`, and `130` for +130. **The spread line is the home team's handicap:** `-6.5` means the home team gives 6.5 points. **Times are UTC**, ISO 8601 with the T and the Z. **The opening price is the first price recorded** for the game, **the closing price the last pre-game price**; each one carries its own time, so you can see how close to tip-off it was taken.

```python
import pandas as pd

df = pd.read_csv("NBA_Opening_Closing_Odds_2018-2026_SAMPLE.csv")

def prob(us):                          # American odds -> implied probability
    return -us / (-us + 100) if us < 0 else 100 / (us + 100)

# Pinnacle's closing price on the home team
df["pinnacle_home_close"] = df["Pinnacle_ML_Home_Close"].map(prob)

# how far each book moved the spread, open to close
for b in ["Pinnacle", "FanDuel", "DraftKings", "BetMGM", "Caesars"]:
    df[b + "_spread_move"] = df[b + "_Spread_Home_Line_Close"] - df[b + "_Spread_Home_Line_Open"]

# how close to tip-off each closing moneyline was recorded, in minutes
tip = pd.to_datetime(df["Kickoff_UTC"])
df["fanduel_close_min"] = (pd.to_datetime(df["FanDuel_ML_Close_Time"]) - tip).dt.total_seconds() / 60
```

---

## Said plainly

- **Before the July 2020 restart, the US books carry closing prices only**, and they can be old: the time columns show it game by game. FanDuel starts on 8 November 2018, DraftKings on 30 January 2019.
- **Opening prices of the US books start with the restart** (FanDuel, DraftKings, Caesars, BetOnline), BetMGM in December 2020, theScore in November 2023. BetRivers, Fanatics and Hard Rock have opening prices in 2026-27 only.
- **Pinnacle has no spread before the restart.** Its closing prices before then are its last recorded price, hours before tip-off.
- **Team totals come from Pinnacle only**, from 31 December 2020 to the 2026 Finals; none yet in 2026-27.
- **Kalshi and Polymarket: moneyline only**, closing prices from December 2025 and January 2026, opening prices in 2026-27 only. Most 2026-27 prices are the ask, converted to American odds.
- **In the NBA Finals, the US books carry closing prices, rarely opening ones.** From the 2020 bubble to the 2026 Finals, 3 of the 40 Finals games have an opening price from a US book; Bet365 has the opening price of all 40, Pinnacle of 34. The other playoff games are not affected: 530 of 550 have a US book's opening moneyline.
- **Coverage has gaps**, season by season in the README: Hard Rock covers 24% of 2024-25 (from 14 March 2025), Fanatics 72% of 2025-26, BetRivers 76% of 2021-22.
- **No preseason, no All-Star games, no props, no quarters or halves, no live odds.** One opening and one closing price per book and market, not every move in between.

---

## Verify before you buy

The figures of the listing and of its README — games, prices, coverage season by season, the closing-time limits
and median ages, the team totals, the games on the listing's images — recomputed from the full file and printed
PASS or FAIL:
[on Kaggle](https://www.kaggle.com/code/oliviersportsdata/nba-opening-closing-odds-verify-before-you-buy) · [on GitHub](https://github.com/ovignez-hash/nba-opening-closing-odds-pinnacle/blob/main/NBA_Verify_Before_You_Buy.ipynb) (results shown).

---

## The full dataset

| | Sample | Full |
|---|---|---|
| Games | 20 | 10,323 |
| Seasons | 2018-19 to 2026-27 | 2018-19 to 2026-27, through 1 Nov 2026 |
| Prices | 1,846 | 882,226 |
| Columns | 284 | 284 |
| Files | 1 CSV + README | 1 CSV + README |

Once a year, after the Finals, the file adds the completed season. The games after 1 November 2026 come with the
[NBA monthly updates](https://sportsdataolivier.gumroad.com/l/uftmyi?utm_source=github&utm_medium=readme&utm_campaign=nba_oc&utm_content=monthly): each month's games, same 284 columns, ready to append.

→ **[Get the full archive](https://sportsdataolivier.gumroad.com/l/degjxu?utm_source=github&utm_medium=readme&utm_campaign=nba_oc&utm_content=footer)**

---

## Licence

Sample: free to explore and evaluate.
Full product: single commercial user. Research, modelling and internal use permitted.
Redistribution and resale of the files are not.

A question before buying: contact@oliviersportsdata.com

---

*Olivier Sports Data — From Chicken Area 🐔*
