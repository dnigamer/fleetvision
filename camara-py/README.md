# Integrated Software Development Project - Python Camera
## Group 3 - 2024/25

## Introduction

The project consists of implementing a system for detecting people in images, using computer vision and machine learning techniques to count the number of people present at a given bus stop. From either images or a webcam stream, the system must be able to identify and count the number of people present in the image or stream.

The use of this system will be done by a public transport operator, who will be able to use the information obtained to optimize resource management and improve the efficiency of the service provided.

This project made in Python utilizes certain libraries and machine learning models to perform people detection that are not available in the program indicated for the development of this project (niop Studio). Thus, part of the project was developed outside of niop Studio, using Python and the OpenCV, Ultralytics, and NumPy libraries for integration with an object detection algorithm.

The YOLOv5 model was used for people detection, and the counting algorithm was implemented using image processing and machine learning techniques.

## Installation

Due to the fact that the project was developed outside of niop Studio, it is necessary to install the required libraries to run the project. To do this, you must have Python 3.8 or higher installed on your system to be able to either compile the project or run it.

To install the necessary libraries, run the following command in the terminal:
```bash
pip install -r requirements.txt
```

## Execution

After installing the necessary libraries, it is possible to execute the project. To do this, run the following command in the terminal:
```bash
python main.py
```

Without any arguments passed, the program will automatically take a picture from the webcam and perform people detection on that captured image using a predefined YOLOv5 model. If there is no webcam available, the program will fail due to not having any image to process.

### Arguments

#### --image, -i

The `--image` or `-i` argument allows you to specify the path to an input image. If not provided, the program will use the webcam as the image source.

#### --verbose, -v

The `--verbose` or `-v` argument enables detailed output of the program. This may include additional information about image processing and detection results.

#### --output, -o

The `--output` or `-o` argument allows you to specify the path to save the output image. If not provided, the output image will not be saved.

#### --model, -m

The `--model` or `-m` argument allows you to specify the path to the YOLOv5 model weights file. The default value is `yolov5su.pt`, which is a pre-trained model. If you want to use another model, you must specify the path to the corresponding weights file.

#### --server, -s

The `--server` or `-s` argument enables the execution mode as a FastAPI server. This allows the program to run as a REST API, where it can be called to process images and return the results in JSON format.

#### --camera, -c

The `--camera` or `-c` argument allows you to specify the camera ID to use as the image source. The camera ID is the camera number that can be used to select the camera to use as input image. If not provided, the program will use the system's default camera with ID 0.

#### --help

The `--help` argument displays the program's help, showing all available arguments and their descriptions.

**NOTE:** Reinforcing, if no argument is provided, the program will use the pre-trained `yolov5su.pt` model by default and will only print the results to the console without any other information or output.

## Execution Example

As an example, let's run the program using the camera as the input image and enabling detailed output:
```bash
python main.py --verbose --output /path/to/output_image.jpg
```
This will process the specified image, enable detailed output, and save the output image to the specified path. The program will print the detection results to the console.
```txt
Captured image from camera and saved as 'frame.jpg'.
Using model: yolov5lu.pt
Input image: frame.jpg
Output image: output_image.jpg
Model loaded from yolov5lu.pt.
Number of people detected: 9
Saving output image to 'output_image.jpg'.
```

As the input image, this was the captured image:
![](assets/image.jpg)

And as the output image, this was the processed image:
![](assets/image_out.jpg)

As can be seen, the program was able to detect 9 people in the captured image. The number of people detected does not always correspond to the actual number of people in the image, since the YOLOv5 model can have difficulties detecting people in certain lighting conditions or viewing angles. However, the model is quite accurate and can detect most of the people present in the image.

## Execution Example in REST API mode

To run the project in REST API mode, it is necessary to have fastapi installed. To do this, run the following command in the terminal:
```bash
pip install fastapi
```

After installing fastapi, it is only necessary to run the following command in the terminal to start the server:
```bash
python main.py --server
```

This will start the FastAPI server on port 8000. The server will expose a `/detect` endpoint that can be used to analyze the webcam image whenever it is called. The endpoint will return a JSON with the number of people detected in the captured image, within the following format:
```json
{
    "num_pessoas":0,
    "tempo":327.0,
    "output_path":"...\\camara-py\\output.jpg"
}
```
The `num_pessoas` field indicates the number of people detected in the image, the `tempo` field indicates the time it took to process the image, and the `output_path` field indicates the path to the output image.

## REST API Endpoints
The FastAPI server will expose the following endpoints:

### GET `/detect`
This endpoint will capture an image from the webcam, process it, and return the number of people detected in the image. The time it took to process the image and the path to the output image will also be returned.

### GET `/camaras`
This endpoint will return a list with the IDs of the cameras available in the system. The camera ID is the camera number that can be used to select the camera to use as an input image.

## Compilation to an executable file

To compile the project to an executable file, it is necessary to have PyInstaller installed. To do this, run the following command in the terminal:
```bash
pip install pyinstaller
```

After installing PyInstaller, run the following command in the terminal to compile the project:
```bash
pyinstaller --onefile main.py
```

This will generate an executable file in the `dist` folder with the name `main.exe` (or `main` on Linux). The executable file can be run directly without the need to have Python or the libraries installed.

The executable will work in the same way as the Python script, accepting the same arguments and options. However, it is important to note that the executable may be larger in size due to the inclusion of the necessary libraries.

Another point to take into account is that the executable will not work outside the operating system for which it was compiled. That is, if you compile the project on Windows, the executable will only work on Windows. To compile the project for another operating system, you must use PyInstaller on that operating system.

### Considerations about the executable

The output program may take some time to be generated, about 2 to 3 minutes, depending on the size of the project and the speed of the computer used.

The execution time of the output program is **relatively higher** compared to direct code execution using the `python main.py` command, due to the inclusion of all necessary libraries to run the project. The execution time of the output program may vary depending on the operating system and the computer used.

It is highly recommended to run the project before compiling it to an executable, to ensure that everything is working correctly. Otherwise, the executable may not work as expected.

## License

MIT License. See the [LICENSE](LICENSE) file for more details.