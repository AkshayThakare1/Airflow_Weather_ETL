# 🌤️ Weather Data ETL Pipeline using Apache Airflow & PostgreSQL

This project automates the process of fetching live weather data from an API, processes it, and stores it in a PostgreSQL database. It is built using **Apache Airflow**, set up locally with the help of the **Astro CLI**.

---

## 📌 What This Project Does

- Fetches current weather data (like temperature, wind speed, etc.) for London
- Processes and organizes the data
- Stores it in a PostgreSQL database
- Automatically runs this flow every day using Airflow
- You can view and query the data live in DBeaver

---

## 🧰 Tools Used

- [Apache Airflow](https://airflow.apache.org/)
- [Astro CLI](https://docs.astronomer.io/astro/cli)
- PostgreSQL
- Docker
- DBeaver (for viewing the database)
- Open-Meteo API (for weather data)

---

## 🚀 Setup Instructions

### 1. Install Astro CLI

Follow [Astro CLI Installation Guide](https://www.astronomer.io/docs/astro/cli/install-cli)

Or simply run:


brew install astro
💡 If brew is not found, you’ll need to install Homebrew.

###  2. Initialize Astro Project

astro dev init
This creates a basic Airflow project structure.

###  3. Add Your DAG
Create a new file inside the dags/ folder:
etlweather.py
Paste your DAG code here. (Full code is available in this repo.)

### 4. Create docker-compose.override.yml (if needed)
Only if you want to override ports or customize your containers.

### 5. Start the Project

astro dev start
🪐 This will start Docker containers with:

Airflow Web UI at localhost:8080

PostgreSQL at localhost:5432 (internal host name used in Airflow)

### 6. Log in to Airflow
Go to: http://localhost:8080
Log in with:

Username: admin

Password: admin

### 7. Set Up Airflow Connections
## 7.1 PostgreSQL Connection:
Go to Admin > Connections > + Add

Conn Id: postgres_default

Conn Type: Postgres

Host: Find this in Docker Desktop > Postgres container > Hostname (e.g., etl-weather_postgres_1)

Port: 5432

Schema: postgres

Login/Password: (leave default or set as per your Docker config)

## 7.2 API Connection:
Conn Id: open_meteo_api

Conn Type: HTTP

Host: https://api.open-meteo.com

### 8. Trigger the DAG
Go to the DAGs page

Turn on the weather_etl_pipeline DAG

Trigger it manually or wait for scheduled run

### 9. Connect PostgreSQL to DBeaver
Open DBeaver and create a new PostgreSQL connection

Host: localhost

Port: 5432

DB: postgres

Username: airflow (or your configured user)

Password: airflow (or your configured password)

You’ll now see the table named weather_data.

### 🔍 Live Weather Data in Action
Once the DAG is triggered, weather data (temperature, windspeed, etc.) is automatically pulled from the Open-Meteo API and added to your PostgreSQL database. You can view this live in DBeaver.

### 📸 Screenshot (Optional)
Add a screenshot of your DAG in Airflow or table in DBeaver here.

---------------------------

## 🧾 PostgreSQL Table Structure

Airflow will create the following table if it doesn’t exist:

```sql
CREATE TABLE weather_data (
    latitude FLOAT,
    longitude FLOAT,
    temperature FLOAT,
    windspeed FLOAT,
    winddirection FLOAT,
    weathercode INT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🌐 API Used

* **Open-Meteo API**

  * Endpoint: `https://api.open-meteo.com/v1/forecast`
  * Parameters used: `latitude`, `longitude`, `current_weather=true`

---

## 📊 Output Sample

An entry in the `weather_data` table looks like:

| Latitude | Longitude | Temperature | Windspeed | Winddirection | Weathercode | Timestamp           |
| -------- | --------- | ----------- | --------- | ------------- | ----------- | ------------------- |
| 51.5074  | -0.1278   | 18.3        | 10.2      | 190           | 1           | 2025-07-25 08:00:00 |

---


