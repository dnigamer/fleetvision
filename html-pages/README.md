# html-pages

This folder contains the PHP pages for system management, organized into different subdirectories based on functionality.

## `alertas` Folder
Contains pages related to alert management in the system:
- **adicionar.php**: Add a new alert.
- **desativar.php**: Deactivate an existing alert.
- **editar.php**: Edit the details of an alert.
- **enviar.php**: Placeholder for sending alerts (not implemented).
- **lista.php**: List all alerts with detailed information.
- **recentes.php**: Show recent alerts.
- **remover.php**: Remove an alert.

## `camaras` Folder
Contains pages for camera management:
- **adicionar.php**: Add a new camera.
- **contagem.php**: Show the count of people detected by a specific camera.
- **editar.php**: Edit the details of a camera.
- **lista.php**: List all cameras with detailed information.
- **remover.php**: Remove a camera.

## `paragens` Folder
Contains pages for bus stop management:
- **adicionar.php**: Add a new stop.
- **editar.php**: Edit the details of a stop.
- **estado.php**: Get the status of a stop.
- **favoritas.php**: List favorite stops.
- **lista.php**: List all stops with detailed information.
- **lotacao.php**: Get the current capacity of a stop.
- **remover.php**: Remove a stop.

## `relatorios` Folder
Contains pages for report generation:
- **fluxo_passageiros.php**: Report on passenger flow over time.
- **geral.php**: General report on stops.
- **lotacao_media.php**: Report on the average capacity of stops.
- **pico_lotacao.php**: Report on the peak capacity of stops.
- **taxa_alertas.php**: Report on the alert rate by severity.

## `static` Folder
Contains static resources, such as CSS files:
- **css/style.css**: Stylesheet for larger screens.
- **css/style-small.css**: Stylesheet for smaller screens.

## License

MIT License. See the [LICENSE](LICENSE) file for more details.