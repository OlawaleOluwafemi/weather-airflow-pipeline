# Weather Airflow Pipeline

A robust data pipeline for collecting, processing, and analyzing weather data using Apache Airflow for orchestration and automation.

## Overview

This project implements an end-to-end weather data pipeline that:
- Fetches weather data from external APIs
- Processes and transforms raw weather data
- Stores data in a scalable format
- Orchestrates all workflows using Apache Airflow
- Provides automated scheduling and monitoring

## Tech Stack
- Airflow (ETL Orchestration)
- PostgreSQL (Data Warehouse)
- Docker Compose (Containerized Infra)
- Metabase (Visualization)
- pgAdmin (DB GUI)

## Features

- **Automated Data Collection**: Scheduled DAGs for continuous weather data ingestion
- **Data Processing**: Transform and clean raw weather data
- **Scalable Architecture**: Designed to handle multiple data sources
- **Monitoring & Alerts**: Built-in error handling and notification system
- **Reproducible Workflows**: Version-controlled pipeline definitions

## Prerequisites

- Python 3.8+
- Apache Airflow 2.0+
- pip or conda

## Installation

1. Clone the repository:
```bash
git clone https://github.com/OlawaleOluwafemi/weather-airflow-pipeline.git
cd weather-airflow-pipeline
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Initialize Airflow database:
```bash
airflow db init
```

5. Create an Airflow user:
```bash
airflow users create \
    --username admin \
    --firstname Admin \
    --lastname User \
    --role Admin \
    --email admin@example.com
```

## Usage

1. Start the Airflow webserver:
```bash
airflow webserver --port 8080
```

2. In another terminal, start the Airflow scheduler:
```bash
airflow scheduler
```

3. Access the Airflow UI at `http://localhost:8080`

## Project Structure

```
weather-airflow-pipeline/
├── dags/                    # Airflow DAG definitions
├── plugins/                 # Custom Airflow plugins
├── config/                  # Configuration files
├── tests/                   # Test suite
├── requirements.txt         # Python dependencies
└── README.md               # This file
```

## Configuration

Update configuration in `config/` directory or via Airflow environment variables.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is open source and available under the MIT License.

## Support

For issues or questions, please open an issue on the [GitHub Issues](https://github.com/OlawaleOluwafemi/weather-airflow-pipeline/issues) page.

## Acknowledgments

- Apache Airflow documentation and community
- Weather data API providers
