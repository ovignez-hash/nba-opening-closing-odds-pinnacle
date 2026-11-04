# NBA Opening & Closing Odds — free sample, 20 games

**Free sample: 20 of the 10,323 games of the full product** (as of 1 November 2026). Same file layout, same 284
columns: every row is copied byte for byte from the full CSV. Only the number of games differs.

`NBA_Opening_Closing_Odds_2018-2026_SAMPLE.csv` — 20 rows, 284 columns, UTF-8, comma-separated. 1,846 prices.

🏀 **[→ The full dataset on Gumroad](https://sportsdataolivier.gumroad.com/l/degjxu?utm_source=github&utm_medium=sample_readme&utm_campaign=nba_oc&utm_content=readme)**

## The 20 games

Two or three games per season, 2018-19 to 2026-27: 10 regular season · 2 play-in · 5 playoffs (3 NBA Finals) · 3 NBA Cup finals. 2 went to overtime. *Closing ML* and
*Opening ML* count the sources, out of 13, with a moneyline for that game.

| Date (ET) | Game | Stage | Final, away–home | Closing ML | Opening ML | Pinnacle team totals | Why it is here |
|---|---|---|---|---:|---:|---|---|
| 16 Oct 2018 | Philadelphia 76ers @ Boston Celtics | Regular Season | 87–105 | 2 | 2 | – | The first game of the file. Two sources: Pinnacle and Bet365. |
| 13 Jun 2019 | Toronto Raptors @ Golden State Warriors | Playoffs | 114–110 | 4 | 2 | – | NBA Finals, Game 6. The US books carry closing prices only, as everywhere before the July 2020 restart. |
| 1 Mar 2020 | Los Angeles Lakers @ New Orleans Pelicans | Regular Season | 122–114 | 6 | 2 | – | Ten days before the March 2020 pause: six sources, the US books with closing prices only. |
| 15 Aug 2020 | Memphis Grizzlies @ Portland Trail Blazers | Play-In | 122–126 | 8 | 6 | – | The only play-in of 2019-20, in the Orlando bubble (neutral site). From the restart, the US books carry opening prices. |
| 30 Jan 2021 | Los Angeles Lakers @ Boston Celtics | Regular Season | 96–95 | 8 | 7 | yes | The 72-game season, the first with Pinnacle's team totals. |
| 21 May 2021 | Memphis Grizzlies @ Golden State Warriors | Play-In | 117–112 OT | 8 | 7 | yes | Play-in, overtime. |
| 25 Dec 2021 | Brooklyn Nets @ Los Angeles Lakers | Regular Season | 122–115 | 8 | 6 | yes | Christmas: Bet365 opened its moneyline 116 days before tip-off, the US books 67 days before, Pinnacle the day before. |
| 18 Apr 2022 | Denver Nuggets @ Golden State Warriors | Playoffs | 106–126 | 8 | 7 | yes | Playoffs, first round. |
| 8 Feb 2023 | Philadelphia 76ers @ Boston Celtics | Regular Season | 99–106 | 8 | 7 | yes | Regular season. |
| 26 Apr 2023 | Miami Heat @ Milwaukee Bucks | Playoffs | 128–126 OT | 8 | 7 | yes | Playoffs, first round, overtime. |
| 15 Nov 2023 | Boston Celtics @ Philadelphia 76ers | Regular Season | 117–107 | 9 | 8 | yes | theScore arrives (November 2023). |
| 9 Dec 2023 | Indiana Pacers @ Los Angeles Lakers | NBA Cup Final | 109–123 | 9 | 8 | yes | The first NBA Cup final. |
| 17 Dec 2024 | Milwaukee Bucks @ Oklahoma City Thunder | NBA Cup Final | 97–81 | 8 | 8 | yes | NBA Cup final. |
| 15 Mar 2025 | New York Knicks @ Golden State Warriors | Regular Season | 94–97 | 10 | 8 | yes | Hard Rock arrives (14 March 2025). |
| 22 Jun 2025 | Indiana Pacers @ Oklahoma City Thunder | Playoffs | 91–103 | 10 | 2 | yes | NBA Finals, Game 7, with Pinnacle's team totals (image 3 of the Gumroad listing). |
| 7 Nov 2025 | Cleveland Cavaliers @ Washington Wizards | Regular Season | 148–115 | 9 | 7 | yes | The score corrected by the NBA after the game: 148-115. |
| 16 Dec 2025 | San Antonio Spurs @ New York Knicks | NBA Cup Final | 113–124 | 10 | 8 | yes | NBA Cup final. |
| 13 Jun 2026 | New York Knicks @ San Antonio Spurs | Playoffs | 94–90 | 13 | 2 | yes | NBA Finals, Game 5: all 13 sources at the close (image 4 of the Gumroad listing). |
| 28 Oct 2026 | Los Angeles Lakers @ Los Angeles Clippers | Regular Season | 103–87 | 13 | 13 | – | 13 sources open and close; 9 of 11 books opened the Clippers at +5.5, 10 of 11 closed them as favourites (image 7 of the Gumroad listing). |
| 1 Nov 2026 | Boston Celtics @ Orlando Magic | Regular Season | 108–97 | 13 | 13 | – | All 13 closing moneylines recorded at the same second, 29 seconds before tip-off (image 2 of the Gumroad listing). |

## Read before you look

- **Games 1 to 3 are from before the July 2020 restart:** the US books carry closing prices only.
- **In the NBA Finals, the US books carry closing prices, rarely opening ones.** From the 2020 bubble to the 2026 Finals, 3 of the 40 Finals games have an opening price from a US book; Bet365 has the opening price of all 40, Pinnacle of 34. The other playoff games are not affected: 530 of 550 have a US book's opening moneyline. The 2025 and 2026 Finals games of this sample show it; the 2019 one is from before the restart, when no US book has an opening price.
- **2026-27 has no team totals yet:** the last two games.
- **Kalshi and Polymarket start in December 2025 and January 2026:** they appear in the last three games.

## Quick start on this sample

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

Everything below is the README shipped with the full product, word for word: its figures describe the full file as
of 1 November 2026, and its Quick start reads the full CSV.

## README of the full product: NBA Opening & Closing Odds — 11 books and 2 prediction markets, 2018–2026

One row per game. 10,323 NBA games from 16 October 2018 to 1 November 2026: seasons 2018-19 through 2026-27, the 2026-27 season through 1 November. Regular season, play-in, playoffs and the three NBA Cup finals. No preseason, no All-Star games.

For every book and every market, the opening price and the closing price where the sources have them, each with the time it was recorded. Pinnacle adds the team totals of both teams from 2020-21.

| | |
|---|---|
| Games | 10,323 |
| Seasons | 2018-19 to 2026-27 |
| Books | Pinnacle · Bet365 · FanDuel · DraftKings · BetMGM · Caesars · BetRivers · BetOnline · theScore · Fanatics · Hard Rock |
| Prediction markets | Kalshi · Polymarket (moneyline only) |
| Markets | Moneyline · Spread · Total · Team totals (Pinnacle, from 2020-21) |
| Prices | 882,226 |
| Columns | 284 |
| File | `NBA_Opening_Closing_Odds_2018-2026.csv` (UTF-8, comma-separated) |

### Games

| Season | Regular season | Play-in | Playoffs | NBA Cup final | Total |
|---|---:|---:|---:|---:|---:|
| 2018/2019 | 1,230 | – | 82 | – | 1,312 |
| 2019/2020 | 1,059 | 1 | 83 | – | 1,143 |
| 2020/2021 | 1,080 | 6 | 85 | – | 1,171 |
| 2021/2022 | 1,230 | 6 | 87 | – | 1,323 |
| 2022/2023 | 1,230 | 6 | 84 | – | 1,320 |
| 2023/2024 | 1,230 | 6 | 82 | 1 | 1,319 |
| 2024/2025 | 1,230 | 6 | 84 | 1 | 1,321 |
| 2025/2026 | 1,230 | 6 | 85 | 1 | 1,322 |
| 2026/2027 | 92 | – | – | – | 92 |

2019/2020 includes the 88 seeding games played in the Orlando bubble from 30 July 2020; 2020/2021 was a 72-game season. 541 games went to overtime.

### Columns

**Game — 14 columns**

| Column | Content |
|---|---|
| `League` | NBA |
| `Game_ID` | `YYYYMMDD_AWAY_HOME`, date in US Eastern time |
| `Season` | `2018/2019` |
| `Stage` | `Regular Season`, `Play-In`, `Playoffs`, `NBA Cup Final` |
| `Kickoff_UTC` | scheduled tip-off, ISO 8601 (`2018-10-17T00:00:00Z`) |
| `Epoch` | the same instant in Unix seconds |
| `Home_Team`, `Away_Team` | full team names |
| `Home_Score`, `Away_Score` | final score, overtime included |
| `Winner` | `Home` or `Away` |
| `Total_Score` | home plus away points |
| `Margin` | absolute difference between the two scores, never negative |
| `Match_Ending` | `Regular Time` or `Overtime` |

**Odds — 22 columns per book**, opening first, then closing:

```
{Book}_ML_Home_Open        {Book}_ML_Home_Close
{Book}_ML_Away_Open        {Book}_ML_Away_Close
{Book}_ML_Open_Time        {Book}_ML_Close_Time
{Book}_Spread_Home_Line_Open   ... _Close
{Book}_Spread_Home_Open        ... _Close
{Book}_Spread_Away_Open        ... _Close
{Book}_Spread_Open_Time        ... _Close_Time
{Book}_Total_Line_Open         ... _Close
{Book}_Total_Over_Open         ... _Close
{Book}_Total_Under_Open        ... _Close
{Book}_Total_Open_Time         ... _Close_Time
```

Kalshi and Polymarket carry the moneyline columns only, 6 each. Hard Rock's columns start with `HardRock_`.

**Team totals — 16 more columns for Pinnacle**, one over/under per team, placed after Pinnacle's total columns (opening, then closing):

```
Pinnacle_Team_Total_Home_Line_Open    ... _Close
Pinnacle_Team_Total_Home_Over_Open    ... _Close
Pinnacle_Team_Total_Home_Under_Open   ... _Close
Pinnacle_Team_Total_Home_Open_Time    ... _Close_Time
```

The same four with `Away` for the away team.

#### How to read it

**Prices are American odds**, as integers: `-150`, and `130` for +130. Even money is written `100`.

**The spread line is the home team's handicap.** `-6.5` means the home team gives 6.5 points; the away team's line is the opposite.

**The total line is in points**, the same for over and under.

**A team total is the points of one team.** `Pinnacle_Team_Total_Home_Line_Close` at `112.5` is over or under 112.5 points for the home team.

**Kalshi and Polymarket are prediction markets.** Their prices are written as American odds. When the source gives no American price, which is the case for most of 2026-27, the price is the cost of buying each side (the ask), converted to American odds.

**One time per book, market and phase.** The `_Time` columns are ISO 8601 in UTC and give the moment the price was recorded. From the July 2020 restart, most closing prices of the US books are recorded at the same second for all of them, within a few minutes of tip-off. The others carry the time of the book's last recorded price before tip-off. The table counts, per season, the games where at least one moneyline, spread or total closing price of the book is stamped more than 15 minutes before the scheduled tip-off:

| Season | Pinnacle | Bet365 | FanDuel | DraftKings | BetMGM | Caesars | BetRivers | BetOnline | theScore | Fanatics | Hard Rock |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 2018/2019 | 1,260 | 310 | 753 | 154 | – | – | – | – | – | – | – |
| 2019/2020 | 920 | 80 | 973 | 838 | 131 | 269 | 966 | 3 | – | – | – |
| 2020/2021 | 14 | 36 | 243 | 34 | 144 | 357 | 1,026 | 5 | – | – | – |
| 2021/2022 | 1 | 82 | 18 | 34 | 115 | 134 | 930 | 20 | – | – | – |
| 2022/2023 | 9 | 117 | 43 | 37 | 49 | 35 | 813 | 13 | – | – | – |
| 2023/2024 | 17 | 18 | 19 | 17 | 52 | 22 | 671 | 5 | 30 | – | – |
| 2024/2025 | 10 | 16 | 13 | 7 | 27 | 36 | 727 | 3 | 16 | – | 209 |
| 2025/2026 | 330 | 78 | 4 | 3 | 11 | 4 | 1 | 7 | 5 | 260 | 3 |
| 2026/2027 | – | 78 | – | – | – | 1 | – | – | – | – | – |

Pinnacle's closing prices before the 2020 restart are its last recorded price: a median 5.4 hours before the scheduled tip-off in 2018-19 and 5.1 hours in 2019-20 before the pause. Some closing prices come from snapshots of the market: those of BetRivers, Fanatics and Hard Rock before 2026-27, those of the other US books before the July 2020 restart, and a minority of their later ones. Their time is the book's last price update seen in the snapshot, even when it is stamped at tip-off.

**The opening price is the first price recorded for the game.** For season openers, Christmas games, NBA Cup nights and other dates set long in advance, that can be weeks or months before tip-off.

**The closing price is the last pre-game price.** `Kickoff_UTC` is the scheduled tip-off; the ball is usually tipped a few minutes later and books take bets until then. Median closing time on the moneyline, against the scheduled tip-off: Pinnacle 9 minutes after (from the 2020 restart); FanDuel, DraftKings, BetMGM, Caesars, BetOnline, theScore, Fanatics, Hard Rock, Kalshi and Polymarket 1 minute after; Bet365 2 minutes before; BetRivers 16 minutes before. No closing price is older than 12 hours before the scheduled tip-off, and none is stamped more than 30 minutes after it. Pinnacle's closing moneyline is stamped more than 10 minutes after the scheduled tip-off in 1,246 games, 27 minutes at most; those prices sit at the level of the other books' closes and show no sign of in-play pricing.

**Closing prices were checked against the market at tip-off.** A closing price was compared with the median of the other books' closing prices recorded at tip-off on the same game, and left out when it was more than 0.05 away in no-vig implied probability on the moneyline, 2.5 points or more away on the spread, or 3 points or more away on the total. This works where the game has enough other books recorded at tip-off, which is the case for most games from the July 2020 restart. Before it, Bet365 is usually the only book recorded at tip-off: the other books are checked against it, while Bet365 itself, as a rule, is not.

### Coverage

Share of games with a closing moneyline, in %, rounded down (100 means every game):

| Season | Pinnacle | Bet365 | FanDuel | DraftKings | BetMGM | Caesars | BetRivers | BetOnline | theScore | Fanatics | Hard Rock | Kalshi | Polymarket |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 2018/2019 | 95 | 99 | 86 | 41 | – | – | – | – | – | – | – | – | – |
| 2019/2020 | 92 | 99 | 85 | 91 | 12 | 28 | 89 | 13 | – | – | – | – | – |
| 2020/2021 | 99 | 99 | 100 | 99 | 91 | 99 | 97 | 97 | – | – | – | – | – |
| 2021/2022 | 99 | 99 | 99 | 99 | 96 | 99 | 76 | 97 | – | – | – | – | – |
| 2022/2023 | 99 | 99 | 100 | 100 | 99 | 99 | 95 | 97 | – | – | – | – | – |
| 2023/2024 | 100 | 99 | 99 | 99 | 100 | 100 | 95 | 98 | 88 | – | – | – | – |
| 2024/2025 | 99 | 100 | 100 | 99 | 100 | 99 | 96 | 98 | 100 | – | 24 | – | – |
| 2025/2026 | 99 | 96 | 100 | 99 | 99 | 99 | 91 | 98 | 99 | 72 | 92 | 75 | 59 |
| 2026/2027 | 100 | 98 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 |

Share of games with an opening moneyline, in %, rounded down:

| Season | Pinnacle | Bet365 | FanDuel | DraftKings | BetMGM | Caesars | BetRivers | BetOnline | theScore | Fanatics | Hard Rock | Kalshi | Polymarket |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 2018/2019 | 99 | 99 | – | – | – | – | – | – | – | – | – | – | – |
| 2019/2020 | 96 | 99 | 12 | 11 | – | 11 | – | 11 | – | – | – | – | – |
| 2020/2021 | 98 | 98 | 91 | 81 | 80 | 82 | – | 80 | – | – | – | – | – |
| 2021/2022 | 99 | 99 | 92 | 88 | 90 | 72 | – | 76 | – | – | – | – | – |
| 2022/2023 | 99 | 98 | 93 | 92 | 89 | 87 | – | 79 | – | – | – | – | – |
| 2023/2024 | 99 | 99 | 95 | 95 | 89 | 89 | – | 80 | 82 | – | – | – | – |
| 2024/2025 | 99 | 99 | 96 | 96 | 92 | 90 | – | 79 | 94 | – | – | – | – |
| 2025/2026 | 99 | 99 | 96 | 96 | 90 | 93 | – | 81 | 90 | – | – | – | – |
| 2026/2027 | 100 | 100 | 100 | 88 | 94 | 97 | 100 | 100 | 100 | 66 | 100 | 94 | 95 |

Share of games with a Pinnacle team total, in %, rounded down:

| Season | Home, opening | Away, opening | Home, closing | Away, closing |
|---|---:|---:|---:|---:|
| 2020/2021 | 94 | 94 | 94 | 94 |
| 2021/2022 | 100 | 100 | 99 | 99 |
| 2022/2023 | 99 | 99 | 99 | 99 |
| 2023/2024 | 99 | 99 | 98 | 98 |
| 2024/2025 | 99 | 99 | 98 | 98 |
| 2025/2026 | 96 | 96 | 83 | 86 |

### Said plainly

- **Before the March 2020 pause, the US books carry closing prices only:** the last pre-game price of each book in each market, with its time. FanDuel starts on 8 November 2018 and DraftKings on 30 January 2019. Median age of that closing price at the scheduled tip-off: FanDuel 19 minutes in 2018-19; in 2019-20 before the pause, Caesars 50 minutes, DraftKings 70 minutes, BetRivers 72 minutes and FanDuel 5 hours. In the 2020 bubble, BetMGM's closing prices are taken a median 92 minutes before tip-off. The time columns show it game by game.
- **Opening prices of the US books start with the July 2020 restart in the bubble**, for FanDuel, DraftKings, Caesars and BetOnline; BetMGM from December 2020; theScore from November 2023. BetRivers has no opening price before 2026-27. Kalshi and Polymarket carry closing prices from December 2025 and January 2026, opening prices in 2026-27 only.
- **Fanatics and Hard Rock carry closing prices only before 2026-27.** Fanatics starts on 21 October 2025, with gaps until January 2026 (December 2025 is almost empty); Hard Rock starts on 14 March 2025. Both have opening prices in 2026-27, Fanatics for 66% of the games.
- **BetOnline's opening moneyline is recorded late:** a median 2.7 hours before tip-off, against 22 hours for its spread and total and about a day for the other books.
- **Pinnacle has no spread before the July 2020 restart**, moneyline and total only.
- **Team totals come from Pinnacle only**, from 31 December 2020 to the 2026 Finals; no other book carries them, and 2026-27 has none yet. From February 2026, many of Pinnacle's last team-total prices were recorded more than 12 hours before tip-off and were left out: in 2025-26, the home team has a closing team total in 83% of the games, the away team in 86%.
- **When the opening record is the closing record itself (same moment), it appears once:** as the closing price, or as the opening price when it was recorded more than 12 hours before tip-off, too early to be a closing price. An opening price equal to the closing price at a different time is kept: the book did not move. No opening price is stamped after the scheduled tip-off. A book's opening and closing prices in a market always come from the same source: when a closing price was replaced by another source's, the first source's opening price was left out with it. 1,182 markets have an opening price and no closing price.
- **Closing prices that lagged the market at tip-off were not used** (see How to read it): 2,172 of them. Most were timed at the book's last update, above all in 2019-20, 2024-25 and 2025-26, or were Pinnacle closes from 2018-2020. For 209, the book's other source agreed with the market and was used instead.
- **Prices that contradict the market were removed rather than kept**: 88 Bet365 and Pinnacle prices taken from an update that came with the two teams swapped against the update next to it, when the other books confirm the swap; 4 opening spreads on the other side of the market's moneyline favourite; 25 opening prices on the wrong side of the whole market's close; 2 where one book's moneyline and spread named different favourites; 70 alternate lines (a line at least 1.5 points away from the other books with unbalanced prices, or at least 2.5 points away with prices leaning to make up for it); 139 prices or lines far from the other books on the same game (more than 0.15 in no-vig implied probability on the moneyline, 4 points on the spread, 6 points on the total for a closing price); and 45 pairs of team totals that did not match the total and spread: 1 against the same book's (6 points), 44 against the market at tip-off (3 points on their sum, 2.5 on their difference). Prices that cannot exist were not used either: moneylines with less than 1.5% margin (the two sides were not taken at the same moment) or more than 25%, closing moneylines with more than 10% margin, spread and total prices beyond ±250 or adding up to less than 100% or more than 115%, prediction-market prices whose two sides do not add up, and lines out of range.
- **The 2020 bubble was played on a neutral site.** Home and away follow the NBA's designation. For 3 bubble games, part of the prices came with the two teams swapped; those prices were left out.
- **Scores were cross-checked game by game.** One was corrected by the NBA after the game: Cleveland at Washington, 7 November 2025, is 148-115, a Washington free throw first recorded as missed.
- **The 2026-27 season stops on 1 November 2026**, 92 games.

### Quick start

```python
import pandas as pd

df = pd.read_csv("NBA_Opening_Closing_Odds_2018-2026.csv", low_memory=False)

# implied probability of the home team at Pinnacle's close
def prob(us):
    return -us / (-us + 100) if us < 0 else 100 / (us + 100)

p = df.Pinnacle_ML_Home_Close.dropna().map(prob)

# line movement: DraftKings spread, open to close
move = df.DraftKings_Spread_Home_Line_Close - df.DraftKings_Spread_Home_Line_Open

# Pinnacle's two team totals against its game total, at the close
gap = (df.Pinnacle_Team_Total_Home_Line_Close + df.Pinnacle_Team_Total_Away_Line_Close
       - df.Pinnacle_Total_Line_Close)
```

*Olivier Sports Data — From Chicken Area 🐔*
