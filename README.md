<img src="/.logo.svg" alt="logo" width="50"/>

# PWHL API Reference

This document serves as an unofficial reference for the Professional Women's Hockey League (PWHL) APIs. Corrections and suggestions are welcome.

There appear to be two primary sources for PWHL APIs:
1. Firebase API (`leaguestat-b9523.firebaseio.com`) - Used primarily for live game data
2. HockeyTech/LeagueStat API (`lscluster.hockeytech.com`) - Used primarily for historical data and statistics

This document is broken into distinct sections detailing each API.

## Table of Contents

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

### [HockeyTech/LeagueStat API](#hockeytech-api-documentation)
1. [Base URL](#hockeytech-base-url)
2. [League Information](#league-information)
   1. [Standings](#standings)
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

# HockeyTech API Documentation

This section provides documentation for the PWHL HockeyTech API (via LeagueStat), which is primarily used for historical data and statistics.

## HockeyTech Base URL

All endpoints described in this section are relative to the following base URL:
```
https://lscluster.hockeytech.com/feed/
```

Most HockeyTech API endpoints require the following parameters:
```
key=446521baf8c38984&client_code=pwhl
```

## League Information

### Standings

#### Get League Standings

- **Endpoint**: `index.php`
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

- **Endpoint**: `index.php`
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

###### Example using cURL:
```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=players&season=5&team=all&position=skaters&rookies=0&statsType=standard&rosterstatus=undefined&site_id=0&league_id=1&lang=en&division=-1&conference=-1&key=446521baf8c38984&client_code=pwhl&league_id=1&limit=500&sort=points&league_id=1&lang=en&division=-1&conference=-1"
```

#### Get All Goalies

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

###### Example using cURL:
```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=players&season=5&team=all&position=goalies&rookies=0&statsType=standard&rosterstatus=undefined&site_id=0&first=0&limit=500&sort=gaa&league_id=1&lang=en&division=-1&conference=-1&qualified=all&key=446521baf8c38984&client_code=pwhl&league_id=1"
```

#### Get Top Players

- **Endpoint**: `index.php`
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

- **Endpoint**: `index.php`
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

- **Endpoint**: `index.php`
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

- **Endpoint**: `index.php`
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

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve summary information for a specific game.
- **Parameters**:
  - `feed` = `statviewfeed`
  - `view` = `gameSummary`
  - `game_id` = `105` (or specific game ID)
  - `site_id` = `0`
  - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:
```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=gameSummary&game_id=105&key=446521baf8c38984&site_id=0&client_code=pwhl&lang=en"
```

#### Get Play-by-Play

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve play-by-play data for a specific game.
- **Parameters**:
  - `feed` = `statviewfeed`
  - `view` = `gameCenterPlayByPlay`
  - `game_id` = `105` (or specific game ID)
- **Response**: JSON format

###### Example using cURL:
```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=gameCenterPlayByPlay&game_id=105&key=446521baf8c38984&client_code=pwhl"
```

#### Get Game Center Preview

- **Endpoint**: `index.php`
- **Method**: GET
- **Description**: Retrieve preview information for a specific game.
- **Parameters**:
  - `feed` = `statviewfeed`
  - `view` = `gameCenterPreview`
  - `game_id` = `106` (or specific game ID)
  - `lang` = `en`
- **Response**: JSON format

###### Example using cURL:
```bash
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=gameCenterPreview&game_id=106&key=446521baf8c38984&client_code=pwhl&lang=en"
```

### Schedule

#### Get Scorebar

- **Endpoint**: `index.php`
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

- **Endpoint**: `index.php`
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

- **Endpoint**: `index.php`
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
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=bootstrap&season=latest&game_id=&pageName=scorebar&key=446521baf8c38984&client_code=pwhl&site_id=0&league_id=&league_code=&conference=-1&division=-1&lang=en"
```

#### Get Game Summary Bootstrap

- **Endpoint**: `index.php`
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
curl -X GET "https://lscluster.hockeytech.com/feed/index.php?feed=statviewfeed&view=bootstrap&season=null&game_id=&pageName=game-summary&key=446521baf8c38984&client_code=pwhl&site_id=0&league_id=&league_code=&conference=-1&division=-1&lang=en"
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
