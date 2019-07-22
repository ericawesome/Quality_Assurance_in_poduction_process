# Quality Assurance in poduction processes (AZURE IOT)


The goal of my final project at the SPICED Academy was to enable continuous learning of a quality measurement system through a holistic process and thus to automatically improve the precision of the measurement system. The solution is based on a Raspberry Pi and a camera to which I deployed a deep learning functionality that allows the object classification to be predicted directly on the edge device in near real-time.

-----

**BUSINESS PROBLEM**

For production companies, the quality of their products is decisive for their business success. While cameras and other sensors try to detect potential defects in the manufacturing process, these quality measurement systems have a high rate of detecting potential defects so that no defect is missed. Operators then review these detected defects but do not train the quality systems with their findings to become even more accurate over time.

------

**SOLUTION**

**1. Concept**

The concept of my solution that I developed will be explained in this section and can be illustrated as following:
![image](https://user-images.githubusercontent.com/48921737/61647137-fbc73680-acac-11e9-91c0-01f9a2fe8d70.png)

The idea is to collect those products with defects that have been detected by the camera. As part of the quality control, the employee responsible for the inspection labels the products again according to their condition. A trade-off in production quality control is that the quality sensory should never classify products as correct that actually have a quality problem (false negative classifications). By establishing these high quality standards, the accuracy of the underlying classification model is low as more potential defects are identified that are actually not. 

With the re-labeled images, the underlying model (in my case a neural net) can be re-trained in the cloud. The accuracy of the new model is then compared with that of the existing model. If the re-trained model has a better accuracy, the model will be deployed on the IoT-Edge device. Continuous learning is then integrated into the production process and can be applied to any process where products are processed.

**2. Architecture**

For my final project I set up a Microsoft Azure account that included 200$ for their services. The architecture is displayed in the following picture: 
<p align="center">
  ![image](https://user-images.githubusercontent.com/48921737/61646886-65931080-acac-11e9-8e55-5637252b1c9d.png)
</p>

(in accordance with on an existing Microsoft project: https://github.com/Azure-Samples/Custom-vision-service-iot-edge-raspberry-pi)


Hardware used for the camera capture (IoT Edge device):
* Raspberry pi 3b+
* Camera B - 1080p

Development machine
* MacBook Pro (2017, 2,3 GHz Intel Core i5)
* Visual Studio Code (with Azure-, Python-, Docker-extension)

Azure Cloud
* IoT-Hub for a wireless bidirectional communication to the IoT device to track and send messages 
* Container registry for deploying the developed modules as docker container to the edge device
* Cognitive Service - Custom Vision AI as the image classifier module that was deployed to and used on the IoT device 
* Cloud Storage to store the data received from the edge for a later training

**3. Image Classification with Custom Vision**

Microsoft Azure offers a cognitive service called "Custom Vision" for rapid prototyping, e.g. when real-time image recognition shall be applied to edge devices with low computing power. For the training I took 3 different objects with 50 images per label. A short test can be performed before the modules will be deployed to the Edge device (see following graphic):
* Waffel with strawberries and cream
* Small cake
* Cupcakes
![image](https://user-images.githubusercontent.com/48921737/61669727-62fede00-ace1-11e9-8cbf-f82930093175.png)

At this point you need to take into account that the service Custom Vision is not optimal for detecting subtle differences and was therefore only used to provide the proof of concept!


**4. Deployment to the IoT Edge device**

To set up everything I used as a test the Simulated Temperature Sensor that is available on the Azure Marketplace.
https://azuremarketplace.microsoft.com/en/marketplace/apps/microsoft.edge-simulated-temperature-sensor-ga?tab=Overview
After the modules had been deployed and the services were correctly linked together, the edge device provided successfully simulated messages to the IoT-Hub and displayed on my MacBook. I replaced the simulation temperature module with a fruit detection classifier and started Monitoring Built-in Event Endpoint (communication Device2Cloud):
![image](https://user-images.githubusercontent.com/48921737/61647485-b820fc80-acad-11e9-8f19-c57d66d92160.png)

-----

**OUTLOOK**

As the final project of my Data Science course I delved deeply into the topic of IoT and therefore into Cloud and Edge Computing. I got to know the MS Azure IoT platform and set up containers for deployment, which I later used on an IoT device like the Raspberry Pi. The camera's functionality was enabled and even the image classification on the Edge device worked and delivered the results as telemetric data to the cloud. The project was completely self-directed and completed in about 80 hours. More detailed technical documentation can be provided on request.

-----
