# Eye Excercise App

In this project, you will use a [Gaze Detection Model](https://docs.openvinotoolkit.org/latest/_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html) to estimate the gaze of the user's eyes. This will help us to Get Score based on Eye Gaze of Excercise Video person and User.

You will be using the InferenceEngine API from Intel's OpenVino ToolKit to build the project. The gaze estimation model requires three inputs:

* The head pose
* The left eye image
* The right eye image.

Below Image shows how we detect Eye Gaze, 
![demoVideo](/bin/output_video.gif)

To get these inputs, you will have to use three other OpenVino models:

* [Face Detection](https://docs.openvinotoolkit.org/latest/_models_intel_face_detection_adas_binary_0001_description_face_detection_adas_binary_0001.html)
* [Head Pose Estimation](https://docs.openvinotoolkit.org/latest/_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html)
* [Facial Landmarks Detection](https://docs.openvinotoolkit.org/latest/_models_intel_landmarks_regression_retail_0009_description_landmarks_regression_retail_0009.html)

### The Pipeline:
You will have to coordinate the flow of data from the input, and then amongst the different models and finally to the mouse controller. The flow of data will look like this:

![pipeline](/imgs/pipeline.png)

## Project Set Up and Installation:

Step1: Download below three softwares:
1. Microsoft Visual Studio* with C++ 2019, 2017, or 2015 with MSBuild
2. CMake 3.4 or higher 64-bit
NOTE: If you want to use Microsoft Visual Studio 2019, you are required to install CMake 3.14.
3. Python 3.6.5 64-bit

Step2. Download **[OpenVino Toolkit 2020.1](https://docs.openvinotoolkit.org/latest/index.html)** with all the prerequisites by following this [installation guide](https://docs.openvinotoolkit.org/2020.1/_docs_install_guides_installing_openvino_windows.html)

Step3: Setup OpenVino Toolkit using below command in command prompt
```
cd C:\Program Files (x86)\IntelSWTools\openvino\bin\
setupvars.bat
```

Step4: Configure Model Optimizer using below commnads in command prompt
```
cd C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\model_optimizer\install_prerequisites
install_prerequisites.bat
```

Step5: Varify installation
```
cd C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\demo\
demo_squeezenet_download_convert_run.bat
```
Above command should give output like this image
![optimizer_output](/imgs/image_classification_script_output_win.png)


## Demo:

Step1. Clone the Repository using `git clone https://github.com/bhadreshpsavani/Computer-Pointer-Controller.git`

Step2. Create Virtual Environment using command `python -m venv base` in the command prompt, then activate environment using below command,
```
cd base/Scripts/
activate
```

Step3. install all the dependency using `pip install requirements.txt`.

Step4. Instantiate OpenVino Environment. For windows use below command
```
cd C:\Program Files (x86)\IntelSWTools\openvino\bin\
setupvars.bat
```

Step5. Go back to the project directory `src` folder
```
cd path_of_project_directory
cd src
```

Step6. Run below commands to execute the project
```
python main.py -fd ../intel/face-detection-adas-binary-0001/FP32-INT1/face-detection-adas-binary-0001.xml -lr ../intel/landmarks-regression-retail-0009/FP32-INT8/landmarks-regression-retail-0009.xml -hp ../intel/head-pose-estimation-adas-0001/FP32-INT8/head-pose-estimation-adas-0001.xml -ge ../intel/gaze-estimation-adas-0002/FP32-INT8/gaze-estimation-adas-0002.xml -i cam
```
Command Line Argument Information:
- fd : Specify path of xml file of face detection model
- lr : Specify path of xml file of landmark regression model
- hp : Specify path of xml file of Head Pose Estimation model
- ge : Specify path of xml file of Gaze Estimation model
- i : cam for Webcam
 
## Documentation: 

### Project Structure:

![project_structure](/imgs/project_structure.png)

intel: This folder contains models in IR format downloaded from Openvino Model Zoo

src: This folder contains model files, pipeline file(main.py) and utilities 
* `model.py` is the model class file which has common property of all the other model files. It is inherited by all the other model files 
This folder has 4 model class files, This class files has methods to load model and perform inference.
* `face_detection_model.py`
* `gaze_estimation_model.py`
* `landmark_detection_model.py`
* `head_pose_estimation_model.py`
* `main.py` file used to run complete pipeline of project. It calls has object of all the other class files in the folder
* `input_feeder.py` is utility to load local video or webcam feed

bin: this folder has `demo.mp4` file which used for Eye Excercise Video

### Team:
* [Bhadresh Savani](https://github.com/bhadreshpsavani)
* [Pakeeza](https://github.com/Hotaru29)
* [Erin Song](https://www.linkedin.com/in/erinsong1/)
* [Richa](https://www.linkedin.com/in/richaphd/)
* [Jose Mariscal](https://github.com/jgmarsm) 

### Road Map:
- [x] Create End to End Pipeline to Extract Eye Gaze Coordinates
- [x] Create Pipeline for Getting Eye Gaze Coordinates for Excersice Video
- [x] Create Pipeline and UI for Webcam Video
- [x] Develop Score Computation Logic
- [x] Develop UI for Comuter to View Output and Score
- [ ] Deploy Application to Azure Cloud

