# Integrated Software Development Project - NIOP Camera
## Group 3 - 2024/25

## Introduction

The project consists of implementing a system for detecting people in images, using computer vision and machine learning techniques to count the number of people present at a given bus stop. From either images or a webcam stream, the system must be able to identify and count the number of people present in the image or stream.

The use of this system will be done by a public transport operator, who will be able to use the information obtained to optimize resource management and improve the efficiency of the service provided.

This part of the project done on the NIOP low-code platform aims to create an application for capturing and processing images captured by a camera installed at a bus stop to count passengers. This project integrates side-by-side with the camara-py project, which is responsible for processing an image or video stream and counting the number of passengers in the image.

The project done here in NIOP serves mainly to receive this information and send it to a server using WebSocket.

## Installation

Due to the fact that the project was developed using the NIOP platform, it is only necessary to download the project and open it on the NIOP platform. To do this, you must have NIOP studio installed on your system and have a basic understanding of how to use the NIOP platform. As well as NIOP studio, it is necessary to have NIOP HMI installed on your system. NIOP HMI is the platform that allows you to run GUIs created on the NIOP platform.

Since the NIOP platform works in a client-server way to run the project, it is necessary to have the NIOP server running to be able to execute the project. To do this, it is necessary to start the NIOP server (niop Engine) and then open the project on the NIOP platform. Thus, by running the following command in the terminal, the NIOP server will start:
```bash
& "C:\Program Files\Neadvance\niop Engine\niopEngine.exe" 0.0.0.0 8091 2
```
After the NIOP server is running, you can open the project on the NIOP platform, click publish, then click publish workflow and then click publish. After that, the project will run and will be available to be used.

## Execution

Because the project was designed to be "standalone", it is only necessary to configure some variables in a configuration file. To do this, you need to open the `info.json` file and configure the variables according to your system. The variables that should be configured are the following:
```json
{
    "identificador": 5,
    "server_ip": "https://backend.dnigamer.xyz",
    "tempo_captura": 10
}
```
The variables that must be configured are the following:
- `identificador`: The camera identifier. The default value is a randomly generated number. This number is used to identify the camera in the application. If the number is not unique in relation to another camera in the system, the project will have problems in the backend that processes the passenger counts.
- `server_ip`: The IP address of the server that will receive the information. This IP address must be the address of the backend server that will receive the information sent by the application, such as stop capacity data, among others. The default value is `https://backend.dnigamer.xyz`, and should be changed to the address of your server.
- `tempo_captura`: The period of time in seconds that the camera will capture the image. This number means how often the camera will capture a new image. The default value is 10 seconds, but it can be changed to whatever value you want. The minimum value is 1 second.

**NOTE:** The IP address (`server_ip`) must be the address of the server running the `server-py` backend, a RESTful server that receives the information sent by the application.

### Integrated camara-niop GUI
As a new version of the project, a GUI integrated into the camara-niop project was added. This GUI allows the user to see the capture status, the captured image, and the number of people detected in the image. The GUI is updated in real-time and allows the user to see the capture status and the number of people detected in the image.

![camara-niop](assets/gui-camara.png)

#### How to analyze the GUI
The GUI is divided into several sections, the captured image section, the capture information section, and the capture status section.

The captured image section shows the image captured by the camera, the capture information section shows the number of people detected in the image, as well as the camera ID and the date and time of the last capture.

The capture status section shows the time it took to capture the image and the time interval between captures.

## Project Explanation

Due to the fact that the project is "low-code/no-code", it is not possible to explain the project from lines of code.

Thus, the project is divided into several parts that are explained below:
![camara-niop](assets/projeto.png)

### Legend
#### 1. Initial Checks

In this section of the program, the algorithm will check if both the `info.json` file and the HMI exist to be able to show the program GUI. If the `info.json` file does not exist, the algorithm will automatically create the file with the default values.

If the HMI does not exist, the algorithm will continue running the program without showing the GUI, but will continue to work in the background.

#### 2. Creation of variables and the info.json file

In this step, the project will get the settings from the `info.json` file and will save the variables in variables that will be used in the project.

If the `info.json` file does not exist or is not configured correctly, the project will fail and will not work. Thus, it is necessary to have the `info.json` file correctly configured for the project to work.

As a way to prevent errors, the application will automatically enter some default values if the `info.json` file is empty.

#### 3. Generation of unique camera identifier

This section of the project performs some bitwise operations to generate a unique identifier for the camera. The identifier is generated from 4 random numbers, which then undergo bitwise operations to generate a unique number.

This number is used to identify the camera in the database as being unique.

#### 4. Checking if a camera is available

This section of the project checks if a camera is available by connecting to any first available camera.

This part of the project serves primarily to ensure that the rest of the project works correctly, since the camara-py project will use the camera to capture the image and process it.

If no camera is available, the project will fail and will not work. Thus, it is necessary to have a camera (webcam via USB for example) available for the project to work correctly.

#### 5. GET call to camera-py

In this section of the project, the algorithm will make a GET call to the camara-py project to capture the image. The camara-py project is responsible for capturing the image and processing it using a machine learning model to count the number of people in the image.

Some error checking is also done here, such as if the GET call fails. If the GET call fails, the project will fail and will not work. Thus, it is necessary to ensure that the camara-py project is running and that the GET call works correctly.

#### 6. Processing of received data

In this section of the project, the project will send the information to a backend previously configured in the `info.json` file. The project will send the information using the `/api/camaras/{camera_id}/lotacao` endpoint and a POST call.

The body of the message must be a JSON with the following structure:
```json
{
    "people_count": 9,
    "timestamp": "1744818115"
}
```

The fields that must be filled in are the following:
- `people_count`: The number of people detected in the image. This number is the number of people who were detected in the captured image.
- `timestamp`: The image timestamp. Made using Unix epoch, this number is the timestamp of when the system captured the image or executed camera-py.

#### 7. Sending data to the server
In this section of the project, the algorithm will send the data to the server using a POST call. The project will send the information using the `/api/camaras/{camera_id}/lotacao` endpoint and a POST call.

#### 8. Loop to capture the image from time to time

In this last section of the project, the application will wait for the time configured in the `info.json` file and will capture the image periodically. The project will continue to run until the user stops it manually or the NIOP server is stopped.

## Final warnings

**NOTE:** Since we only have access to the trial version of NIOP, the application will only run for 180 minutes. After that time, the application will automatically stop and will not work. If this happens, you need to redeploy the workflow for the application to work again.

## License

MIT License. See the [LICENSE](LICENSE) file for more details.