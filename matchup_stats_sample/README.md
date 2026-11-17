# NBA Matchup & Stats — free sample, the same 20 games

The four tables of **NBA Matchup & Stats** for the 20 games of this repository's odds sample. Same files and same columns as the full product: only the number of games differs.

| File | One row per | Rows |
|---|---|---:|
| `NBA_Matchup_Stats_Games_2008-2026_SAMPLE.csv` | game | 20 |
| `NBA_Matchup_Stats_Team_Box_Scores_2008-2026_SAMPLE.csv` | team and game | 40 |
| `NBA_Matchup_Stats_Player_Box_Scores_2008-2026_SAMPLE.csv` | player and game | 421 |
| `NBA_Matchup_Stats_Inactive_Players_2008-2026_SAMPLE.csv` | inactive player and game | 129 |

Every table joins the odds sample on `Game_ID`, the same key as in *NBA Opening & Closing Odds — 11 books and 2 prediction markets, 2018–2026*:

```python
import pandas as pd

odds = pd.read_csv("../sample/NBA_Opening_Closing_Odds_2018-2026_SAMPLE.csv", low_memory=False)
games = pd.read_csv("NBA_Matchup_Stats_Games_2008-2026_SAMPLE.csv", dtype={"NBA_Game_ID": str})

stats_cols = ["Game_ID"] + [c for c in games.columns if c not in odds.columns]
df = odds.merge(games[stats_cols], on="Game_ID")   # 20 games, odds and game sheet side by side
```

The full product: 23,329 games from 2008-09 to 16 November 2026, 491,155 player rows, 139,928 inactive-player rows.

→ **[Get NBA Matchup & Stats](https://sportsdataolivier.gumroad.com/l/nnadkm?utm_source=github&utm_medium=readme&utm_campaign=nba_oc&utm_content=matchup_sample)** · also on [Whop](https://whop.com/oliviersportsdata/nba-matchup-stats-game-sheets-box-scores-2008-2026/?utm_source=github&utm_medium=readme&utm_campaign=nba_oc&utm_content=matchup_sample_whop)

Sample: free to explore and evaluate. Full product: single commercial user; redistribution and resale of the files, or of the raw data in another format, are not permitted. A question: contact@oliviersportsdata.com

---

*The README of the full product follows.*

## NBA Matchup & Stats — game sheets, team and player box scores, 2008–2026

Every NBA game from the 2008-09 season to 16 November 2026: the game sheet (quarter scores, arena, attendance, officials), both teams' box scores with the game charts (points in the paint, second-chance and fast-break points, bench points, biggest lead), every player's box score, and the players each team declared inactive. Four tables, one key.

Built to sit next to the NBA Opening & Closing Odds files: `Game_ID` is the same key, so every game of the odds files finds its row here, with no name matching. Statistics only: there are no odds in this file.

| | |
|---|---|
| Games | 23,329 |
| Seasons | 2008-09 to 2026-27 (2026-27 through 16 November 2026) |
| Team box scores | 46,658 rows |
| Player box scores | 491,155 rows, 2,092 players |
| Inactive players | 139,928 rows |
| Files | 4 CSV files, UTF-8, comma-separated |
| Source | the NBA's official statistics |

### Games

| Season | Regular season | Play-in | Playoffs | NBA Cup final | Total |
|---|---:|---:|---:|---:|---:|
| 2008/2009 | 1,230 | – | 85 | – | 1,315 |
| 2009/2010 | 1,230 | – | 82 | – | 1,312 |
| 2010/2011 | 1,230 | – | 81 | – | 1,311 |
| 2011/2012 | 990 | – | 84 | – | 1,074 |
| 2012/2013 | 1,229 | – | 85 | – | 1,314 |
| 2013/2014 | 1,230 | – | 89 | – | 1,319 |
| 2014/2015 | 1,230 | – | 81 | – | 1,311 |
| 2015/2016 | 1,230 | – | 86 | – | 1,316 |
| 2016/2017 | 1,230 | – | 79 | – | 1,309 |
| 2017/2018 | 1,230 | – | 82 | – | 1,312 |
| 2018/2019 | 1,230 | – | 82 | – | 1,312 |
| 2019/2020 | 1,059 | 1 | 83 | – | 1,143 |
| 2020/2021 | 1,080 | 6 | 85 | – | 1,171 |
| 2021/2022 | 1,230 | 6 | 87 | – | 1,323 |
| 2022/2023 | 1,230 | 6 | 84 | – | 1,320 |
| 2023/2024 | 1,230 | 6 | 82 | 1 | 1,319 |
| 2024/2025 | 1,230 | 6 | 84 | 1 | 1,321 |
| 2025/2026 | 1,230 | 6 | 85 | 1 | 1,322 |
| 2026/2027 | 205 | – | – | – | 205 |

2011/2012 is the 66-game lockout season. 2012/2013 has 1,229 regular-season games: Indiana at Boston was cancelled after the Boston Marathon bombing and is not in the file. 2019/2020 includes the 88 seeding games and the play-in game played in the Orlando bubble from 30 July 2020; 2020/2021 was a 72-game season. NBA Cup games are flagged in `NBA_Cup_Game` (67 per season from 2023/2024, 28 so far in 2026/2027): the group-stage and knockout games count in the regular season, the final does not. 1,330 games went to overtime, 5 of them to a fourth overtime.

### Four tables, one key

| File | One row per | Rows | Columns |
|---|---|---:|---:|
| `NBA_Matchup_Stats_Games_2008-2026.csv` | game | 23,329 | 51 |
| `NBA_Matchup_Stats_Team_Box_Scores_2008-2026.csv` | team and game | 46,658 | 41 |
| `NBA_Matchup_Stats_Player_Box_Scores_2008-2026.csv` | player and game | 491,155 | 30 |
| `NBA_Matchup_Stats_Inactive_Players_2008-2026.csv` | inactive player and game | 139,928 | 10 |

Every table carries `Game_ID`, the key shared with the odds files, and `NBA_Game_ID`, the NBA's own game number.

### Joining an odds file

`Game_ID` is `YYYYMMDD_AWAY_HOME`, date in US Eastern time, team codes of the time: the same key as in *NBA Opening & Closing Odds — Pinnacle and 7 international books, 2008–2026* and *NBA Opening & Closing Odds — 11 books and 2 prediction markets, 2018–2026*. Every game of both odds files is found here, with the same stage and the same overtime status. This file runs a little further: the odds files stop at the end of their own update.

```python
import pandas as pd

games = pd.read_csv("NBA_Matchup_Stats_Games_2008-2026.csv", dtype={"NBA_Game_ID": str}, low_memory=False)
odds = pd.read_csv("NBA_World_Opening_Closing_Odds_2008-2026.csv", low_memory=False)

stats_cols = ["Game_ID"] + [c for c in games.columns if c not in odds.columns]
df = odds.merge(games[stats_cols], on="Game_ID", how="left")
```

### Columns

**Games — 51 columns**

| Column | Content |
|---|---|
| `League` | NBA |
| `Game_ID` | `YYYYMMDD_AWAY_HOME`, date in US Eastern time, team codes of the time |
| `NBA_Game_ID` | the NBA's game number, 10 digits with leading zeros (`0020800001`): read it as text |
| `Season` | `2008/2009` |
| `Stage` | `Regular Season`, `Play-In`, `Playoffs`, `NBA Cup Final` |
| `NBA_Cup_Game` | 1 for every NBA Cup game (group stage, knockout rounds, final), from 2023/2024 |
| `Date_ET` | game date, US Eastern time |
| `Kickoff_UTC` | scheduled tip-off, ISO 8601 (`2008-10-29T00:00:00Z`) |
| `Epoch` | the same instant in Unix seconds |
| `Home_Team`, `Away_Team` | full team names, as the team was named that season (the names of the odds files) |
| `Home_Code`, `Away_Code` | team codes of the time |
| `Home_Score`, `Away_Score` | final score, overtime included |
| `Winner` | `Home` or `Away` |
| `Total_Score` | home plus away points |
| `Margin` | absolute difference between the two scores |
| `Match_Ending` | `Regular Time` or `Overtime` |
| `Overtimes` | number of overtimes, 0 to 4 |
| `Home_Q1` … `Home_Q4`, `Home_OT1` … `Home_OT4` | home points in each quarter and overtime; overtime columns are empty when not played |
| `Away_Q1` … `Away_Q4`, `Away_OT1` … `Away_OT4` | the same for the away team |
| `Neutral_Site` | 1 when the NBA lists the game as played on neutral ground (from 2024/2025, see below) |
| `Arena`, `Arena_City`, `Arena_State`, `Arena_Country` | where the game was played |
| `Attendance` | spectators; 0 means the game was played without fans |
| `Sellout` | 1 when the arena was sold out |
| `Duration_Min` | game duration in minutes |
| `Lead_Changes`, `Times_Tied` | lead changes and ties during the game |
| `Official_1` … `Official_5` | the officials, in the order the NBA lists them |

Team names follow the season: New Jersey Nets (`NJN`) until 2011-12, then Brooklyn Nets (`BKN`); New Orleans Hornets (`NOH`) until 2012-13, then New Orleans Pelicans (`NOP`); Charlotte Bobcats until 2013-14, then Charlotte Hornets (`CHA` for both).

**Team box scores — 41 columns, two rows per game**

| Column | Content |
|---|---|
| `Game_ID`, `NBA_Game_ID`, `Season`, `Stage`, `Date_ET` | as in the games table |
| `Side` | `Home` or `Away` |
| `Team_Code`, `Team`, `Opponent_Code`, `Opponent` | the team and its opponent |
| `Result` | `W` or `L` |
| `Points`, `Opponent_Points` | final score, overtime included |
| `Minutes` | team minutes: 240, plus 25 per overtime |
| `FGM`, `FGA`, `FG_Pct` | field goals made, attempted, and the ratio (`0.446`) |
| `FG3M`, `FG3A`, `FG3_Pct` | three-pointers |
| `FTM`, `FTA`, `FT_Pct` | free throws; the ratio is empty when no free throw was attempted |
| `OREB`, `DREB`, `REB` | offensive, defensive and total rebounds of the players |
| `AST`, `STL`, `BLK`, `PF` | assists, steals, blocks, personal fouls |
| `TOV` | all turnovers: the players' plus the team's (`Team_Turnovers`) |
| `Plus_Minus` | point difference |
| `Points_In_Paint`, `Second_Chance_Points`, `Fast_Break_Points` | points by type |
| `Points_Off_Turnovers` | points scored after the opponent's turnovers |
| `Bench_Points` | points scored by the players who did not start |
| `Biggest_Lead`, `Biggest_Scoring_Run` | largest lead and largest unanswered run, in points |
| `Team_Turnovers` | turnovers credited to the team rather than to a player (shot clock, 8 seconds…) |
| `Team_Rebounds` | rebounds credited to the team rather than to a player |

**Player box scores — 30 columns**

| Column | Content |
|---|---|
| `Game_ID`, `NBA_Game_ID`, `Season`, `Stage`, `Date_ET`, `Side` | as in the team table |
| `Team_Code`, `Opponent_Code` | the player's team and its opponent |
| `Player_ID` | the NBA's player number, the same across seasons and teams |
| `Player` | name |
| `Points`, `Minutes` | points scored; minutes played, in whole minutes |
| `FGM` … `PF`, `TOV`, `Plus_Minus` | the same statistics as in the team table, for the player |

One row per player who took the floor. Players who were available but did not play have no row; players declared inactive are in their own table.

**Inactive players — 10 columns**

| Column | Content |
|---|---|
| `Game_ID`, `NBA_Game_ID`, `Season`, `Stage`, `Date_ET`, `Side`, `Team_Code` | the game and the team |
| `Player_ID`, `Player`, `Jersey` | the player declared inactive |

The list each team declared inactive for the game, as published by the NBA: 3.0 players per team and game on average.

### Checks run on every game

- Each team's score is the sum of its quarters and overtimes, and the sum of its players' points.
- Each team total (field goals, three-pointers, free throws, rebounds, assists, steals, blocks, fouls) is the sum of its players' lines; players' turnovers plus team turnovers make `TOV`.
- Team minutes are 240 plus 25 per overtime.
- No duplicate game, team line, player line or inactive line, and no inactive player has a line in the box score of the same game.
- Every game of the two NBA odds files is found, with the same stage and the same overtime status.

### Said plainly

- **`Neutral_Site` comes from the NBA and only exists from 2024/2025**: 13 games (6 in Las Vegas, 3 in Mexico City, 2 in Paris, 1 in Berlin, 1 in London). Earlier games played away from the home team's arena keep the designated home team and `Neutral_Site` 0: 24 games abroad (12 in Mexico City, 9 in London, 3 in Paris), the 3 NBA Cup semi-finals and final of 2023/2024 in Las Vegas, and the 172 games of the 2020 Orlando bubble. `Arena_City` and `Arena_Country` identify them.
- **Mexico City:** for 11 games from 2014 to 2022, the NBA lists the city as "Mexico City, Mexico" in the United States. They read Mexico City, `MX` here.
- **Scores come from the NBA's season logs.** For 4 games, the score printed on the NBA's game sheet differs by one or two points, while its quarter scores and the players' points agree with the log: New Orleans at Washington (10 January 2010), Memphis at Dallas (29 October 2010), LA Clippers at Indiana (20 March 2012), Phoenix at Houston (28 January 2018).
- **3 game sheets of 19 November 2025** (Washington at Minnesota, Denver at New Orleans, Sacramento at Oklahoma City) are empty on the NBA's game summary. They come from the NBA's live box score of the same game, checked the same way.
- **`Points_Off_Turnovers` is 0 for both teams in 42 games of 2008/2009**: not tracked for those games.
- **`Duration_Min` is empty for 40 games**: not published (0:00) or not credible (25 minutes, 4 h 44, 71 h 49).
- **`Attendance` is 0 for the 172 games of the Orlando bubble** (30 July to 11 October 2020) **and 614 games of 2020/2021** played without fans. It is empty for 21 other games the NBA lists at 0 (not recorded).
- **One team line was corrected:** Denver at New Orleans, 14 November 2026, shows 168 team minutes at the NBA for a game without overtime; it reads 240 here. The rest of the line agrees with its players.
- **Officials:** 3 in most games, 4 listed in 456 games (mostly playoffs and play-in), 4 games with only 2 listed, 1 with 5.
- **96 games have no inactive list at the NBA:** 49 playoff games (47 of them from 2022/2023 to 2025/2026) and 47 regular-season games (36 of them in 2026/2027 so far, 10 in 2011/2012).
- **2,373 player rows show 0 minutes:** players who were on the floor for only a few seconds (minutes are whole numbers).
- **`Kickoff_UTC` is the NBA's scheduled tip-off.** It can differ by a few minutes from the time in an odds file: join on `Game_ID`, not on the time.
- **Read `NBA_Game_ID` and `Jersey` as text.** Jersey "00" and jersey "0" are two different numbers; a spreadsheet turns "00" into 0.
- **The 2026/2027 season stops on 16 November 2026**, 205 games. Later games come with the monthly update.

### Quick start

```python
import pandas as pd

games = pd.read_csv("NBA_Matchup_Stats_Games_2008-2026.csv", dtype={"NBA_Game_ID": str}, low_memory=False)
teams = pd.read_csv("NBA_Matchup_Stats_Team_Box_Scores_2008-2026.csv", dtype={"NBA_Game_ID": str})
players = pd.read_csv("NBA_Matchup_Stats_Player_Box_Scores_2008-2026.csv", dtype={"NBA_Game_ID": str})
inactive = pd.read_csv("NBA_Matchup_Stats_Inactive_Players_2008-2026.csv", dtype={"NBA_Game_ID": str, "Jersey": str})

# first-half points of each team
games["Home_H1"] = games.Home_Q1 + games.Home_Q2
games["Away_H1"] = games.Away_Q1 + games.Away_Q2

# inactive players per team and game
out = inactive.groupby(["Game_ID", "Team_Code"]).size().rename("Inactive_Count")

# a player's last 10 games before a given date
lebron = players[players.Player == "LeBron James"].sort_values("Date_ET")
last10 = lebron[lebron.Date_ET < "2026-11-01"].tail(10)
```

### Licence

Single commercial user. Use the data as you wish, including the models, predictions and products you sell. Redistribution and resale of the files, or of the raw data in another format, are not permitted.

A question: contact@oliviersportsdata.com

*Olivier Sports Data — From Chicken Area 🐔*
