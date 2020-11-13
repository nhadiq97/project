# AIROBOT
Humanoid Robotic interface/ System Development for simplified control and managment based on intel Architectures

<h2>Overview / Usage</h2>
The project when complete creates and an easily replicatable completely offline robot with extended capabilities of Processing the environment and interacting accordingly. It could easily be used as a receptionist or a welcoming assistant or a home robot or if developed further even a robot that can aid in Hazardous operations.

<h2>Methodology / Approach</h2>
Speech Recognition: Speech to Text conversion on the basis of Baidu Deep speech model using Intel optimized tensorflow and trained with Audiobooks of at least 5000 Books and its text files alongside available open datasets available for speech training including the tedlium, mozilla speech corpus.

Image recognition: Derivative of Imagenet trained with a dataset of 5Million plus images and added gesture recognition capabilities. Using Tensorflow, Open CV.

The project shall primarily Be run on Devcloud to train huge datasets and then the trained model shall be executed on the robot utilizing Intel Processor based boards and Movidius NCS. Thereby considerably reducing the compute requirements and device cost, Power Requirement for the AI element in the robot.

Response system: A Self-developed and trained model to initiate responses and actions from self-learned or Online Responses to Refined and understood Queries.

Sensory Modules: The system utilizes Gyromagnetic domains to Balance the robot and at the same time record the coordinates and movements alongside Recognition of obstacles and mapping the space around 3dimentionally.

Robot Movement: Each degree of freedom and its movements are coupled and synchronized to work using twin Arduino mega boards externally controlled by our compute server(Upsquared board with Movidius)

<h2>Technologies Used</h2>
IOT, Embedded Computing, Movidius Neural Compute Stick, Theano, Tensorflow, OpenCV, Devcloud, Linux, Kinect Sensor, Openvino, DeepSpeech, Linux

<h2>Required hardware</h2>
Movidius Neural Compute stick-4
Realsense camera(or any other webcam)-1
Upsquared Developer board-1(preferably quad core models with atleast 8gb ram and ssd of 128gb)
Microphone (Multimicrophone array recomended)
Speaker- any bluetooth speaker
wifi module.
