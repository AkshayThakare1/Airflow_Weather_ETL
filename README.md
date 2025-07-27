

```markdown
# 🌦️ Weather Data Pipeline with Apache Airflow

This project automates the process of fetching current weather data using the Open-Meteo API and stores it in a PostgreSQL database. Built with Apache Airflow, it showcases a simple ETL (Extract, Transform, Load) pipeline using the TaskFlow API.

---

## 📁 Project Structure

```

.
├── dags/
│   └── weather\_etl\_pipeline.py    # The DAG that runs the ETL process
├── docker-compose.yaml            # Docker config to run Airflow locally
├── requirements.txt               # Python dependencies for Airflow and providers
└── README.md                      # You're here!

````

---

## 🧠 What It Does

The DAG (`weather_etl_pipeline`) performs the following steps daily:

1. **Extract**: Fetches current weather data for London from the Open-Meteo API using `HttpHook`.
2. **Transform**: Extracts key fields like temperature, wind speed, wind direction, and weather code.
3. **Load**: Inserts the cleaned data into a PostgreSQL table called `weather_data`.

---

## 🔧 Tech Stack

- **Apache Airflow** (v2.9+)
- **PostgreSQL**
- **Open-Meteo API**
- **Python**
- **Docker + Docker Compose**

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/weather-airflow-pipeline.git
cd weather-airflow-pipeline
````

### 2. Start Airflow Locally

Make sure Docker is running, then:

```bash
docker compose up --build
```

This will start the following services:

* **Airflow Webserver** at [localhost:8080](http://localhost:8080)
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


