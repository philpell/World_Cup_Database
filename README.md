🏆 World Cup Database

A PostgreSQL relational database project built as part of the freeCodeCamp Relational Database Certification.

This project models FIFA World Cup data for the 2014 and 2018 tournaments, including teams, matches, scores, and tournament rounds.

📂 Project Overview

The database contains:

2 tables

24 unique teams

32 matches per tournament (64 total matches)

Proper primary keys, foreign keys, and constraints

Auto-incrementing IDs using PostgreSQL sequences

🗄 Database Structure
1️⃣ teams Table

Stores unique national teams.

Column	Type	Constraints
team_id	integer	Primary Key
name	varchar(50)	Unique, Not Null

Key Features:

Unique constraint on name

Auto-incrementing team_id

24 teams inserted

2️⃣ games Table

Stores match results.

Column	Type	Constraints
game_id	integer	Primary Key
year	integer	Not Null
round	varchar(15)	Not Null
winner_id	integer	FK → teams(team_id)
opponent_id	integer	FK → teams(team_id)
winner_goals	integer	Not Null
opponent_goals	integer	Not Null

Key Features:

Foreign key relationships to teams

Auto-incrementing game_id

64 matches total (2014 & 2018 tournaments)

🔗 Relationships

Each game references two teams:

winner_id

opponent_id

Both reference teams.team_id

This ensures:

No duplicate team entries

Strong relational integrity

No games referencing non-existent teams

📊 Data Included
🏆 Tournaments Covered

2014 FIFA World Cup

2018 FIFA World Cup

👥 Total Teams

24 unique national teams

⚽ Total Matches

64 games:

Final

Third Place

Semi-Final

Quarter-Final

Eighth-Final

🛠 Setup Instructions
1️⃣ Create Database
psql -U postgres


Then run:

CREATE DATABASE worldcup;

2️⃣ Import Database Dump

From your terminal:

psql -U postgres -d worldcup -f worldcup.sql


This will:

Create tables

Create sequences

Insert all data

Add constraints

Configure foreign keys

🔒 Constraints Implemented

Primary Keys:

teams_pkey

games_pkey

Unique Constraint:

teams_name_key

Foreign Keys:

games_winner_id_fkey

games_opponent_id_fkey

These ensure:

No duplicate teams

Referential integrity between games and teams

🧠 Example Queries
Get World Cup Winners by Year
SELECT year, name
FROM games
JOIN teams ON games.winner_id = teams.team_id
WHERE round = 'Final';

Total Goals Scored by Each Team
SELECT name, SUM(winner_goals) AS goals
FROM games
JOIN teams ON games.winner_id = teams.team_id
GROUP BY name;

🎯 Learning Objectives

This project demonstrates:

PostgreSQL database creation

Table relationships

Primary & foreign keys

Sequences & auto-incrementing IDs

Data integrity constraints

Querying relational data

📜 License

This project was created for educational purposes as part of the freeCodeCamp curriculum.
