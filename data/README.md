# PWHL Data Collection

This directory contains raw data files in CSV format for the Professional Women's Hockey League (PWHL). These files are
provided for convenience to users who prefer working with pre-processed data rather than accessing the API directly.

Last full update: April 8, 2025

## Directory Structure

```
data/
├── basic/                  # PWHL-related datasets
│   ├── seasons.csv         # Seasons information
│   ├── league.csv          # League information
│   ├── conferences.csv     # Conferences information
│   ├── divisions.csv       # Divisions information
│   ├── teams.csv           # Teams information
│   ├── standings.csv       # Standings and team statistics information
├── games/                  # Game-related datasets
│   ├── all_games.csv       # Complete list of all PWHL games
│   └── play_by_play/       # All play-by-play events
│       ├── shots.csv       # Play-by-play shot events
│       ├── goals.csv       # Play-by-play goal events
│       ├── penalties.csv   # Play-by-play penalty events
│       └── ...
├── players/                # Player-related datasets
│   ├── all_players.csv     # Complete list of all PWHL players
```

## Data Dictionary

### basic/seasons.csv

- `id` - Unique identifier for the season
- `name` - Full name of the season
- `shortname` - Abbreviated season name
- `career` - Flag indicating if statistics count toward career totals (1 = yes, 0 = no)
- `playoff` - Flag indicating if this is a playoff season (1 = yes, 0 = no)
- `start_date` - Season start date (YYYY-MM-DD)
- `end_date` - Season end date (YYYY-MM-DD)

### basic/league.csv

- `id` - Unique identifier for the league
- `name` - Full league name
- `short_name` - League nickname
- `code` - Four-letter league code
- `logo_url` - URL to the league's logo image

### basic/conferences.csv

- `id` - Unique identifier for the conference
- `name` - Name of the conference
- `league_id` - Identifier for the conference's league

### basic/divisions.csv

- `id` - Unique identifier for the division
- `name` - Name of the division
- `league_id` - Identifier for the division's league
- `conference_id` - Identifier for the division's conference

### basic/teams.csv

- `id` - Unique identifier for the team
- `name` - Full team name
- `nickname` - Team nickname
- `code` - Three-letter team code
- `city` - City the team represents
- `logo_url` - URL to the team's logo image
- `league_id` - Identifier for the team's league
- `conference_id` - Identifier for the team's conference
- `division_id` - Identifier for the team's division

### basic/standings.csv

- `id` - Unique identifier for the standings record
- `season_id` - Season identifier (references seasons table)
- `team_id` - Team identifier (references teams table)
- `division_id` - Division identifier
- `wins` - Total wins
- `losses` - Total losses
- `ties` - Total ties
- `ot_losses` - Overtime losses
- `reg_ot_losses` - Regulation overtime losses
- `reg_losses` - Regulation losses
- `ot_wins` - Overtime wins
- `shootout_wins` - Shootout wins
- `shootout_losses` - Shootout losses
- `regulation_wins` - Regulation wins
- `row` - Regulation/overtime wins (excludes shootout wins)
- `points` - Total points
- `bench_minutes` - Bench penalty minutes
- `penalty_minutes` - Total penalty minutes
- `goals_for` - Goals scored
- `goals_against` - Goals allowed
- `goals_diff` - Goal differential (goals_for - goals_against)
- `power_play_goals` - Power play goals scored
- `power_play_goals_against` - Power play goals allowed
- `shootout_goals` - Shootout goals scored
- `shootout_goals_against` - Shootout goals allowed
- `shootout_attempts` - Shootout attempts taken
- `shootout_attempts_against` - Shootout attempts faced
- `short_handed_goals_for` - Short-handed goals scored
- `short_handed_goals_against` - Short-handed goals allowed
- `percentage` - Points percentage
- `percentage_full` - Full points percentage
- `shootout_games_played` - Games that went to shootout
- `games_played` - Total games played
- `shootout_pct` - Shootout percentage
- `power_play_pct` - Power play percentage
- `shootout_pct_goals_for` - Percentage of shootout goals scored
- `shootout_pct_goals_against` - Percentage of shootout goals allowed
- `penalty_kill_pct` - Penalty kill percentage
- `pim_pg` - Penalty minutes per game
- `power_plays` - Total power play opportunities
- `win_percentage` - Win percentage
- `times_short_handed` - Times team was short-handed
- `shootout_record` - Shootout record (W-L format)
- `home_record` - Home record (W-L-OTL format)
- `visiting_record` - Away record (W-L-OTL format)

### games/all_games.csv

- `id` - Unique identifier for the game
- `season_id` - Season identifier for the game
- `game_number` - Game number in the season
- `date` - Game date (ISO format)
- `home_team` - Home team identifier
- `visiting_team` - Away team identifier
- `home_goal_count` - Number of goals scored by the home team
- `visiting_goal_count` - Number of goals scored by the visiting team
- `periods` - Number of periods played
- `overtime` - Whether overtime was required (1 = yes, 0 = no)
- `shootout` - Whether shootouts were required (1 = yes, 0 = no)
- `status` - Game status (1 = upcoming, 2 = in progress, 3 = final/not official, 4 = final/official)
- `game_status` - Description of game status
- `venue_name` - Game venue
- `venue_location` - Game venue location
- `attendance` - Recorded attendance

### games/play_by_play/blocked_shots.csv

- `id` - Unique identifier for the event
- `event_id` - League-assigned identifier for the event
- `game_id` - Game identifier
- `season_id` - Season identifier
- `player_id` - Player identifier of the shooter
- `goalie_id` - Player identifier of the goalie
- `blocker_id` - Player identifier of the shot blocker
- `team_id` - Team identifier of the shooter
- `blocker_team_id` - Team identifier of the goalie/blocker
- `home` - Whether the shooter player was home (1 = home, 0 = visiting)
- `period` - Period of play of the event
- `time` - Time of the event
- `time_formatted` - Formatted time of the event
- `seconds` - Time of the event in seconds
- `x_location` - X-coordinate of the event (on a scale of 0 to 600)
- `y_location` - Y-coordinate of the event (on a scale of 0 to 300)
- `orientation` - Orientation of the coordinates
- `shot_type` - Identifier representing the type of shot
- `shot_type_description` - Description of the type of shot
- `quality` - Identifier representing the quality of shot
- `shot_quality_description` - Description of the quality of shot

### games/play_by_play/faceoffs.csv

- `id` - Unique identifier for the event
- `game_id` - Game identifier
- `season_id` - Season identifier
- `period` - Period of play of the event
- `time` - Time of the event
- `time_formatted` - Formatted time of the event
- `seconds` - Time of the event in seconds
- `home_player_id` - Identifier of the home player
- `visitor_player_id` - Identifier of the visiting player
- `home_win` - Whether the home player won the faceoff (1 = true, 0 = false)
- `win_team_id` - Team identifier of the player who won the faceoff
- `opponent` - Team identifier of the player who lost the faceoff
- `x_location` - X-coordinate of the event (on a scale of 0 to 600)
- `y_location` - Y-coordinate of the event (on a scale of 0 to 300)
- `location` - League-assigned identifier representing faceoff location (1 to 9)

### games/play_by_play/goalie_changes.csv

- `id` - Unique identifier for the event
- `game_id` - Game identifier
- `season_id` - Season identifier
- `period` - Period of play of the event
- `time` - Time of the event
- `seconds` - Time of the event in seconds
- `team_id` - Identifier of the goalie
- `opponent_team_id` - Identifier of the opposing team
- `goalie_in_id` - Player identifier of the goalie coming in
- `goalie_out_id` - Player identifier of the goalie going out

### games/play_by_play/goals.csv

- `id` - Unique identifier for the event
- `event_id` - Unique numerical league-assigned identifier for the goal
- `game_id` - Game identifier
- `season_id` - Season identifier
- `team_id` - Goal-scoring team identifier
- `opponent_team_id` - Team identifier of the opposing team
- `home` - Whether the scoring team was home (1 = true, 0 = false)
- `goal_player_id` - Player identifier of the goalscorer
- `assist1_player_id` - Player identifier of the first assisting player
- `assist2_player_id` - Player identifier of the second assisting player
- `period` - Period of play of the event
- `time` - Time of the event
- `seconds` - Time of the event in seconds
- `x_location` - X-coordinate of the event (on a scale of 0 to 600)
- `y_location` - Y-coordinate of the event (on a scale of 0 to 300)
- `location_set` - Unsure, league-assigned value
- `power_play` - Whether the goal was scored on a power-play (1 = true, 0 = false)
- `empty_net` - Whether the goal was scored on an empty-net (1 = true, 0 = false)
- `penalty_shot` - Whether the goal was scored on a penalty-shot (1 = true, 0 = false)
- `short_handed` - Whether the goal was scored short-handed (1 = true, 0 = false)
- `insurance_goal` - Whether the goal was an insurance goal (1 = true, 0 = false)
- `game_winning` - Whether the goal was game-winning (1 = true, 0 = false)
- `game_tieing` - Whether the goal was game-tieing (1 = true, 0 = false)
- `scorer_goal_num` - Number of goals scored by the goalscorer this season
- `goal_type` - Description of the type of goal

### games/play_by_play/goals_minus.csv

Players who were on the ice when a goal was scored against their team.

- `id` - Unique identifier for the event
- `goal_id` - Goal identifier
- `game_id` - Game identifier
- `season_id` - Season identifier
- `team_id` - Team identifier
- `player_id` - Identifier of the minus player
- `jersey_number` - Jersey number of the minus player

### games/play_by_play/goals_plus.csv

Players who were on the ice when a goal was scored for their team.

- `id` - Unique identifier for the event
- `goal_id` - Goal identifier
- `game_id` - Game identifier
- `season_id` - Season identifier
- `team_id` - Team identifier
- `player_id` - Identifier of the plus player
- `jersey_number` - Jersey number of the plus player

### games/play_by_play/hits.csv

- `id` - Unique identifier for the event
- `event_id` - Unique numerical league-assigned identifier for the hit
- `game_id` - Game identifier
- `season_id` - Season identifier
- `period` - Period of play of the event
- `time` - Time of the event
- `time_formatted` - Formatted time of the event
- `seconds` - Time of the event in seconds
- `player_id` - Identifier of the player
- `team_id` - Team identifier of the player
- `opponent_team_id` - Team identifier of the opposing team
- `home` - Whether the player's team was home (1 = home, 0 = visiting)
- `x_location` - X-coordinate of the event (on a scale of 0 to 600)
- `y_location` - Y-coordinate of the event (on a scale of 0 to 300)
- `hit_type` - Identifier of the hit type (either 1 or 2; unsure what the values represent)

### games/play_by_play/penalties.csv

- `id` - Unique identifier for the event
- `event_id` - Unique numerical league-assigned identifier for the penalty
- `game_id` - Game identifier
- `season_id` - Season identifier
- `player_id` - Identifier of the player who took the penalty
- `player_served_id` - Identifier of the player who served the penalty
- `team_id` - Identifier of the penalized team
- `opponent_team_id` - Identifier of the opposing team
- `home` - Whether the penalized team was home (1 = home, 0 = visiting)
- `period` - Period of play of the event
- `time_off_formatted` - Formatted time of the event
- `minutes` - Number of penalty minutes
- `minutes_formatted` - Formatted number of penalty minutes
- `bench` - Whether the penalty was a bench penalty (1 = true, 0 = false)
- `penalty_shot` - Whether the team was awarded a penalty shot (1 = true, 0 = false)
- `pp` - Whether the penalty led to a power-play (1 = true, 0 = false)
- `offense` - Number of the offense
- `penalty_class_id` - Identifier of the penalty class (1 = Minor, 2 = Double-Minor, 3 = Major, 4 = Match, 5 =
  Misconduct)
- `penalty_class` - Description of the penalty class
- `lang_penalty_description` - Description of the penalty

### games/play_by_play/shootouts.csv

- `id` - Unique identifier for the event
- `event_id` - Unique numerical league-assigned identifier for the shootout attempt
- `game_id` - Game identifier
- `season_id` - Season identifier
- `player_id` - Identifier of the shooter
- `goalie_id` - Identifier of the goalie
- `team_id` - Team identifier of the shooter
- `opponent_team_id` - Identifier of the opposing team
- `home` - Whether the shooter was home (1 = home, 0 = visiting)
- `shot_order` - Order of the shot
- `goal` - Whether the shootout attempt led to a goal (1 = true, 0 = false)
- `winning_goal` - If a goal was scored, whether it was a game-winning goal (1 = true, 0 = false)
- `seconds` - Starts as zero and increases by one for every shootout attempt

### games/play_by_play/shots.csv

- `id` - Unique identifier for the event
- `event_id` - Unique numerical league-assigned identifier for the shot
- `game_id` - Game identifier
- `season_id` - Season identifier
- `player_id` - Identifier of the shooter
- `goalie_id` - Identifier of the goalie
- `team_id` - Team identifier of the shooter
- `opponent_team_id` - Identifier of the opposing team
- `home` - Whether the shooter was home (1 = home, 0 = visiting)
- `period` - Period of play of the event
- `time` - Time of the event
- `time_formatted` - Formatted time of the event
- `seconds` - Time of the event in seconds
- `x_location` - X-coordinate of the event (on a scale of 0 to 600)
- `y_location` - Y-coordinate of the event (on a scale of 0 to 300)
- `shot_type` - Identifier representing the type of shot
- `shot_type_description` - Description of the type of shot
- `quality` - Identifier representing the quality of the shot
- `shot_quality_description` - Description of the quality of the shot
- `game_goal_id` - Associated goal_id (if the shot led to a goal)

### players/all_players.csv

- `id` - Unique identifier for the player
- `first_name` - Player's first name
- `last_name` - Player's last name
- `team_id` - Current team identifier
- `jersey_number` - Player's jersey number
- `type` - Whether the player is a skater or a goalie
- `position` - Player's primary position
- `position_analysis` - Simplified position for analysis purposes (F, D, G)
- `shoots` - Handedness for shooting (L/R)
- `catches` - Handedness for catching (L/R)
- `birthdate` - Date of birth (YYYY-MM-DD)
- `hometown` - City of origin
- `hometown_div` - Province/state or country of origin
- `nationality` - Player nationality
- `image_url` - URL to the player's image

## Notes on Data Usage

1. All dates are in ISO format (YYYY-MM-DD)
2. All identifiers (IDs) correspond to the official PWHL HockeyTech API IDs
3. Missing or null values are represented as empty strings
4. Boolean values are represented as 1 (true) or 0 (false)
5. Percentage values are stored as decimals (e.g., 0.925 for 92.5%)

## Data Sources

All data is sourced from:

1. HockeyTech/LeagueStat API (`lscluster.hockeytech.com`)
2. Firebase API (`leaguestat-b9523.firebaseio.com`)

Full API documentation is available in the repository's [README.md](../README.md).

## Contributing

Want to help maintain these datasets? Please read our [CONTRIBUTING.md](../CONTRIBUTING.md) file for guidelines on how
to contribute.

## Issues and Corrections

If you notice any issues with the data or have suggestions for improvements, please open an issue in the GitHub
repository.

---

This data is provided under the MIT License. See the [LICENSE](../LICENSE) file for details.
