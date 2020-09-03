# 🌱 Eye Excercise App🏋️🚴:
Our aim is to make an Exercise Assistant Application which can help to increase effectiveness of Eye Excercise. We Detect eye gaze of user using Computer Vision and Pretrained Machine Learning model. we check it with eye gaze corrdianates of Instructor and show user a live score of Excercise Effectiveness. We also want our Exercise Assistant to be voice enabled to instruct and motivate users for Excercise.

## How we get Eye Gaze Vectors🤩:
![demoVideo](/bin/output_video.gif)

We have used Four Pretrained Machine Learning Models from Intel Openvino Toolkit:

1. [Face Detection](https://docs.openvinotoolkit.org/latest/_models_intel_face_detection_adas_binary_0001_description_face_detection_adas_binary_0001.html): Detects face coordinates from Video or Webcam images
2. [Head Pose Estimation](https://docs.openvinotoolkit.org/latest/_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html): Detects Pose coordinates for Head
3. [Facial Landmarks Detection](https://docs.openvinotoolkit.org/latest/_models_intel_landmarks_regression_retail_0009_description_landmarks_regression_retail_0009.html): Gives coordinates or location for facial landmarks like Eyes, Nose and Mouth
4. [Gaze Detection Model](https://docs.openvinotoolkit.org/latest/_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html): Takes Head Pose Coordinates and Eye Landmark as input and predicts Gaze Vector

### The Pipeline⚙️🧵:
![pipeline](/imgs/pipeline.png)


## How we get Exercise Score🏆🏅:
We compare Eye Gaze Vector of Instructor and User using Cosine Similarity. 
```
>> from scipy.spatial.distance import cosine
>> eye_gaze_instructor = [ 0.62916321,  0.10232677, -0.77875257]
>> eye_gaze_user = [ 0.09647849,  0.03398839, -0.82852501]
>> cosine(eye_gaze_instructor, eye_gaze_user)
0.15561332345537238
```

## Project Set Up and Installation💻:

Step1. Download below three softwares:
1. Microsoft Visual Studio* with C++ 2019, 2017, or 2015 with MSBuild
2. CMake 3.4 or higher 64-bit
NOTE: If you want to use Microsoft Visual Studio 2019, you are required to install CMake 3.14.
3. Python 3.6.5 64-bit

Step2. Download **[OpenVino Toolkit 2020.1](https://docs.openvinotoolkit.org/latest/index.html)** with all the prerequisites by following this [installation guide](https://docs.openvinotoolkit.org/2020.1/_docs_install_guides_installing_openvino_windows.html)

Step3. Setup OpenVino Toolkit using below command in command prompt
```
cd C:\Program Files (x86)\IntelSWTools\openvino\bin\
setupvars.bat
```

Step4. Configure Model Optimizer using below commnads in command prompt
```
cd C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\model_optimizer\install_prerequisites
install_prerequisites.bat
```

Step5. Varify installation
```
cd C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\demo\
demo_squeezenet_download_convert_run.bat
```
Above command should give output like this image
![optimizer_output](/imgs/image_classification_script_output_win.png)


## Demo🔎:

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
 
## Documentation🗞️📚: 

### Project Structure📂:

![project_structure](/imgs/project_structure.png)
**bin**: This folder has `demo.mp4` file which we are using for Eye Excercise Video

**imgs**: It contains images used in this project for documentations and results

**intel**: This folder contains Machine Learning models in IR(Intermediate Representation) format

**src**: This folder contains model files, pipeline file(main.py) and utilities 
* `model.py` is the model class file which has common property of all the other model files. It is inherited by all the other model files 
This folder has 4 model class files, 
This class files has methods to load model and perform inference.
  * `face_detection_model.py`
  * `gaze_estimation_model.py`
  * `landmark_detection_model.py`
  * `head_pose_estimation_model.py`
* `main.py` file used to run complete pipeline of project. It calls has object of all the other class files in the folder
* `input_feeder.py` is utility to load local video or webcam feed

## Team🔥:
* [Bhadresh Savani](https://github.com/bhadreshpsavani)
* [Pakeeza](https://github.com/Hotaru29)
* [Erin Song](https://www.linkedin.com/in/erinsong1/)
* [Richa](https://www.linkedin.com/in/richaphd/)
* [Jose Mariscal](https://github.com/jgmarsm) 

## Road Map✨:
- [x] Create End to End Pipeline to Extract Eye Gaze Coordinates
- [x] Create Pipeline for Getting Eye Gaze Coordinates for Excersice Video
- [x] Create Pipeline and UI for Webcam Video
- [x] Develop Score Computation Logic
- [x] Develop UI for Comuter to View Output and Score
- [ ] Enable App with Voice Assistance
- [ ] Deploy Application to Azure Cloud
- [ ] Create a Mobile App
