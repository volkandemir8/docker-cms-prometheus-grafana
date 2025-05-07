# Dockerized CMS with Prometheus and Grafana Monitoring

This project demonstrates a containerized setup for running Joomla CMS instances with MySQL and PostgreSQL databases, while integrating Prometheus and Grafana for monitoring.

## Features

- **MySQL and PostgreSQL Databases**: Two separate Joomla instances, one using MySQL and the other PostgreSQL.
- **Prometheus Monitoring**: Collects metrics from MySQL and PostgreSQL exporters.
- **Grafana Dashboard**: Visualizes the metrics collected by Prometheus.
- **Database Exporters**: Includes MySQL and PostgreSQL exporters for Prometheus.

## Prerequisites

- Docker and Docker Compose installed on your system.

## Setup Instructions

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd docker-cms-prometheus-grafana
    ```

2. Create the `prometheus.yml` configuration file in the project root:
    ```yaml
    global:
      scrape_interval: 15s

    scrape_configs:
      - job_name: 'mysql'
         static_configs:
            - targets: ['mysqld_exporter:9105']

      - job_name: 'postgres'
         static_configs:
            - targets: ['postgres_exporter:9187']
    ```

3. Start the containers:
    ```bash
    docker-compose up -d
    ```

4. Access the services:
    - Joomla (MySQL): [http://localhost:8081](http://localhost:8081)
    - Joomla (PostgreSQL): [http://localhost:8082](http://localhost:8082)
    - Prometheus: [http://localhost:9090](http://localhost:9090)
    - Grafana: [http://localhost:3000](http://localhost:3000)

5. Configure Grafana:
    - Log in with the default credentials (`admin`/`admin`).
    - Add Prometheus as a data source.
    - Import or create dashboards to visualize metrics.

## Volumes

The following Docker volumes are used for persistent storage:
- `mysql_data`: MySQL database data.
- `postgres_data`: PostgreSQL database data.
- `grafana_data`: Grafana configuration and data.
- `joomla1_data`: Joomla instance using MySQL.
- `joomla2_data`: Joomla instance using PostgreSQL.

## Network

All services are connected to a custom Docker network named `monitoring`.

## Notes

- Ensure that the `prometheus.yml` file is correctly configured before starting the containers.
- Modify the environment variables in the `docker-compose.yml` file as needed for your setup.

## Stopping the Containers

To stop and remove the containers, run:
```bash
docker-compose down
```

## License

This project is licensed under the MIT License.  