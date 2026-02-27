# Integrated Software Development Project - FleetVision
## Group 3 - 2024/25

## Introduction
This project is developed within the scope of the Integrated Software Development curricular unit of the Telecommunications and Informatics Engineering (LETI) Bachelor's degree at the University of Minho. The objective is to apply the knowledge acquired throughout the course in the development of a technological solution that meets a real need.

The project is carried out in partnership with Transportes Urbanos de Braga (TUB), the company responsible for public transport in the city. Currently, one of the challenges faced by TUB is the lack of accurate data on the capacity of the stops, making it difficult to make decisions to optimize the fleet's operation. Without this information, it becomes more complex to adjust bus supply to real demand, which can result in overcrowding or wasted resources.

To solve this problem, the developed system will allow the automated analysis of stop occupation from CCTV cameras installed at waiting points. Through real-time image processing, it will be possible to estimate the number of passengers present at each stop and provide detailed statistical data to TUB. With this information, the company will be able to make more informed decisions about fleet management, improving service efficiency and ensuring transport that is more appropriate to the city's needs.

## Repository Structure

The repository is organized into multiple directories, each responsible for a component of the system:

### [`camara-niop`](camara-niop/README.md)

Project developed on the NIOP low-code platform. Responsible for capturing images from the cameras installed at the stops, integration with the graphical interface (HMI), and sending the count data to the backend via WebSocket. The configuration is done through the `info.json` file.

### [`camara-py`](camara-py/README.md)

Python implementation for capturing images from the webcam, detecting people using the YOLOv5 (Ultralytics) model, counting passengers, and generating statistics. Uses the OpenCV, Ultralytics, and NumPy libraries. The code is modular, facilitating future adaptations.

### [`server-py`](server-py/README.md)

Backend developed in Python with FastAPI, responsible for receiving data from cameras, managing the MySQL database, and providing a RESTful API for querying and managing data (cameras, stops, alerts, reports). Includes endpoints for all main operations and automatic documentation via OpenAPI.

### [`html-pages`](html-pages/README.md)

A set of PHP pages organized into subdirectories for system management via a web interface. Includes pages for managing alerts, cameras, stops, reports, and static resources (CSS). Must be placed in the `htdocs` folder of XAMPP or an equivalent web server.

### [`sistema-niop`](sistema-niop/README.md)

Main project developed in NIOP, integrating all system functionalities into a graphical application (HMI). Allows viewing and managing cameras, stops, alerts, and reports, communicating with the backend and analyzing the collected data.

### [`scriptDB.sql`](scriptDB.sql)

SQL script for creating the MySQL database necessary for the system to function. Contains the definitions of the tables, views, and stored procedures used by the backend.

## Installation and Execution

### General Requirements

- **niop Studio & HMI** (for NIOP components)
- **Python 3.8+** (for backend and camara-py)
- **MySQL Server** (database)
- **XAMPP/Apache/Nginx** (to serve PHP pages)
- **Python Libraries**: `fastapi`, `uvicorn`, `mysql-connector-python`, `opencv-python`, `ultralytics`, `numpy`

### General Steps

1. **Database**: Run the [`scriptDB.sql`](scriptDB.sql) script to create the necessary tables and views.
2. **Backend**: Configure and run the FastAPI server in [`server-py`](server-py/README.md).
3. **Cameras**: Configure and run the [`camara-niop`](camara-niop/README.md) and/or [`camara-py`](camara-py/README.md) projects as needed.
4. **Web Interface**: Copy the contents of [`html-pages`](html-pages/README.md) to the `htdocs` folder of XAMPP or web server.
5. **NIOP System**: Open and run the project in [`sistema-niop`](sistema-niop/README.md) through niop Studio/HMI.

## Main Features

- **Automatic passenger counting at stops**
- **Management of cameras, stops, and alerts**
- **Statistical reports (average capacity, peak, flow, alert rate)**
- **Intuitive graphical interface (web and HMI)**
- **Documented RESTful API for integration with other systems**

## License

MIT License. See the [LICENSE](LICENSE) file for more details.