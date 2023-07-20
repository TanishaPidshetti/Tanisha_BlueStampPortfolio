# Object Detection with Tenserflow and Raspberry Pi
This project uses an integration of Tenserflow and tflite on Raspberry Pi to detect and label objects. In this project, based on any desired object, the program will capture a picture and move a servo motor to point to a label listing the object's name.  

 | **Engineer**|**School** |**Area of Interest** |**Grade** | 
 |:--:|:--:|:--:|:--:|
 | Tanisha P | Cypress High School | Aerospace Engineering | Incoming Junior

# Picture of Me
<img src="https://user-images.githubusercontent.com/72050310/180516357-11ce3a2c-c6c2-44a1-87a5-e348b9397158.jpg" width="300" height="400"/>


# Project Picture 
<img src= "https://user-images.githubusercontent.com/72050310/180518314-00cac4af-10e9-4404-a8d4-ea1087dc9ce2.jpg" width = "400" height = "200"/>

# Project Video 
<video src="https://user-images.githubusercontent.com/72050310/180522914-b6111730-d223-4188-ae10-3517eb8f7634.mp4" controls="controls" style="max-width: 730px;">
</video>
  
# Final Milestone
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/N-vriJu8_hM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<center>
  
For my final milestone, my goal was to implement changes to the code that would allow me to use the data of the detected object. However, before starting, I had to understand the code better. The program utilized OpenCV, a Python library for computer vision, and tflite, a flexible machine-learning model library. It performed object detection on camera-captured images, visualizing results with red boxes, labels, and confidence markers. Objects below a confidence threshold of 0.3 were ignored. To get a hands-on understanding, I aimed to add a simple command, printing "Found" when the desired object was detected. Once I felt more confident with the code, my next step was to take a picture once the desired object was found. I used flags to ensure all conditions were met to prevent repetition and saved each image to the desktop. I then attempted to connect the servo motor to the Raspberry Pi. Unfortunately, I faced several challenges with servo jitter. I later learned that changing the pin factory would help prevent this issue. I tried several versions of pin factory before finding a combination of a specific pin factory, and using pulses rather than degrees worked better. With everything set, I created a box to hole the setup and make it look more presentable. After facing numerous challenges and enduring various obstacles, I was finally able to successfully modify and create something of what I had learned. 

# Second Milestone
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/S1QEutZ81Ns" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<center>
  
With the Raspberry Pi setup complete, it was time for my second milestone of building the base project. I created a virtual environment to separate installed libraries and packages from my primary terminal background. Once I activated the new virtual environment, I downloaded different libraries to allow OpenCV to process images and videos, the TensorFlow Lite backend, and GUI processing. I faced many challenges during this step, as many of the libraries I needed to download were unavailable, and I had to find replacements. I attempted to approach this project differently when the errors and issues persisted. I installed the TensorFlow Lite runtime directly onto my Raspberry Pi and downloaded the files with the data and code the object detection program would use onto my virtual environment. I faced new issues downloading the setup files but soon figured it out. With all the libraries, discrepancies, and packages set, I ran the program on my Raspberry Pi. A real-time video feed would open up and have red boxes outlining each detected object with the name and a confidence marker. With the base project successful, I was ready for the next milestone. 

# First Milestone
  

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/EvNvRWB8Lvk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<center>
  
My first milestone was setting up the Raspberry Pi hardware and software. With all the parts of the Raspberry Pi present, I assembled the physical components. Since the circuit quickly overheats, I attached heatsinks to the CPU, RAM, USB controller, and fan. In addition, I attached a Raspberry Pi Camera Module 2 due to my project's need for a camera. Once this step was completed, I inputted the SD card and connected the cabling, one to a power source and an HDMI to an external monitor. A raspberry pi interface opened up, and once I completed setting the configurations and updates, it was finally time to move to the next step. However, before I could start, I realized that I needed the Raspberry Pi OS directly downloaded to my SD card. This step would require wiping the SD card, including all my previous efforts, and restarting everything. After resetting the configurations and re-updating, the Raspberry Pi setup was finally completed and ready for the next milestone. 

# Bill of Materials 
Here is a list of everything you need for the project!

| **Item** | **Quantity** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Breadboard | 1 | $2.99/count |https://tinyurl.com/yc8njk2w  |
| Wires | 20 | $0.06/count |https://tinyurl.com/4f9u42mw |
| Arduino | 1 | $27 |https://tinyurl.com/4e8n27yw |
| Speaker/Amplifier | 1 | $11.99 | https://tinyurl.com/wwpmkfcx |
| Accelerometer | 1 | $3.33/count | https://tinyurl.com/5896vvbk |
| Ultrasonic Sensor | 1 | $1.83/count | https://tinyurl.com/3c6zuk3w |
| Soldering Kit | 1 | $19.99 | https://tinyurl.com/3embv5ct |
| Glove | 1 | $5.99 | https://tinyurl.com/myjw8ejd |
| Hot Glue Gun | 1 | $14.99 | https://tinyurl.com/5c53sdv5 |
| Resistors | 4 | $1.04/count | https://tinyurl.com/5yb2psfc |
| Conductive Fabric | 1 | $15.99 |https://tinyurl.com/vr52v38t |


# Schematic 
NOTE: The pins on the Arduino Uno do not represent the actual orientation, it is simply a reference. Please refer to the Ardunino Pinout (and other pinouts) linked below. 

<img src="https://user-images.githubusercontent.com/72050310/180590632-e17755ef-0d13-4bf6-8d67-355a4af92291.png" width="400" height="200"/>


In my project, I used an external VRM for the speaker since the Ardunino can only supply 200mA, the speaker needed more than that. So, the speaker is powered by the external VRM. 

# Pinout/Useful Links 
1. Arduino - https://docs.arduino.cc/hardware/uno-rev3
3. Accelerometer to Arduino - https://howtomechatronics.com/tutorials/arduino/arduino-and-mpu6050-accelerometer-and-gyroscope-tutorial/
4. Ultrasonic to Arduino - https://create.arduino.cc/projecthub/abdularbi17/ultrasonic-sensor-hc-sr04-with-arduino-tutorial-327ff6 
5. Voltage Regulator Module (VRM) - pinout for this is in the product on amazon, you can find the link in the bill of materials. 
