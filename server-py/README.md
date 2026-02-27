# REST API Backend Project - People Counting System

## Introduction

This project implements a RESTful API developed in Python with FastAPI, responsible for managing and providing data for a people counting system at bus stops.

The backend integrates with a MySQL database and allows the management of cameras, stops, alerts, capacity records, and statistical reports.

The API serves as a backend for real-time monitoring, management, and analysis applications of occupancy and alerts, allowing integration with frontend systems, dashboards, or other applications.

## Main Features

- **Camera Management**: Add, list, update, remove, and query camera data and their respective capacity records.
- **Stop Management**: Add, list, update, remove, mark/unmark as favorite, and query stop data.
- **Alert Management**: Add, list, update, remove, activate/deactivate, send, and query alerts, including recent alerts.
- **Reports**: Get reports on passenger flow, average capacity, peak capacity, and alert rate per stop.

## Installation

1. **Prerequisites**:
    - Python 3.8 or higher
    - MySQL Server
    - Install dependencies:
    ```bash
    pip install fastapi uvicorn mysql-connector-python
    ```

2. **Database Configuration**:
    - To configure the database, you need to create a MySQL database and run the SQL script available in the project's root directory named `scriptDB.sql`. This script will create the necessary tables for the API to work.

## Execution
To start the FastAPI server, run the following command in the terminal:

```bash
python main.py
```

The server will be available at `http://localhost:8000`, unless you have configured a different port.

## API Documentation
The interactive API documentation can be accessed at `http://localhost:8000/docs` after starting the server. This documentation allows you to explore the available endpoints, test requests, and view the data models used.

Documentation image:
![API Documentation](assets/openapi.png)

## Available Endpoints

### Cameras

- `GET /api/camaras`  
  Lists all registered cameras.
- `GET /api/camaras/{camera_id}`  
  Queries the data of a specific camera.
- `POST /api/camaras`  
  Adds a new camera.
- `PUT /api/camaras/{camera_id}`  
  Updates the data of a camera.
- `DELETE /api/camaras/{camera_id}`  
  Removes a camera.
- `GET /api/camaras/lotacao`  
  Gets the last registered capacity of all cameras.
- `GET /api/camaras/{camera_id}/lotacao`  
  Lists the capacity history of a camera.
- `POST /api/camaras/lotacao`  
  Registers a new capacity for a camera.
- `POST /api/camaras/{camera_id}/lotacao/{limit}`  
  Registers a new capacity for a camera with a limit.

### Stops

- `GET /api/paragens`  
  Lists all stops.
- `GET /api/paragens/{paragem_id}`  
  Queries the data of a stop.
- `POST /api/paragens`  
  Adds a new stop.
- `PUT /api/paragens/{paragem_id}`  
  Updates the data of a stop.
- `DELETE /api/paragens/{paragem_id}`  
  Removes a stop.
- `GET /api/paragens/favoritas`  
  Lists the stops marked as favorites.
- `PUT /api/paragens/{paragem_id}/favoritas`  
  Marks or unmarks a stop as favorite.
- `GET /api/paragens/{paragem_id}/lotacao`  
  Gets the current capacity of a stop.

### Alerts

- `GET /api/alertas`  
  Lists all alerts.
- `GET /api/alertas/{alerta_id}`  
  Queries the data of an alert.
- `POST /api/alertas`  
  Adds a new alert.
- `PUT /api/alertas/{alerta_id}`  
  Updates the data of an alert.
- `DELETE /api/alertas/{alerta_id}`  
  Removes an alert.
- `PUT /api/alertas/{alerta_id}/desativar`  
  Deactivates (finishes) an alert.
- `PUT /api/alertas/{alerta_id}/ativar`  
  Activates an alert.
- `PUT /api/alertas/{alerta_id}/enviar`  
  (Placeholder) Sends an alert.
- `GET /api/alerta/recentes`  
  Lists recent alerts.

### Reports

- `GET /api/relatorios/fluxopassageiros`  
  Returns the passenger flow (capacity over time) for each stop.
- `GET /api/relatorios/lotacaomedia`  
  Returns the average capacity for each stop.
- `GET /api/relatorios/picolotacao`  
  Returns the peak capacity for each stop.
- `GET /api/relatorios/taxaalertas`  
  Returns the alert rate per stop.

## Usage Example

### Add a new camera

```bash
curl -X POST http://localhost:8080/api/camaras \
  -H "Content-Type: application/json" \
  -d '{"paragem_id":1,"modelo":"Canon EOS","fabricante":"Canon","latitude":41.55,"longitude":-8.42,"data_instalacao":"2025-04-20","estado":"Ativo"}'
```

### Get average capacity report

```bash
curl http://localhost:8080/api/relatorios/lotacaomedia
```

## Database Structure

The database consists of four main tables: `paragens`, `camaras`, `alertas`, and `registo_lotacao`. It also includes several views for reports (recent alerts, average capacity, peak capacity, alert rate, and capacity flow) and a trigger that keeps the capacity updated at each stop after new registrations.

**Tables summary:**
- **paragens**: Bus stop data (name, location, status, capacity, favorite).
- **camaras**: Information about the cameras installed at each stop.
- **alertas**: Record of alerts generated by the system, associated with stops and cameras.
- **registo_lotacao**: People counting history by camera and stop.

**Views and trigger:**
- Views for alert reports, average/peak capacity, alert rate, and passenger flow.
- Trigger to automatically update the stop capacity after a new record.

The complete SQL script can be found in the `scriptDB.sql` file in the project directory.

## License

MIT License. See the [LICENSE](LICENSE) file for more details.
