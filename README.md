<img src="/.logo.svg" alt="logo" width="50"/>

# PWHL Data Documentation

This document serves as an unofficial reference for the Professional Women's Hockey League (PWHL) data sources.
Corrections and suggestions are welcome!

In addition to available formatted data, there appear to be two primary sources for PWHL APIs:

1. HockeyTech/LeagueStat API (`lscluster.hockeytech.com`) - Used primarily for historical data and statistics

2. Firebase API (`leaguestat-b9523.firebaseio.com`) - Used primarily for live game data

This document is broken into distinct sections detailing each data source.

## Table of Contents

### [HockeyTech/LeagueStat API](#hockeytech-api-documentation)

1. [Base URL](#hockeytech-base-url)
2. [API Information](#league-information)
    1. [Standings](#standings-1)
        1. [Get League Standings](#get-league-standings)
        2. [Get Team Standings by Division](#get-team-standings-by-division)
    2. [Players](#players)
        1. [Get All Skaters](#get-all-skaters)
        2. [Get All Goalies](#get-all-goalies)
        3. [Get Top Players](#get-top-players)
        4. [Get Player Profile](#get-player-profile)
        5. [Get Player Leaders](#get-player-leaders)
    3. [Teams](#teams)
        1. [Get Team Roster](#get-team-roster)
    4. [Game Information](#game-information)
        1. [Get Game Summary](#get-game-summary)
        2. [Get Play-by-Play](#get-play-by-play)
        3. [Get Game Center Preview](#get-game-center-preview)
    5. [Schedule](#schedule)
        1. [Get Scorebar](#get-scorebar)
    6. [Playoffs](#playoffs)
        1. [Get Playoff Bracket](#get-playoff-bracket)
    7. [Bootstrap Data](#bootstrap-data)
        1. [Get Scorebar Bootstrap](#get-scorebar-bootstrap)
        2. [Get Game Summary Bootstrap](#get-game-summary-bootstrap)

### [Firebase API](#firebase-api-documentation)

1. [Base URL](#firebase-base-url)
2. [Game Data](#game-data)
    1. [All Live Game Data](#all-live-game-data)
    2. [Game Clock](#game-clock)
        1. [Running Clock](#get-running-clock)
        2. [Published Clock](#get-published-clock)
    3. [Game Events](#game-events)
        1. [Faceoffs](#get-faceoffs)
        2. [Goals](#get-goals)
        3. [Penalties](#get-penalties)
        4. [Shot Summary](#get-shot-summary)

### [Formatted Data](#formatted-data)

1. [Base URL](#hockeytech-base-url-1)
2. [Mobile Site](#mobile-site)
    1. [League Schedule](#league-schedule)
        1. [Monthly Schedule](#monthly-schedule)
        2. [Daily Schedule](#daily-schedule)
        3. [Calendar Feed](#calendar-feed)
    2. [Game Summaries](#game-summaries)
    3. [Team Rosters](#team-rosters)
    4. [Player Statistics](#player-statistics)
    5. [Player Profile](#player-profile)
3. [Media Access](#media-access)
    1. [Standings](#standings)
    2. [Daily Report](#daily-report)
    3. [Team Reports](#team-reports)
        1. [Season Schedule](#season-schedule)
        2. [Player Game by Game](#player-game-by-game)
        3. [Roster](#roster)
    4. [Special Reports](#special-reports)
        1. [Team Head to Head](#team-head-to-head)
        2. [Player Stats By Team](#player-stats-by-team)
        3. [Overall Team Records](#overall-team-records)
        4. [Team Game Highs and Lows](#team-game-highs-and-lows)
        5. [Attendance Report](#attendance-report)

---

# HockeyTech API Documentation

This section provides documentation for the PWHL HockeyTech API (via LeagueStat), which is primarily used for historical
data and statistics.

## HockeyTech Base URL

All endpoints described in this section are relative to the following base URL:

```
https://lscluster.hockeytech.com/
```

Most HockeyTech API endpoints require the following parameters:

```
key=446521baf8c38984&client_code=pwhl
```

## League Information

### Standings

#### Get League Standings

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve current PWHL standings grouped by division.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `teams`
    - `groupTeamsBy` = `division`
    - `context` = `overall`
    - `site_id` = `0`
    - `season` = `5` (or specific season ID)
    - `special` = `false`
    - `league_id` = `1`
    - `sort` = `points`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=teams&groupTeamsBy=division&context=overall&site_id=0&season=5&special=false&key=446521baf8c38984&client_code=pwhl&league_id=1&conference=-1&division=-1&sort=points&lang=en"
```

#### Get Team Standings by Division

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve team standings for a specific division.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `teams`
    - `groupTeamsBy` = `division`
    - `context` = `overall`
    - `season` = `5` (or specific season ID)
    - `division` = `1` (division ID)
    - `league_id` = `1`
    - `statsType` = `inline`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=teams&groupTeamsBy=division&context=overall&season=5&division=1&key=446521baf8c38984&client_code=pwhl&league_id=1&statsType=inline&lang=en"
```

### Players

#### Get All Skaters

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve statistics for all skaters in the league.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `players`
    - `season` = `5` (or specific season ID)
    - `team` = `all`
    - `position` = `skaters`
    - `rookies` = `0`
    - `statsType` = `standard`
    - `league_id` = `1`
    - `limit` = `500`
    - `sort` = `points`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=players&season=5&team=all&position=skaters&rookies=0&statsType=standard&rosterstatus=undefined&site_id=0&league_id=1&lang=en&division=-1&conference=-1&key=446521baf8c38984&client_code=pwhl&league_id=1&limit=500&sort=points&league_id=1&lang=en&division=-1&conference=-1"
```

#### Get All Goalies

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve statistics for all goalies in the league.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `players`
    - `season` = `5` (or specific season ID)
    - `team` = `all`
    - `position` = `goalies`
    - `rookies` = `0`
    - `statsType` = `standard`
    - `league_id` = `1`
    - `limit` = `500`
    - `sort` = `gaa`
    - `qualified` = `all`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=players&season=5&team=all&position=goalies&rookies=0&statsType=standard&rosterstatus=undefined&site_id=0&first=0&limit=500&sort=gaa&league_id=1&lang=en&division=-1&conference=-1&qualified=all&key=446521baf8c38984&client_code=pwhl&league_id=1"
```

#### Get Top Players

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve statistics for top players in the league.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `players`
    - `season` = `5` (or specific season ID)
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=players&season=5&key=446521baf8c38984&client_code=pwhl"
```

#### Get Player Profile

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve detailed information for a specific player.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `player`
    - `player_id` = `32` (or specific player ID)
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=player&player_id=32&key=446521baf8c38984&client_code=pwhl"
```

#### Get Player Leaders

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve extended statistics for league leaders.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `leadersExtended`
    - `season_id` = `5` (or specific season ID)
    - `team_id` = `0` (all teams)
    - `playerTypes` = `skaters`
    - `skaterStatTypes` = `points,goals` (comma-separated stat categories)
    - `goalieStatTypes` = `save_percentage,wins,goals_against_average,shutouts` (comma-separated stat categories)
    - `activeOnly` = `0`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=leadersExtended&key=446521baf8c38984&league_id=undefined&season_id=5&division=&conference=&team_id=0&site_id=0&client_code=pwhl&playerTypes=skaters&skaterStatTypes=points,goals&goalieStatTypes=save_percentage,wins,goals_against_average,shutouts&activeOnly=0&lang=en"
```

### Teams

#### Get Team Roster

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve roster for a specific team.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `roster`
    - `team_id` = `3` (or specific team ID)
    - `season_id` = `5` (or specific season ID)
    - `site_id` = `0`
    - `league_id` = `1`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=roster&team_id=3&season_id=5&key=446521baf8c38984&client_code=pwhl&site_id=0&league_id=1&lang=en"
```

### Game Information

#### Get Game Summary

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve summary information for a specific game.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `gameSummary`
    - `game_id` = `137` (or specific game ID)
    - `site_id` = `0`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=gameSummary&game_id=137&key=446521baf8c38984&site_id=0&client_code=pwhl&lang=en"
```

#### Get Play-by-Play

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve play-by-play data for a specific game.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `gameCenterPlayByPlay`
    - `game_id` = `137` (or specific game ID)
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=gameCenterPlayByPlay&game_id=137&key=446521baf8c38984&client_code=pwhl"
```

#### Get Game Center Preview

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve preview information for a specific game.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `gameCenterPreview`
    - `game_id` = `137` (or specific game ID)
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=gameCenterPreview&game_id=137&key=446521baf8c38984&client_code=pwhl&lang=en"
```

### Schedule

#### Get Scorebar

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve schedule and score information for upcoming games.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `scorebar`
    - `site_id` = `0`
    - `numberofdaysback` = `0`
    - `numberofdaysahead` = `1000`
    - `league_id` = `1`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=scorebar&site_id=0&numberofdaysback=0&numberofdaysahead=1000&key=446521baf8c38984&client_code=pwhl&league_id=1&conference=-1&division=-1&lang=en"
```

For a more limited view with JSON format specified:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&key=446521baf8c38984&client_code=pwhl&view=scorebar&numberofdaysahead=6&numberofdaysback=0&limit=1000&fmt=json&site_id=0&lang=en&league_id=1"
```

### Playoffs

#### Get Playoff Bracket

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve playoff bracket information.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `brackets`
    - `season_id` = `3` (or specific season ID)
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=brackets&season_id=3&key=446521baf8c38984&client_code=pwhl"
```

### Bootstrap Data

#### Get Scorebar Bootstrap

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve bootstrap configuration data for scorebar.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `bootstrap`
    - `season` = `latest`
    - `pageName` = `scorebar`
    - `site_id` = `0`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=bootstrap&season=latest&pageName=scorebar&key=446521baf8c38984&client_code=pwhl&site_id=0&league_id=&league_code=&conference=-1&division=-1&lang=en"
```

#### Get Game Summary Bootstrap

- **Endpoint**: `feed/index.php`
- **Method**: GET
- **Description**: Retrieve bootstrap configuration data for game summary.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `bootstrap`
    - `season` = `null`
    - `pageName` = `game-summary`
    - `site_id` = `0`
    - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=bootstrap&season=null&pageName=game-summary&key=446521baf8c38984&client_code=pwhl&site_id=0&league_id=&league_code=&conference=-1&division=-1&lang=en"
```

---

# Firebase API Documentation

This section provides documentation for the PWHL Firebase API, which is primarily used for real-time game data.

## Firebase Base URL

All endpoints described in this section are relative to the following base URL:

```
https://leaguestat-b9523.firebaseio.com/svf/pwhl
```

The Firebase API endpoints typically require authentication parameters:

```
?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ&key=AIzaSyBVn0Gr6zIFtba-hQy3StkifD8bb7Hi68A
```

## Game Data

### All Live Game Data

- **Endpoint**: `.json`
- **Method**: GET
- **Description**: Retrieve all available real-time data for current PWHL games.
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ&key=AIzaSyBVn0Gr6zIFtba-hQy3StkifD8bb7Hi68A"
```

### Game Clock

#### Get Running Clock

- **Endpoint**: `/runningclock.json`
- **Method**: GET
- **Description**: Retrieve the current running clock data for active games.
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/runningclock.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

#### Get Published Clock

- **Endpoint**: `/publishedclock.json`
- **Method**: GET
- **Description**: Retrieve the published clock data for active games.
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/publishedclock.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

### Game Events

#### Get Faceoffs

- **Endpoint**: `/faceoffs.json`
- **Method**: GET
- **Description**: Retrieve faceoff data from active games.
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/faceoffs.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

#### Get Goals

- **Endpoint**: `/goals.json`
- **Method**: GET
- **Description**: Retrieve goal data from active games.
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/goals.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

#### Get Penalties

- **Endpoint**: `/penalties.json`
- **Method**: GET
- **Description**: Retrieve penalty data from active games.
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/penalties.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

#### Get Shot Summary

- **Endpoint**: `/shotssummary.json`
- **Method**: GET
- **Description**: Retrieve shot summary data from active games.
- **Response**: JSON format

###### Example using cURL:

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/shotssummary.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

---

# Formatted Data Documentation

This section provides references for the publically-available formatted data, such as game calendars, standings tables,
and player statistics.

## HockeyTech Base URL

Since formatted data seems to be provided entirely by HockeyTech/LeagueStat, all endpoints described in this section are
relative to the following base URL:

```
https://lscluster.hockeytech.com/
```

## Mobile Site

### League Schedule

#### Monthly Schedule

- **Endpoint**: `statview/mobile/pwhl/schedule`
- **Description**: View a calendar of games for the current month.

###### Full URL:

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/schedule
```

#### Daily Schedule

- **Endpoint**: `statview/mobile/pwhl/daily-schedule`
- **Description**: View a list of games by date.

###### Full URL:

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/daily-schedule
```

#### Calendar Feed

- **Endpoint**: `components/calendar/ical_add_games.php`
- **Description**: Download the game calendar for a given season.
- **Parameters**:
    - `client_code` = `pwhl`
    - `season` = `5` (or specific season ID)

###### Full URL:

```
https://lscluster.hockeytech.com/components/calendar/ical_add_games.php?client_code=pwhl&season_id=5
```

### Game Summaries

- **Endpoint**: `statview/mobile/pwhl/game-center`
- **Description**: View the game summary for a given game.

###### Full URL:

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/game-center/137
```

### Team Rosters

- **Endpoint**: `statview/mobile/pwhl/roster`
- **Description**: Retrieve a table of player statistics.

###### Full URL:

The example below shows the roster for team 3 (MTL) for season 5 (2024-2025 Regular Season).

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/roster/3/5
```

### Player Statistics

- **Endpoint**: `statview/mobile/pwhl/player-stats`
- **Description**: Retrieve a table of player statistics.

###### Full URL:

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/player-stats
```

### Player Profile

- **Endpoint**: `statview/mobile/pwhl/player`
- **Description**: Retrieve a table of player statistics.

###### Full URL:

The example below shows the profile for player 32 (Laura Stacey) for season 5 (2024-2025 Regular Season).

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/player/32/5
```

## Media Access

### Standings

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Retrieve team standings for the league.
- **Parameters**:
    - `step` = `4`
    - `sub` = `0`
    - `season_id` = `5` (or specific season ID)
    - `order` = `overall`

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?step=4&sub=0
```

### Daily Report

- **Endpoint**: `download.php`
- **Description**: View the daily report for the league.
- **Parameters**:
    - `client_code` = `pwhl`
    - `file_path` = `daily-report`

###### Full URLs:

```
https://lscluster.hockeytech.com/download.php?client_code=pwhl&file_path=daily-report/daily-report.html
```

```
https://lscluster.hockeytech.com/download.php?client_code=pwhl&file_path=daily-report/daily-report.pdf
```

### Team Reports

#### Season Schedule

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Retrieve the season schedule for a given team.
- **Parameters**:
    - `step` = `4`
    - `sub` = `9`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)
    - `team` = `3` (or specific team ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?step=4&sub=9&format=HTML&season_id=5&team=3
```

#### Player Game by Game

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Retrieve player game-by-game report for a given team.
- **Parameters**:
    - `step` = `4`
    - `sub` = `11`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)
    - `team` = `3` (or specific team ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?step=4&sub=11&format=HTML&season_id=5&team=3
```

#### Roster

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Retrieve the roster for a given team.
- **Parameters**:
    - `step` = `4`
    - `sub` = `4`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)
    - `team` = `3` (or specific team ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?step=4&sub=4&format=HTML&season_id=5&team=3
```

## Special Reports

#### Team Head to Head

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Retrieve the head-to-head records for two teams for a given season.
- **Parameters**:
    - `step` = `4`
    - `sub` = `13`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)
    - `team` = `3` (or specific team ID)
    - `second_team` = `5` (or specific team ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?season_id=5&step=4&sub=13
```

#### Player Stats By Team

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Retrieve player stats by team for a given season.
- **Parameters**:
    - `step` = `4`
    - `sub` = `1`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?format=HTML&season_id=5&step=4&sub=1
```

#### Overall Team Records

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Retrieve detailed team records for a given season.
- **Parameters**:
    - `step` = `4`
    - `sub` = `10`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?format=HTML&season_id=5&step=4&sub=10
```

#### Team Game Highs and Lows

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Show game records for a given season (i.e., most goals, most saves, etc.).
- **Parameters**:
    - `step` = `4`
    - `sub` = `12`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?format=HTML&season_id=5&step=4&sub=12
```

#### Attendance Report

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Show the attendance report for a given season.
- **Parameters**:
    - `step` = `4`
    - `sub` = `15`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?format=HTML&season_id=5&step=4&sub=15
```

#### Hat Tricks and Shutouts

- **Endpoint**: `media/pwhl/pwhl/index.php`
- **Description**: Show hat trick and shutout records for a given season.
- **Parameters**:
    - `step` = `4`
    - `sub` = `16`
    - `format` = `HTML` (or `CSV`, `TAB`, `Word2000`)
    - `season_id` = `5` (or specific season ID)

###### Full URL:

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?format=HTML&season_id=5&step=4&sub=16
```

---

## Notes on API Usage

1. **Authentication**:
    - Firebase API requires both `auth` and `key` parameters
    - HockeyTech API requires `key` and `client_code` parameters

2. **Season IDs**:
    - HockeyTech API uses numeric season IDs (e.g., `5` for the 2023-2024 season)

3. **Game IDs**:
    - Each game has a unique numeric ID used across both API systems

4. **Pagination**:
    - Use `limit` and `first` (or `start`) parameters for pagination in HockeyTech API endpoints

5. **Error Handling**:
    - The APIs do not consistently return standard HTTP status codes for errors
    - Check for specific error fields in the JSON response
