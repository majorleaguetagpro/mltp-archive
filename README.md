
# mltp-archive

This is an archive of MLTP matches from S10 to present. Each JSON file under the majors and minors folders corresponds to a match played by two teams in one week of play and follows the following format:

`season_week_team1abbr_team2abbr.json`

In addition, raw game/half data is included as .tsv files. For convenience, here are links to the data in Google Sheets:

Link | Description
:--: | :--:
[Majors Game Data](https://docs.google.com/spreadsheets/d/1-m2QGi9HP-h8SSK5KHvyD5hxZkFKhAsfbRDe3jFLLKI/edit?usp=sharing) | Player statistics per game (MLTP)
[Majors Half Data](https://docs.google.com/spreadsheets/d/1g2rZKevIsY8mFhLSJpzVLHMGrnOMk98ihJJ_kcJ573w/edit?usp=sharing) | Player statistics per half (MLTP)
[Minors Game Data](https://docs.google.com/spreadsheets/d/1QNxg5Ao3KgswdLEVv4Ol-vTpkN4kL9dD5T_F7F_mi9w/edit?usp=sharing) | Player statistics per game (mLTP)
[Minors Half Data](https://docs.google.com/spreadsheets/d/1XEgQBjptYu1p0ZQLMpQ23J3O70EEQ9xdi0oRDq38S8s/edit?usp=sharing) | Player statistics per half (mLTP)

# Table of Contents
- **[Match Data Structure](#Match-Data-Structure)**
	- [JSON Structure](#JSON-Structure) / [Overtime](#Overtime)
- **[Abbreviations Structure](#Abbreviations-Structure)**
	- [tier_info.json Structure](#tier_info.json-Structure)/[Abbreviation Rules](#Abbreviation-Rules)
- **[Statistics Structure](#Statistics-Structure)**
	- [Stats Information](#Stats-Information)/[Stats Issues](#Stats-Issues)
-**[To-Do](#To-Do)**

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
## Overtime
All OT properties will appear in the json file irrespective of whether or not OT was played during the game. If you need to detect whether or not a game had overtime, you can check the length of gameX["links"]["ot"], as it will be non-zero when overtime occurred.  

# Abbreviations Structure

## tier_info.json-Structure

Teams are not sorted alphabetically in a single match and have been standardized to team abbreviations. There are two files, `majors_info.json` and `minors_info.json` which contain information about each team and the seasons that team was active.

```js
{
    "M877": { // standardized abbreviation used in the match files
        "name": "877-CAPSNOW", // regular team name
        "seasons": ["14"] // seasons the team was active in MLTP
    }
}
```

All abbreviations are accounted for in the respective info.json files, so you can simply refer to those files if you need to use the regular team name for your analysis instead of the abbreviations.

## Abbreviation Rules
Will be updated.

# Statistics Structure
## Stats Information
Statistic | Full Name | Description
:--: | :--: | :--:
score | Score | -
team | Team | Player's team during the half (1 for red, 2 for blue)
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
Team | If using game data instead of half data, note that team number may not accurately represent true teams (i.e. whether player is a member of team1 or team2.) In the future, team will represent true team instead of red/blue during the match.
Minutes | Minutes is rounded to the nearest integer. This will result in small differences for minute based stats from their true value.
Hold Against | Hold Against is calculated by half. This means players who do not play the full match length will have inaccurate HA because the full HA value is assigned.
Plus/Minus | Like HA, Plus/Minus is calculated by half. This means players who do not play the full match length will have inaccurate PM because the full PM value is assigned.
Saves | Saves do not register 100% of the time when using the TPL extractor.
Hold Against per Minute | While all per-minute statistics will be slightly inaccurate as described above, HAPM may produce mathematically impossible results if the player did not play the full match length.

# To-Do
1. Fix undefined maps
2. Rename community selection to proper map names
3. Change team to proper team names instead of integers
4. Profit?