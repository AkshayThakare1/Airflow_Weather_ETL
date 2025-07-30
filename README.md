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

4. Create docker-compose.override.yml (if needed)
Only if you want to override ports or customize your containers.

5. Start the Project
bash
Copy
Edit
astro dev start
🪐 This will start Docker containers with:

Airflow Web UI at localhost:8080

PostgreSQL at localhost:5432 (internal host name used in Airflow)



------------------------
* **PostgreSQL** at `localhost:5432`

### 3. Access Airflow UI

Log in to Airflow:

* **Username:** `admin`
* **Password:** `admin` *(or as defined in your environment variables)*

Trigger the DAG named `weather_etl_pipeline`.

---

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


