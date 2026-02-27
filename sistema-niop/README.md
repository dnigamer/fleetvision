# sistema-niop

## Introduction
This folder contains the complete code for the system that displays the recorded data from the people counting system database at the stops. This application was developed using the niop low-code tool.

The system consists of an application containing different pages, each with a specific purpose. Below, we provide a brief description of each page and its functionalities.

## Project Execution
To execute the project, you must have niop installed, as well as a MySQL database and a web server (Apache, Nginx, etc.) configured to serve the project's PHP files.

1. **Install niop**: Follow the installation instructions for niop studio and niop HMI.
2. **Configure the database**: Ensure the MySQL database is configured correctly and the necessary tables are created. For information about the database structure, refer to the database creation script included in the project.
3. **Configure the web server**: Configure the web server to point to the folder where the project files are located (e.g., `http://localhost/`).
4. **Run the project**: After ensuring everything is configured correctly, open niop HMI, niop Studio, and start the project. The application should load and display the pages that make up the system.

## Requirements
- **niop**: Low-code/no-code development tool.
- **PHP**: Version 7.4 or higher.
- **MySQL**: Version 5.7 or higher.
- **Web Server**: Apache, Nginx, or another PHP-compatible server.

## Installation

To install the part of the system that loads the PHP pages, follow these steps:
1. **Install XAMPP**: XAMPP is a package that includes Apache, MySQL, and PHP. It can be downloaded from the official XAMPP website (https://www.apachefriends.org/index.html).
2. **Download the project**: Download the project code from the GitHub repository or the location where the code is hosted.
3. **Place the files in the XAMPP folder**: Copy the contents of the project's html-pages folder directly to the XAMPP `htdocs` folder. Normally, this folder is located in `C:\xampp\htdocs` on Windows or `/opt/lampp/htdocs` on Linux.
   - Example: If the project name is `sistema-niop`, the folder structure should be `C:\xampp\htdocs\` or `/opt/lampp/htdocs/` having all subdirectories and project files within that folder.
      ```
      C:\xampp\htdocs\
        ├── alertas
            ├── adicionar.php
            ├── desativar.php
            ├── editar.php
            ├── enviar.php
            ├── lista.php
            ├── recentes.php
            └── remover.php
        ├── camaras
            ├── adicionar.php
            ├── contagem.php
            ├── editar.php
            ├── lista.php
            └── remover.php
        ├── paragens
            ├── adicionar.php
            ├── editar.php
            ├── estado.php
            ├── favoritas.php
            ├── lista.php
            ├── lotacao.php
            └── remover.php
        ├── relatorios
            ├── fluxo_passageiros.php
            ├── geral.php
            ├── lotacao_media.php
            ├── pico_lotacao.php
            └── taxa_alertas.php
        ├── static
            └── css
                ├── style-small.css
                └── style.css
        └── config.php
      ```
4. **Configure XAMPP**: Make sure XAMPP is configured correctly to serve PHP files. Usually, this is already configured by default.
   - Also, check the `config.php` file in the project root to ensure that the database connection settings are correct (username, password, database name).
      ```php
      <?php
      $host = 'server-ip';         // Example: 'localhost' or '127.0.0.1'
      $dbname = 'bd_sistema_niop'; // Database name
      $username = 'user';          // Database username
      $password = 'password';      // Database password
      ...
      ```

4. **Start XAMPP**: Open the XAMPP control panel and start the Apache and MySQL services.
5. **Access the XAMPP server**: Open a web browser and type `http://localhost`, where `project-name` is the name of the folder you copied to the `htdocs` folder (preferably `http://localhost/` since the project is loaded directly in the server root).

When accessing this URL, you should see the contents of the `htdocs` folder, including the project files.

## Project Explanation

Due to the fact that the project is "low-code/no-code", it is not possible to explain the project from lines of code.

This project can contain many lines going back and forth, but the explanation of the project is quite simple, as the project only presents graphical interfaces and does not contain complex operational logic.

The system consists of a graphical interface (HMI) that allows the user to interact with the different functionalities of the system. The system's operational logic is divided into two main parts: the left part and the right part.

Thus, the project code consists of at least 2 main parts:
![sistema-niop](assets/niop.png)

**Left part**: Contains the logic that checks whether the HMI is ONLINE or OFFLINE, and functional, checking if there was any user input, changing the current page.

**Right part**: Contains the page change logic, where each page is an entity that contains the components and logic to perform specific operations (e.g., Cameras, Stops, Alerts, Reports).

## Home Page

The system's home page serves as a central control panel, providing a quick overview of the system's status and access to key features. It contains:

- **Side Menu**: Located on the left, it allows navigating between the different pages of the system, such as:
  - **Cameras**: Management of connected cameras.
  - **Stops**: Information about monitored stops.
  - **Alerts**: Display of recent alerts.
  - **Reports**: Generation and viewing of reports.
  - **Settings**: System adjustments and preferences.

- **System Status**: Displayed in the upper right corner, indicating whether the system is operational (ONLINE) or not (OFFLINE).

- **Recent Alerts**: A central table that lists the most recent alerts, including information such as ID, date, alert description, and severity.

- **Favorite Stops**: A table displaying stops marked as favorites by the user, with information such as name and people count.

- **Welcome Message**: Centered text that welcomes the user.

This page was designed to be intuitive and provide quick access to the most important system information.

Image:
![homepage](assets/homepage.png)

## Cameras

The **Cameras** page allows you to manage the cameras connected to the system. On it, the user can perform the following actions:

- **Add Camera**: Insert a new camera into the system, specifying information such as model, manufacturer, and associated stop.
- **Edit Camera**: Update data for an existing camera.
- **Remove Camera**: Delete a camera from the system.
- **Get Count**: Check the limit of people recorded by a specific camera.

Furthermore, the page displays a table with the list of registered cameras, containing the following information:
- **ID**: Unique camera identifier.
- **Stop**: Stop associated with the camera.
- **Model**: Camera model.
- **Manufacturer**: Camera manufacturer.
- **Installation Date**: Date the camera was installed.
- **Status**: Current status of the camera (Active or Inactive).

This page is designed to facilitate camera management and ensure all information is organized and accessible.

Image:
![camaras](assets/camaras.png)

## Stops

The **Stops** page allows you to manage the stops monitored by the system. On it, the user can perform the following actions:

- **Add Stop**: Insert a new stop into the system, specifying information such as name and location.
- **Edit Stop**: Update data for an existing stop.
- **Remove Stop**: Delete a stop from the system.
- **Get Status**: Consult the current status of a stop (Active or Inactive).
- **Update Capacity**: Manually update the capacity of a stop.

Additionally, the page displays a table with the list of registered stops, containing the following information:
- **ID**: Unique stop identifier.
- **Name**: Stop name.
- **Location**: Stop location.
- **Status**: Current stop status (Active or Inactive).
- **Capacity**: Current number of people at the stop.

This page is designed to facilitate the management of stops and ensure all information is organized and accessible.

Image:
![paragens](assets/paragens.png)

## Alerts

The **Alerts** page allows you to manage the alerts generated by the system. On it, the user can perform the following actions:

- **Add Alert**: Create a new alert in the system, specifying information such as stop, camera, type, and description.
- **Edit Alert**: Update the data of an existing alert.
- **Remove Alert**: Delete an alert from the system.
- **Send Alert**: Notify the responsible parties about a specific alert.
- **Deactivate Alert**: Change the status of an alert to deactivated.

Furthermore, the page displays a table with the list of registered alerts, containing the following information:
- **ID**: Unique alert identifier.
- **Stop**: Stop associated with the alert.
- **Camera**: Camera associated with the alert.
- **Alert Date**: Date the alert was generated.
- **Resolution Date**: Date the alert was resolved (if applicable).
- **Alert Type**: Type of the alert (e.g., Service, Security).
- **Description**: Detailed description of the alert.
- **Severity**: Severity level of the alert.
- **Status**: Current status of the alert (e.g., Pending, Finished).

This page is designed to facilitate the tracking and resolution of problems detected by the system, ensuring that alerts are handled efficiently.

Image:
![alertas](assets/alertas.png)

## Reports

The **Reports** page allows you to generate and view reports based on data collected by the system. On it, the user can perform the following actions:

- **Get Average Capacity**: Calculate the average capacity of the monitored stops.
- **Get Peak Capacity**: Identify the peak capacity at each stop.
- **Get Passenger Flow**: Analyze the passenger flow at different stops.
- **Get Alert Rate**: Calculate the rate of alerts generated in relation to the total number of stops or cameras.

In addition, the page displays a table with the list of stops, containing the following information:
- **ID**: Unique stop identifier.
- **Name**: Stop name.
- **Location**: Stop location.
- **Status**: Current stop status (Active or Inactive).
- **Capacity**: Current number of people at the stop.

This page is designed to provide detailed reports on the system, aiding in decision making and monitoring the performance of monitored stops.

Image:
![relatorios](assets/relatorios.png)

## License

MIT License. See the [LICENSE](LICENSE) file for more details.