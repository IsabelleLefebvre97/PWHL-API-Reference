<img src="/.logo.svg" alt="logo" width="50"/>

# PWHL Data Documentation

This document serves as an unofficial reference for the Professional Women's Hockey League (PWHL) data sources.
Corrections and suggestions are welcome!

There appear to be two primary sources for PWHL APIs:

1. **HockeyTech/LeagueStat API** (`lscluster.hockeytech.com`) - Used primarily for historical data and statistics

2. **Firebase API** (`leaguestat-b9523.firebaseio.com`) - Used primarily for live game data

This document is broken into distinct sections detailing each data source.

## Table of Contents

### [HockeyTech/LeagueStat API](#hockeytech-api-documentation)

1. [Base URL](#hockeytech-base-url)
2. [Season Information](#season-information)
3. [Schedule Information](#schedule-information)
    1. [Season Schedule](#season-game-schedule)
    2. [Team Schedule](#team-schedule)
    3. [Daily Schedule](#daily-schedule)
    4. [Scorebar](#scorebar)
4. [Team Information](#team-information)
    1. [All Teams](#all-teams)
    2. [Rosters](#rosters)
    3. [League Standings](#league-standings)
5. [Player Information](#player-information)
    1. [Skaters](#skaters)
        1. [All Skaters](#all-skaters)
        2. [Skater Statistics by Team](#skater-statistics-by-team)
    2. [Goalies]()
        1. [All Goalies](#all-goalies)
        2. [Goalie Statistics by Team](#goalie-statistics-by-team)
    3. [Player Details](#player-details)
        1. [Player Profile](#player-profile)
        2. [Game-by-Game](#game-by-game)
        3. [Season Statistics](#season-statistics)
        4. [Most Recent Season Statistics](#most-recent-season-statistics)
    4. [League Leaders](#league-leaders)
        1. [Leading Skaters](#leading-skaters)
        2. [Top Scorers](#top-scorers)
        3. [Leading Goalies](#leading-goalies)
        4. [Top Goalies](#top-goalies)
    5. [Player Streaks](#player-streaks)
    6. [Player Transactions](#player-transactions)
    7. [Player Search](#player-search)
6. [Game Information](#game-information)
    1. [Game Preview](#game-preview)
    2. [Game Clock](#game-clock)
    3. [Play-by-Play (Short)](#play-by-play-short)
    4. [Play-by-Play (Long)](#play-by-play-long)
    5. [Game Summary](#game-summary)
7. [Playoff Information](#playoff-information)
8. [Bootstrap Data](#bootstrap-data)
    1. [Get Scorebar Bootstrap](#get-scorebar-bootstrap)
    2. [Get Game Summary Bootstrap](#get-game-summary-bootstrap)

### [Firebase API](#firebase-api-documentation)

1. [Base URL](#firebase-base-url)
2. [All Live Game Data](#all-live-game-data)
3. [Game Clock](#game-clock-1)
    1. [Running Clock](#running-clock)
    2. [Published Clock](#published-clock)
4. [Game Events](#game-events)
    1. [Faceoffs](#faceoffs)
    2. [Goals](#goals)
    3. [Penalties](#penalties)
    4. [Shot Summary](#shot-summary)

### [Formatted Data](#formatted-data)

1. [Base URL](#hockeytech-base-url-1)
2. [Mobile Site](#mobile-site)
    1. [League Schedule](#league-schedule)
        1. [Monthly Schedule](#monthly-schedule)
        2. [Daily Schedule](#daily-schedule-1)
        3. [Calendar Feed](#calendar-feed)
    2. [Game Summaries](#game-summaries)
    3. [Team Rosters](#team-rosters)
    4. [Player Statistics](#player-statistics)
    5. [Player Profile](#player-profile-1)
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
        6. [Hat Tricks and Shutouts](#hat-tricks-and-shutouts)

### [Notes on API Usage](#notes-on-api-usage)

---

# HockeyTech API Documentation

This section provides documentation for the PWHL HockeyTech API (via LeagueStat), which is primarily used for historical
data and statistics.

## HockeyTech Base URL

All endpoints described in this section are relative to the following base URL:

```
https://lscluster.hockeytech.com/feed/
```

Most HockeyTech API endpoints require the following parameters:

```
key=446521baf8c38984&client_code=pwhl
```

## Season Information

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve all PWHL seasons.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `seasons`
- **Response**: JSON format
- **Output**: [seasons.csv](./data/seasons.csv)

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=seasons&key=446521baf8c38984&client_code=pwhl"
```

## Schedule Information

### Season Game Schedule

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve the full game schedule for a given season.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `schedule`
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/?feed=modulekit&view=schedule&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### Team Schedule

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve the game schedule for a given team and season.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `schedule`
    - `team` = `3` (or specific team ID)
    - `season` = `5` (or specific season ID)
    - `month` = `-1` (to include all months)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=schedule&team=3&season=5&month=-1&key=446521baf8c38984&client_code=pwhl"
```

### Daily Schedule

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve the daily game schedule.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `gamesperday`
    - `start_date` = `2023-01-01`
    - `end_date` = `2026-01-01`
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=gamesperday&start_date=2023-01-01&end_date=2026-01-01&key=446521baf8c38984&client_code=pwhl"
```

### Scorebar

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve scorebar information (contains game schedules and scores).
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `scorebar`
    - `numberofdaysback` = `1000`
    - `numberofdaysahead` = `1000`
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=scorebar&numberofdaysback=1000&numberofdaysahead=1000&key=446521baf8c38984&client_code=pwhl"
```

## Team Information

### All Teams

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve all PWHL teams for a given season.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `teamsbyseason`
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format
- **Output**: [teams.csv](./data/teams.csv)

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=teamsbyseason&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### Rosters

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve roster for a specific team.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `roster`
    - `team_id` = `3` (or specific team ID)
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=roster&team_id=3&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### League Standings

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve PWHL standings for a given season.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `statviewtype`
    - `stat` = `conference`
    - `type` = `standings`
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=statviewtype&stat=conference&type=standings&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

## Player Information

### Skaters

#### All Skaters

- **Endpoint**: `index.php`
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

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=players&season=5&team=all&position=skaters&rookies=0&statsType=standard&rosterstatus=undefined&site_id=0&league_id=1&lang=en&division=-1&conference=-1&key=446521baf8c38984&client_code=pwhl&league_id=1&limit=500&sort=points&league_id=1&lang=en&division=-1&conference=-1"
```

#### Skater Statistics by Team

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve skater statistics by team.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `statviewtype`
    - `type` = `skaters`
    - `league_id` = `1`
    - `team_id` = `3` (or specific team ID)
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=statviewtype&type=skaters&league_id=1&team_id=3&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### Goalies

#### All Goalies

- **Endpoint**: `index.php`
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

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=players&season=5&team=all&position=goalies&rookies=0&statsType=standard&rosterstatus=undefined&site_id=0&first=0&limit=500&sort=gaa&league_id=1&lang=en&division=-1&conference=-1&qualified=all&key=446521baf8c38984&client_code=pwhl&league_id=1"
```

#### Goalie Statistics by Team

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve goalie statistics by team.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `statviewtype`
    - `type` = `goalies`
    - `league_id` = `1`
    - `team_id` = `3` (or specific team ID)
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=statviewtype&type=goalies&league_id=1&team_id=3&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### Player Details

#### Player Profile

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve detailed information for a specific player.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `player`
    - `category` = `profile`
    - `player_id` = `32` (or specific player ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/?feed=modulekit&view=player&category=profile&player_id=32&key=446521baf8c38984&client_code=pwhl"
```

#### Player Media

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve media for a specific player.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `player`
    - `category` = `media`
    - `player_id` = `32` (or specific player ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/?feed=modulekit&view=player&category=media&player_id=32&key=446521baf8c38984&client_code=pwhl"
```

#### Game-by-Game

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve game-by-game statistics for a specific player, for a given season.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `player`
    - `category` = `gamebygame`
    - `season_id` = `5` (or specific season ID)
    - `player_id` = `32` (or specific player ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=player&category=gamebygame&season_id=5&player_id=32&key=446521baf8c38984&client_code=pwhl"
```

#### Season Statistics

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve season and career statistics for a specific player.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `player`
    - `category` = `seasonstats`
    - `player_id` = `32` (or specific player ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=player&category=seasonstats&player_id=32&key=446521baf8c38984&client_code=pwhl"
```

#### Most Recent Season Statistics

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve most reason season statistics for a specific player.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `player`
    - `category` = `mostrecentseasonstats`
    - `player_id` = `32` (or specific player ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=player&category=mostrecentseasonstats&player_id=32&key=446521baf8c38984&client_code=pwhl"
```

### League Leaders

#### Leading Skaters

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve extended statistics for top skaters.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `combinedplayers`
    - `type` = `skaters`
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=combinedplayers&type=skaters&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

#### Top Scorers

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve extended statistics for top scorers.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `statviewtype`
    - `type` = `topscorers`
    - `season_id` = `5` (or specific season ID)
    - `first` = `0`
    - `limit` = `100`
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=statviewtype&type=topscorers&first=0&limit=100&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

#### Leading Goalies

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve extended statistics for leading goalies.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `combinedplayers`
    - `type` = `goalies`
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=combinedplayers&type=goalies&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

#### Top Goalies

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve extended statistics for top goalies.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `statviewtype`
    - `type` = `topgoalies`
    - `season_id` = `5` (or specific season ID)
    - `first` = `0`
    - `limit` = `100`
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=statviewtype&type=topgoalies&first=0&limit=100&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### Player Streaks

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve player streaks for the given season.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `statviewtype`
    - `type` = `streaks`
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=statviewtype&type=streaks&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### Player Transactions

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve player transactions for the given season.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `statviewtype`
    - `type` = `transactions`
    - `season_id` = `5` (or specific season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=statviewtype&type=transactions&season_id=5&key=446521baf8c38984&client_code=pwhl"
```

### Player Search

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Search function for players.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `searchplayers`
    - `search_term` = `Poulin`
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=searchplayers&search_term=Poulin&key=446521baf8c38984&client_code=pwhl"
```

## Game Information

### Game Preview

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve preview information for a specific game.
- **Parameters**:
    - `feed` = `gc`
    - `tab` = `preview`
    - `game_id` = `137` (or specific game ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=gc&tab=preview&game_id=137&key=446521baf8c38984&client_code=pwhl"
```

### Game Clock

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve the official clock and basic information for a specific game.
- **Parameters**:
    - `feed` = `gc`
    - `tab` = `clock`
    - `game_id` = `137` (or specific game ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=gc&tab=clock&game_id=137&key=446521baf8c38984&client_code=pwhl"
```

### Play-by-Play (Short)

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve summarized play-by-play data for a specific game.
- **Parameters**:
    - `feed` = `gc`
    - `tab` = `pxp`
    - `game_id` = `137` (or specific game ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=gc&tab=pxp&game_id=137&key=446521baf8c38984&client_code=pwhl"
```

### Play-by-Play (Long)

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve play-by-play data for a specific game.
- **Parameters**:
    - `feed` = `gc`
    - `tab` = `pxpverbose`
    - `game_id` = `137` (or specific game ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=gc&tab=pxpverbose&game_id=137&key=446521baf8c38984&client_code=pwhl"
```

### Game Summary

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve summary information for a specific game.
- **Parameters**:
    - `feed` = `gc`
    - `tab` = `gamesummary`
    - `game_id` = `137` (or specific game ID)
    - `site_id` = `0`
    - `lang` = `en`
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=gc&tab=gamesummary&game_id=137&key=446521baf8c38984&client_code=pwhl"
```

## Playoff Information

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve playoff bracket information.
- **Parameters**:
    - `feed` = `modulekit`
    - `view` = `brackets`
    - `season_id` = `3` (or specific playoff season ID)
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=modulekit&view=brackets&season_id=3&key=446521baf8c38984&client_code=pwhl"
```

## Bootstrap Data

### Get Scorebar Bootstrap

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve bootstrap configuration data for scorebar.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `bootstrap`
    - `season_id` = `latest`
    - `pageName` = `scorebar`
    - `site_id` = `0`
    - `lang` = `en`
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=bootstrap&season=latest&pageName=scorebar&key=446521baf8c38984&client_code=pwhl&site_id=0&league_id=&league_code=&conference=-1&division=-1&lang=en"
```

### Get Game Summary Bootstrap

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve bootstrap configuration data for game summary.
- **Parameters**:
    - `feed` = `statviewfeed`
    - `view` = `bootstrap`
    - `season_id` = `null`
    - `pageName` = `game-summary`
    - `site_id` = `0`
    - `lang` = `en`
- **Response**: JSON format

**Example using cURL:**

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

## All Live Game Data

- **Endpoint**: `.json`
- **Method**: GET
- **Description**: Retrieve all available real-time data for current PWHL games.
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ&key=AIzaSyBVn0Gr6zIFtba-hQy3StkifD8bb7Hi68A"
```

## Game Clock

### Running Clock

- **Endpoint**: `/runningclock.json`
- **Method**: GET
- **Description**: Retrieve the current running clock data for active games.
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/runningclock.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

### Published Clock

- **Endpoint**: `/publishedclock.json`
- **Method**: GET
- **Description**: Retrieve the published clock data for active games.
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/publishedclock.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

## Game Events

### Faceoffs

- **Endpoint**: `/faceoffs.json`
- **Method**: GET
- **Description**: Retrieve faceoff data from active games.
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/faceoffs.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

### Goals

- **Endpoint**: `/goals.json`
- **Method**: GET
- **Description**: Retrieve goal data from active games.
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/goals.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

### Penalties

- **Endpoint**: `/penalties.json`
- **Method**: GET
- **Description**: Retrieve penalty data from active games.
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/penalties.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

### Shot Summary

- **Endpoint**: `/shotssummary.json`
- **Method**: GET
- **Description**: Retrieve shot summary data from active games.
- **Response**: JSON format

**Example using cURL:**

```bash
curl -X GET "https://leaguestat-b9523.firebaseio.com/svf/pwhl/shotssummary.json?auth=uwM69pPkdUhb0UuVAxM8IcA6pBAzATAxOc8979oJ"
```

---

# Formatted Data Documentation

This section provides references for the publicly-available formatted data, such as game calendars, standings tables,
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
- **Description**: View a list of games by calendar month.

**Full URL:**

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/schedule
```

#### Daily Schedule

- **Endpoint**: `statview/mobile/pwhl/daily-schedule`
- **Description**: View a list of games by day.

**Full URL:**

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/daily-schedule
```

#### Calendar Feed

- **Endpoint**: `components/calendar/ical_add_games.php`
- **Description**: Download the league's game calendar for a given season.
- **Parameters**:
    - `client_code` = `pwhl`
    - `season_id` = `5` (or specific season ID)

**Full URL:**

```
https://lscluster.hockeytech.com/components/calendar/ical_add_games.php?client_code=pwhl&season_id=5
```

### Game Summaries

- **Endpoint**: `statview/mobile/pwhl/game-center`
- **Description**: View the game summary for a given game.

**Full URL:**

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/game-center/137
```

### Team Rosters

- **Endpoint**: `statview/mobile/pwhl/roster`
- **Description**: View team rosters.

**Full URL:**

The example below shows the roster for team 3 (MTL) for season 5 (2024-2025 Regular Season).

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/roster/3/5
```

### Player Statistics

- **Endpoint**: `statview/mobile/pwhl/player-stats`
- **Description**: View a player statistics table.

**Full URL:**

```
https://lscluster.hockeytech.com/statview/mobile/pwhl/player-stats
```

### Player Profile

- **Endpoint**: `statview/mobile/pwhl/player`
- **Description**: View a given player's profile.

**Full URL:**

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

**Full URL:**

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?step=4&sub=0
```

### Daily Report

- **Endpoint**: `download.php`
- **Description**: View the daily report for the league.
- **Parameters**:
    - `client_code` = `pwhl`
    - `file_path` = `daily-report`

**Full URLs:**

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

**Full URL:**

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

**Full URL:**

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

**Full URL:**

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?step=4&sub=4&format=HTML&season_id=5&team=3
```

### Special Reports

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

**Full URL:**

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

**Full URL:**

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

**Full URL:**

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

**Full URL:**

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

**Full URL:**

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

**Full URL:**

```
https://lscluster.hockeytech.com/media/pwhl/pwhl/index.php?format=HTML&season_id=5&step=4&sub=16
```

---

# Notes on API Usage

1. **Authentication**:
    - Firebase API requires both `auth` and `key` parameters.
    - HockeyTech API requires `key` and `client_code` parameters.

2. **PWHL IDs**:
    - Both APIs use numeric season IDs (e.g., `5` for the 2024-2025 season). See [seasons.csv](./data/seasons.csv).
    - Each team has a unique numeric ID (e.g., `3` for MTL). See [teams.csv](./data/teams.csv).
    - Games also have unique numeric IDs used across both API systems.

3. **Error Handling**:
    - The APIs do not consistently return standard HTTP status codes for errors.
    - Check for specific error fields in the JSON response.
