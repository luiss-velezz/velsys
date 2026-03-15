# VELSYS Edge Stack

Docker-based edge platform for industrial data acquisition, messaging,
visualization, and orchestration.

This stack deploys the following services:

-   **Mosquitto** -- MQTT broker
-   **Node-RED** -- Low-code automation and integration platform
-   **Grafana** -- Data visualization and dashboards
-   **Portainer** -- Docker container management UI

The stack is designed to run on a **Raspberry Pi or small edge server**.

------------------------------------------------------------------------

# Architecture

Internet / LAN │ ├── MQTT Broker (Mosquitto) ├── Node-RED (logic /
automation) ├── Grafana (dashboards) └── Portainer (container
management)

All services run as Docker containers and are orchestrated with **Docker
Compose**.

------------------------------------------------------------------------

# Requirements

-   Docker \>= 20
-   Docker Compose \>= 2
-   Linux host (tested on Raspberry Pi OS)

Install Docker:

    curl -fsSL https://get.docker.com | sh

Add user to docker group:

    sudo usermod -aG docker $USER

Then reboot or relog.

------------------------------------------------------------------------

# Configuration

Environment variables are defined in `.env`.

Example `.env`:

    TZ=America/Mexico_City

    GRAFANA_PORT=3000
    NODE_RED_PORT=1880
    MOSQUITTO_PORT=1883
    MOSQUITTO_TLS_PORT=8883
    PORTAINER_PORT=9994

------------------------------------------------------------------------

# Deployment

Start the stack:

    docker compose up -d

Stop the stack:

    docker compose down

Check containers:

    docker compose ps

View logs:

    docker compose logs -f

------------------------------------------------------------------------

# Access the Services

  Service     URL
  ----------- -------------------
  Node-RED    http://HOST:1880
  Grafana     http://HOST:3000
  Portainer   https://HOST:9994
  MQTT        mqtt://HOST:1883

Example (local network):

    http://prismo.local:1880
    http://prismo.local:3000
    https://prismo.local:9994

------------------------------------------------------------------------

# Persistent Data

Container data is stored locally in the repository:

    grafana/data
    mosquitto/data
    mosquitto/log
    node-red/data
    portainer/data

These folders are excluded from Git using `.gitignore`.

------------------------------------------------------------------------

# Updating Containers

Pull the latest images:

    docker compose pull

Restart the stack:

    docker compose up -d

------------------------------------------------------------------------

# Backup

Important files to backup:

-   node-red/data/flows.json
-   grafana/data/grafana.db
-   mosquitto/config/mosquitto.conf

Example backup:

    tar -czf velsys-backup.tar.gz node-red grafana mosquitto

------------------------------------------------------------------------

# Repository Structure

    velsys/
    ├── docker-compose.yml
    ├── .env.example
    ├── README.md
    ├── grafana/
    ├── mosquitto/
    ├── node-red/
    └── portainer/

------------------------------------------------------------------------

# Author

VELSYS Industrial Automation Platform

