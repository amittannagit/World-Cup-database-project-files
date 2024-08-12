# World Cup Database

> Welcome to the World Cup Database project!

## Overview

In this project, you will create a database to manage World Cup game data, insert data from a CSV file, and run queries to retrieve specific information. The project is divided into three parts:

1. **Create the Database**: Set up your database structure.
2. **Insert Data**: Populate the database with data from `games.csv`.
3. **Query the Database**: Write queries to retrieve and display specific information.

## Part 1: Create the Database

1. **Log into PostgreSQL**: Start by logging into the PostgreSQL interactive terminal with:
   ```bash
   psql --username=freecodecamp --dbname=postgres
   ```

2. **Create the `worldcup` Database**: Create a new database named `worldcup`.

3. **Connect to the `worldcup` Database**:
   ```bash
   \c worldcup
   ```

4. **Create Tables**:
   - **Teams Table**: Should include `team_id` (SERIAL PRIMARY KEY) and `name` (UNIQUE).
   - **Games Table**: Should include `game_id` (SERIAL PRIMARY KEY), `year` (INT), `round` (VARCHAR), `winner_id` (FOREIGN KEY), `opponent_id` (FOREIGN KEY), `winner_goals` (INT), and `opponent_goals` (INT).

   Ensure all columns have the `NOT NULL` constraint.

   ```sql
   CREATE TABLE teams (
       team_id SERIAL PRIMARY KEY,
       name VARCHAR(255) UNIQUE NOT NULL
   );

   CREATE TABLE games (
       game_id SERIAL PRIMARY KEY,
       year INT NOT NULL,
       round VARCHAR(50) NOT NULL,
       winner_id INT REFERENCES teams(team_id),
       opponent_id INT REFERENCES teams(team_id),
       winner_goals INT NOT NULL,
       opponent_goals INT NOT NULL
   );
   ```

## Part 2: Insert Data

1. **Complete the `insert_data.sh` Script**:
   - This script will read from `games.csv` and insert data into the `teams` and `games` tables.
   - Ensure that each unique team is added to the `teams` table.
   - Insert each row from `games.csv` into the `games` table, using the correct `team_id` values from the `teams` table.

   **Note**: Ensure the script runs efficiently and avoids multiple queries where possible.

   ```bash
   #!/bin/bash

   # Define PSQL variable
   PSQL="psql --username=freecodecamp --dbname=worldcup -t --no-align -c"

   # Clear existing data
   $($PSQL "TRUNCATE TABLE games, teams;")

   # Read data from CSV and insert into database
   # ...
   ```

2. **Check Data Insertion**:
   - After running the script, verify that there are 24 rows in the `teams` table and 32 rows in the `games` table.

## Part 3: Query the Database

1. **Complete the `queries.sh` Script**:
   - This script should include queries to retrieve specific data and match the output with `expected_output.txt`.

   **Example Queries**:
   ```bash
   #!/bin/bash

   PSQL="psql --username=freecodecamp --dbname=worldcup --no-align --tuples-only -c"

   echo -e "\nTotal number of goals in all games from winning teams:"
   echo "$($PSQL "SELECT SUM(winner_goals) FROM games")"

   echo -e "\nTotal number of goals in all games from both teams combined:"
   echo "$($PSQL "SELECT SUM(winner_goals + opponent_goals) FROM games")"

   # Add more queries as needed
   ```

2. **Verify Output**:
   - Ensure that the output of each query matches exactly what is in the `expected_output.txt` file.

## Additional Notes

- **Database Dump**: If you need to save your progress or transfer your database, use the following command:
  ```bash
  pg_dump -cC --inserts -U freecodecamp worldcup > worldcup.sql
  ```

- **Restoring Database**: To rebuild the database from the dump file:
  ```bash
  psql -U postgres < worldcup.sql
  ```

- **Permissions**: Ensure that both `insert_data.sh` and `queries.sh` have executable permissions:
  ```bash
  chmod +x insert_data.sh queries.sh
  ```

## Submission

- Save your progress on freeCodeCamp.org.
- Upload the `worldcup.sql` file, as well as the final versions of `insert_data.sh` and `queries.sh` to a public repository.
- Submit the URL to the repository on freeCodeCamp.org.

