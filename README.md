# 🏆 Premier Zone App
A Spring Boot REST API for Premier League player statistics, powered by PostgreSQL.
This project includes a CSV file containing the player data so anyone can recreate the database easily.

## 📁 Project Structure

```
src
 └── main
      ├── java/com/pl/premier_zone/...   # Spring Boot source code
      └── resources
           ├── application-example.properties
           └── data/
                └── player_statistic.csv   # your dataset
```

## 📌 Requirements

- Java 17+
- Maven
- PostgreSQL 14+ or higher
- Docker (optional but recommended)

## 📌 1. Environment Setup

Set your PostgreSQL password using an environment variable.

### Mac / Linux:
```
export POSTGRES_PASSWORD=yourpassword
```

### Windows (PowerShell):
```
setx POSTGRES_PASSWORD "yourpassword"
```

## 📌 2. Application Configuration

This repo includes:

```
src/main/resources/application-example.properties
```

Create an actual config file:

```
cp src/main/resources/application-example.properties src/main/resources/application.properties
```

Update values inside it as needed.

## 📌 3. (Optional) Start PostgreSQL Using Docker

If you want to use Docker:

```
docker compose up -d
```

## 📌 4. Database Setup

The project includes a clean CSV file:

```
src/main/resources/data/player_statistic.csv
```

### Create the table:

```
CREATE TABLE player_statistic (
    player_name TEXT PRIMARY KEY,
    nation TEXT,
    position TEXT,
    age INT,
    matches_played INT,
    starts INT,
    minutes_played INT,
    goals INT,
    assists INT,
    penalties_scored INT,
    yellow_cards INT,
    red_cards INT,
    expected_goals DOUBLE PRECISION,
    expected_assists DOUBLE PRECISION,
    team_name TEXT
);
```

### Import the CSV file:

```
\copy player_statistic FROM 'src/main/resources/data/player_statistic.csv' CSV HEADER;
```

## 📌 5. Run the Spring Boot App

Using Maven Wrapper:

```
./mvnw spring-boot:run
```

Or:

```
mvn spring-boot:run
```

## 📌 6. API Endpoints

### Get all players
```
GET /api/v1/player
```

### Filter by team
```
GET /api/v1/player?team=Arsenal
```

### Filter by player name
```
GET /api/v1/player?name=Ramsdale
```

### Filter by position
```
GET /api/v1/player?position=DF
```

### Filter by nation
```
GET /api/v1/player?nation=eng ENG
```

## 📌 7. Git Ignore Policy

The repository includes a `.gitignore` that ensures sensitive data is not committed.

### You DO commit:
- Source code
- `application-example.properties`
- The CSV dataset
- Docker files
- README

### You DO NOT commit:
- `application.properties`
- `.env` files
- Postgres data directory
- `target/`

