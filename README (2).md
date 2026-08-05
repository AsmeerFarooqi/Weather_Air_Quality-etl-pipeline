# Weather & Air Quality ETL Pipeline

Automated data pipeline that collects, processes, and stores live weather and air quality readings — built to run on its own, every day, without manual intervention.

## What it does

- Connects to the OpenWeather API to pull current weather and air quality readings
- Processes and cleans the raw JSON using Python and Pandas
- Writes the final structured data into Microsoft SQL Server
- Runs automatically on a daily schedule, orchestrated end-to-end with Apache Airflow

## Architecture

![Pipeline architecture](docs/architecture.png)

## Tech stack

| Layer | Tools |
|---|---|
| Language | Python |
| Data processing | Pandas |
| Database | Microsoft SQL Server |
| Orchestration | Apache Airflow |
| API access | Requests, OpenWeather API |
| DB connectivity | PyODBC, SQLAlchemy |

## How the pipeline works

1. **Extract** — pull raw weather and air quality data from the OpenWeather API in JSON format
2. **Transform** — normalize fields, convert units, and handle missing or malformed values
3. **Load** — insert the cleaned records into the `weather_data` and `air_quality_data` tables
4. **Orchestrate** — an Airflow DAG triggers the run daily, manages task order, and retries on failure

## Database schema

### `weather_data`

| Column | Type | Description |
|---|---|---|
| city | varchar | City the reading belongs to |
| temperature_celsius | float | Recorded temperature |
| humidity | int | Relative humidity percentage |
| description | varchar | Short weather condition summary |
| datetime | datetime | Timestamp of the reading |

### `air_quality_data`

| Column | Type | Description |
|---|---|---|
| city | varchar | City the reading belongs to |
| aqi | int | Air Quality Index |
| pm2_5 | float | PM2.5 particulate concentration |
| pm10 | float | PM10 particulate concentration |
| datetime | datetime | Timestamp of the reading |

## Notes

Built as a hands-on exercise in production-style data engineering: separating extract/transform/load into distinct stages, validating incoming API data, designing a clean relational schema, and automating the whole workflow with scheduled, dependency-aware Airflow tasks.
