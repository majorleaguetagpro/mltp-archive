# mltp-archive

This is an archive of MLTP matches from S10 to present. Each JSON file under the majors and minors folders corresponds to a match played by two teams in one week of play and follows the following format:

`season_week_team1abbr_team2abbr.json`

---

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

All OT properties will appear in the json file irrespective of whether or not OT was played during the game. If you need to detect whether or not a game had overtime, you can check the length of gameX["links"]["ot"], as it will be non-zero when overtime occurred.  

---

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

