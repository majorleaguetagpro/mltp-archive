# mltp-archive

This is an archive of MLTP matches from S10 to present. Each JSON file under the majors and minors folders corresponds to a match played by two teams in one week of play and uses the following naming convention:

`season_week_team1abbr_team2abbr.json`

In addition, raw data for scores and player statistics is included as .tsv files in the `/tsv_data` folder. The structures for each of these files is detailed below. For convenience, here are links to most of the data in Google Sheets:

Link | Description
:--: | :--:
[Majors Game Data](https://docs.google.com/spreadsheets/d/1-m2QGi9HP-h8SSK5KHvyD5hxZkFKhAsfbRDe3jFLLKI/edit?usp=sharing) | Player statistics per game (MLTP)
[Majors Half Data](https://docs.google.com/spreadsheets/d/1g2rZKevIsY8mFhLSJpzVLHMGrnOMk98ihJJ_kcJ573w/edit?usp=sharing) | Player statistics per half (MLTP)
[Majors Score Data](https://docs.google.com/spreadsheets/d/1MB-vc9L4TQTjf5Tn5nNsiJaSI3tUOsN-JvOQ7r4xs2I/edit?usp=sharing) | Match scores per game and per half (MLTP)
[Minors Game Data](https://docs.google.com/spreadsheets/d/1QNxg5Ao3KgswdLEVv4Ol-vTpkN4kL9dD5T_F7F_mi9w/edit?usp=sharing) | Player statistics per game (mLTP)
[Minors Half Data](https://docs.google.com/spreadsheets/d/1XEgQBjptYu1p0ZQLMpQ23J3O70EEQ9xdi0oRDq38S8s/edit?usp=sharing) | Player statistics per half (mLTP)
[Minors Score Data](https://docs.google.com/spreadsheets/d/1ODLMo6nl72I6RUZA5e_iw1-swhMqlX0nR6yJUSx58VA/edit?usp=sharing) | Match scores per game and per half (mLTP)

You are free to use this data however you see fit and are encouraged to post any bulk analysis to the [/r/MLTP subreddit](https://www.reddit.com/r/MLTP). If you are using this data in a public-facing manner, please include a link to this repository so others can use this data as well.

# Table of Contents
- **[Match Data Structure](#match-data-structure)**
	- [JSON Structure](#json-stucture)
	- [TSV Structure](#tsv-structure)
	- [Overtime](#overtime)
- **[Abbreviations Structure](#abbreviations-structure)**
	- [tier_info.json Structure](#tier_infojson-structure)
	- [Abbreviation Rules](#abbreviation-rules)
- **[Statistics Structure](#statistics-structure)**
	- [Stats Information](#stats-information)
	- [Stats Issues](#stats-issues)
- **[To-Do](#to-do)**

# Match Data Structure

## JSON Stucture
Each file contains information about the match played in the following format:

```js
{
    "season": 10, // season this match corresponds to
    "week": 1, // week this match corresponds to
    "team1": "MAB", // team abbreviation for the first team in this match
    "team2": "MBC", // team abbreviation for the second team in this match
    "game1": { //information about game1 of the match
        "map": "EMERALD", // map game1 was played on
        "scores": { // scores from each half of g1
            "t1h1": 6, // caps scored by team1 during half 1
            "t1h2": 3, // caps scored by team1 during half 2
            "t1ot": 0, // caps scored by team1 during OT
            "t2h1": 2, // caps scored by team2 during half 1
            "t2h2": 4, // caps scored by team2 during half 2
            "t2ot": 0, // caps scored by team2 during OT
        },
        "links": {
            "h1": [...], // array of links corresponding to half 1
            "h2": [...], // array of links corresponding to half 2
            "ot": [...], // array of links corresponding to OT
        },
        "stats": { // individual half statistics
            "h1": { // statistics corresponding to half 1
                "Altiger": { // player 1
                    // stats will be detailed at the bottom
                }
            },
            "h2": {...}, // statistics corresponding to half 2
            "ot": {...}, // statistics corresponding to OT
            "total": {...} // the summation of half 1 and half 2 statistics
        }
    }
    "game2": {} // game2 follows the same format as game1
}
```
## TSV Structure

For convenience, much of the data stored in the json files has also been converted into TSV files. This data can be easily imported into Excel or you can just copy the data from the Google Sheets spreadsheets linked above. (Both contain the same corresponding information.) Each tsv file holds different sections of the complete data stored in the json files.

`majors_ scores_by_game.tsv` and `minors_scores_by_game.tsv` hold the score data by game for the respective tier. OT scores for each team (t1OT and t2OT) are in separate columns from the t1score and t2score, which are the summation of the h1 and h2 scores for the respective teams.

`majors_scores_by_half.tsv` and `minors_scores_by_half.tsv` hold the score data by half for the respective tier. OT scores for each team are represented as a third half (`OT` in the half column) for each game.

For both of these datasets, every game/half will have a value in the respective OT position. I have kept them in for now to ensure consistency, so if you need to check for OT, I would recommend checking to see if `t1OT` and `t2OT` are both zero OR if `t1score` and `t2score` are not equal.

`majors_stats_by_game.tsv` and `minors_stats_by_game.tsv` hold the player data by game for the respective tier. The stats follow the same order as the JSON files, so you can refer to [Stats Information](#stats-information) if you need help deciphering statistics. Statistics by game do not include overtime statistics.

`majors_stats_by_half.tsv` and `minors_stats_by_half.tsv` hold the player data by half for the respective tier. The stats follow the same order as the JSON files, so you can refer to [Stats Information](#stats-information) if you need help deciphering statistics. OT stats are included here as a third half (`OT` in the half column) for each game that had an overtime period.

## Overtime
All OT properties will appear in the json file irrespective of whether or not OT was played during the game. If you need to detect whether or not a game had overtime, you can check the length of gameX["links"]["ot"], as it will be non-zero when overtime occurred.

Total statistics does not include overtime statistics because not every game plays overtime. If you need to include overtime in your analysis, you can add the statistics manually.

# Abbreviations Structure

## tier_info.json-Structure

Teams are not sorted alphabetically in a single match and have been standardized to team abbreviations. There are two files, `majors_info.json` and `minors_info.json` which contain information about each team and the seasons that team was active.

```js
{
    "M877": { // standardized abbreviation used in the match files
        "name": "877-CAPSNOW", // regular team name
        "seasons": [14] // seasons the team was active in MLTP
    }
}
```

All abbreviations are accounted for in the respective info.json files, so you can simply refer to those files if you need to use the regular team name for your analysis instead of the abbreviations.

## Abbreviation Rules

All teams have a standardized abbreviation using the following rules:
- The first letter of a team's abbreviation will define the tier of the team. This identifier is `M` for MLTP majors and `N` for MLTP minors.
- This will be followed by a 2-3 character (all teams who played their first season after season 14 will have three characters, any teams prior may elect to use their historical 2 character abbreviation if applicable) unique alphanumeric identifier for the team.
- A team is defined as a historical team if it played its first season prior to season 14, when abbreviations were first standardized.

Certain teams do not use the tier identifier because their historical abbreviation was four characters:

Tier | Abbreviation | Team
:--: | :--: | :--:
Majors | DLTP | A Developmental Lad
Majors | RHCP | Red Hot Chili Poppers
Minors | BHCP | Blue Hot Chili Poppers

All teams from S10 to present other than the teams listed above conform to these rules, even if that team played in a season prior to season 14. (i.e. `AB` for Angry Balls in season 10 has been changed to `MAB` in this dataset.)
 
# Statistics Structure
## Stats Information

All statistics after cohandoff (Caps off Handoffs) on the following table are derived from the raw statistics before it. They are included in this dataset as a courtesy since TPL displays these statistics as well. If you plan on extending this dataset by combining matches together in some fashion, you should recalculate all of these statistics with the definition shown below, since your results will be incorrect if you add them together like you would the raw statistics.

Statistic | Full Name | Description
:--: | :--: | :--:
score | Score | -
team | Team | Abbreviation of the team which player corresponds to
grabs | Grabs | -
pops | Pops | -
drops | Drops | -
hold | Hold | Hold in seconds
captures | Captures | -
prevent | Prevent | -
ndpops | Non-Drop Pops | # of pops that did not come from drops (pops - drops)
returns | Returns | -
tags | Tags | -
pups | Powerups | -
minutes | Minutes | -
goregrab | Grabs off Regrab | # of grabs player made off regrab
longholds | Long Holds | Will be updated
goodhandoff | Good Handoffs | # of handoffs which resulted in a teammate hold of >5 seconds
handoff | Handoffs | Teammate grabs within two seconds of a player hold of <3 seconds
coregrab | Caps off Regrab | # of caps from grabs player made off regrab
retinbase | Returns in Base | # of returns within 5 tiles of the player's flag
nrtags | Non-Return Tags | # of tags that did not come from returns (tags-returns)
holdagainst | Hold Against | Amount of hold the opposing team accumulated during the match
pupscomp | Total Powerups | Total number of powerups available during the match
pm | Plus/Minus | -
quickret | Quick Returns | # of returns where the flag carrier had a hold of <2 seconds
flaccids | Flaccids | # of grabs player made with a hold of <2 seconds
gohandoff | Grabs off Handoff | # of grabs player made off handoff
keyret | Key Returns | # of returns which resulted in a team capture within three seconds
saves | Saves | # of returns within 5 tiles of the enemy team flag
cohandoff | Caps off Handoff | # of caps from grabs the player made off a handoff
capspm | Caps per Minute | Caps/Minutes
holdpm | Hold per Minute | Hold/Minutes
grabspm | Grabs per Minute | Grabs/Minutes
score% | Score Percent | Caps/Grabs
holdpgrab | Hold per Grab | Hold/Grabs
spark% | Spark Percent | # of captures which were self-produced (not from regrab/handoff)
flcd% | Flaccid Percent | Flaccids/Grabs
tagspm | Tags per Minute | Tags/Minutes
retpm | Returns per Minute | Returns/Minutes
prepm | Prevent per Minute | Prevent/Minutes
hapm | Hold Against per Minute | Hold Against/Minutes
prepret | Prevent per Return | Prevent/Returns
prepha | Prevent per Hold Against | Prevent/Hold Against
rib% | Return in Base Percent | Returns in Base/Returns
qr% | Quick Return Percent | Quick Returns/Returns
nrtpm | Non-Return Tags per Minute | Non-Return Tags/Minutes
kd | Kill/Death Ratio | Tags/Pops
kf | Kept Flags | # of indefinite grabs (grabs-drops-captures)
pup% | Pup Percentage | pups/pupscomp

## Stats Issues

The TPL stats extractor currently being used isn't perfect and has some issues. If you are doing analysis with this data set, you should take these issues into account. If the TPL stats extractor is updated and issues are resolved, I will update this section accordingly.

Statistic | Issue
:--: | :--:
Minutes | Minutes is rounded to the nearest integer. This will result in small differences for minute based stats from their true value.
Hold Against | Hold Against is calculated by half. This means players who do not play the full match length will have inaccurate HA because the full HA value is assigned.
Plus/Minus | Like HA, Plus/Minus is calculated by half. This means players who do not play the full match length will have inaccurate PM because the full PM value is assigned.
Saves | Saves do not register 100% of the time when using the TPL extractor.
Hold Against per Minute | While all per-minute statistics will be slightly inaccurate as described above, HAPM may produce mathematically impossible results (i.e. >60) if the player did not play the full match length.

In addition, some matches will not have advanced statistics (i.e. statistics calculated from the match timeline) because a [tagpro.eu](https://tagpro.eu) match was not available. Do not use pastebin links as the only condition for detecting matches without advanced statistics, as some matches may use pastebin to upload tagpro.eu match data that did not upload properly due to some error.

# To-Do
1. Fix team name errors for tied halves (oops)
2. Rename players as needed (rip)
3. Standardize team abbreviations for teams prior to season 10
4. Import data for seasons prior to season 10
5. Profit?