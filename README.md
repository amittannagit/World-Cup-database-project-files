```markdown
# World Cup Database Project

This project is designed to demonstrate skills in creating, populating, and querying a PostgreSQL database. The data consists of World Cup game results from the final three rounds since 2014. This `README.md` file provides an overview of how the project was completed, including database creation, data insertion, and query execution.

## Project Overview

The project was completed in three main parts:

1. **Create the Database**:
   - Create the `worldcup` database and necessary tables.
2. **Insert Data**:
   - Populate the database with data from `games.csv`.
3. **Query the Database**:
   - Write SQL queries to extract information from the database and match the provided output specifications.

## Instructions and Steps

### Part 1: Create the Database

1. **Log into PostgreSQL**:
   ```bash
   psql --username=freecodecamp --dbname=postgres
   ```

2. **Create the Database**:
   ```sql
   CREATE DATABASE worldcup;
   ```

3. **Connect to the Database**:
   ```bash
   \c worldcup
   ```

4. **Create the Tables**:
   ```sql
   CREATE TABLE teams (
     team_id SERIAL PRIMARY KEY,
     name VARCHAR(50) UNIQUE NOT NULL
   );

   CREATE TABLE games (
     game_id SERIAL PRIMARY KEY,
     year INT NOT NULL,
     round VARCHAR(50) NOT NULL,
     winner_id INT REFERENCES teams(team_id) NOT NULL,
     opponent_id INT REFERENCES teams(team_id) NOT NULL,
     winner_goals INT NOT NULL,
     opponent_goals INT NOT NULL
   );
   ```

### Part 2: Insert Data

1. **Script to Insert Data (`insert_data.sh`)**:
   - This script processes `games.csv` to populate the `teams` and `games` tables.
   - It inserts unique teams into the `teams` table and then inserts game results into the `games` table.

2. **Run the Insert Data Script**:
   ```bash
   ./insert_data.sh
   ```

### Part 3: Query the Database

1. **Script for Queries (`queries.sh`)**:
   - This script includes SQL queries to fetch various pieces of information from the database.
   - Each query is designed to match the expected output specified in `expected_output.txt`.

2. **Run the Queries Script**:
   ```bash
   ./queries.sh
   ```

### Files Included

- **`worldcup.sql`**: Contains SQL commands to recreate the database schema and insert data.
- **`insert_data.sh`**: Bash script to read `games.csv` and insert data into the database.
- **`queries.sh`**: Bash script containing SQL queries to retrieve data from the database.
- **`games.csv`**: CSV file with data about World Cup games.

### Final Steps

1. **Make Scripts Executable**:
   Ensure the script files have executable permissions:
   ```bash
   chmod +x insert_data.sh queries.sh
   ```

2. **Push to GitHub**:
   - Uploaded the files to a public repository on GitHub.
   - Repository URL: [https://github.com/amittannagit/World-Cup-database-project-files](https://github.com/amittannagit/World-Cup-database-project-files)

### Summary

- Created a PostgreSQL database named `worldcup`.
- Designed and implemented the `teams` and `games` tables.
- Developed and ran a script to populate the database with data from `games.csv`.
- Completed a set of queries to extract specific information from the database and verified against expected outputs.

This project showcases skills in database design, data manipulation, and SQL query formulation.
```

