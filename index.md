

# Object Detection with Tenserflow and Raspberry Pi
This project uses an integration of Tenserflow and tflite on Raspberry Pi to detect and label objects. In this project, based on any desired object, the program will capture a picture and move a servo motor to point to a label listing the object's name.  

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Tanisha Pidshetti | Cypress High School | Aerospace Engineering | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)

# Final Milestone
<!--<center> -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/N-vriJu8_hM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<!--<center> -->
  
For my final milestone, my goal was to implement changes to the code that would allow me to use the data of the detected object. However, before starting, I had to understand the code better. The program utilized OpenCV, a Python library for computer vision, and tflite, a flexible machine-learning model library. It performed object detection on camera-captured images, visualizing results with red boxes, labels, and confidence markers. Objects below a confidence threshold of 0.3 were ignored. To get a hands-on understanding, I aimed to add a simple command, printing "Found" when the desired object was detected. Once I felt more confident with the code, my next step was to take a picture once the desired object was found. I used flags to ensure all conditions were met to prevent repetition and saved each image to the desktop. I then attempted to connect the servo motor to the Raspberry Pi. Unfortunately, I faced several challenges with servo jitter. I later learned that changing the pin factory would help prevent this issue. I tried several versions of pin factory before finding a combination of a specific pin factory, and using pulses rather than degrees worked better. With everything set, I created a box to hole the setup and make it look more presentable. After facing numerous challenges and enduring various obstacles, I was finally able to successfully modify and create something of what I had learned. 

# Second Milestone
<!--<center> -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/S1QEutZ81Ns" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<!--<center> -->

  
With the Raspberry Pi setup complete, it was time for my second milestone of building the base project. I created a virtual environment to separate installed libraries and packages from my primary terminal background. Once I activated the new virtual environment, I downloaded different libraries to allow OpenCV to process images and videos, the TensorFlow Lite backend, and GUI processing. I faced many challenges during this step, as many of the libraries I needed to download were unavailable, and I had to find replacements. I attempted to approach this project differently when the errors and issues persisted. I installed the TensorFlow Lite runtime directly onto my Raspberry Pi and downloaded the files with the data and code the object detection program would use onto my virtual environment. I faced new issues downloading the setup files but soon figured it out. With all the libraries, discrepancies, and packages set, I ran the program on my Raspberry Pi. A real-time video feed would open up and have red boxes outlining each detected object with the name and a confidence marker. With the base project successful, I was ready for the next milestone. 

# First Milestone
<!--<center> -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/EvNvRWB8Lvk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<!--<center> -->
  
My first milestone was setting up the Raspberry Pi hardware and software. With all the parts of the Raspberry Pi present, I assembled the physical components. Since the circuit quickly overheats, I attached heatsinks to the CPU, RAM, USB controller, and fan. In addition, I attached a Raspberry Pi Camera Module 2 due to my project's need for a camera. Once this step was completed, I inputted the SD card and connected the cabling, one to a power source and an HDMI to an external monitor. A raspberry pi interface opened up, and once I completed setting the configurations and updates, it was finally time to move to the next step. However, before I could start, I realized that I needed the Raspberry Pi OS directly downloaded to my SD card. This step would require wiping the SD card, including all my previous efforts, and restarting everything. After resetting the configurations and re-updating, the Raspberry Pi setup was finally completed and ready for the next milestone. 

# Code
Detect.py:
```python
# Copyright 2021 The TensorFlow Authors. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#import RPi.GPIO as GPIO

"""Setting the Servo"""

import pigpio
import time

servo = 18

pwm = pigpio.pi()
pwm.set_mode(servo, pigpio.OUTPUT)

pwm.set_PWM_frequency( servo, 50 )
#servo = AngularServo(18, min_pulse_width=0.0006, max_pulse_width=0.0023)

import os

"""Main script to run the object detection routine."""
import argparse
import sys
import time

import cv2
from tflite_support.task import core
from tflite_support.task import processor
from tflite_support.task import vision
import utils

pwm.set_servo_pulsewidth( servo, 500 ) ;

def run(model: str, camera_id: int, width: int, height: int, num_threads: int,
        enable_edgetpu: bool) -> None:
  """Continuously run inference on images acquired from the camera.

  Args:
    model: Name of the TFLite object detection model.
    camera_id: The camera id to be passed to OpenCV.
    width: The width of the frame captured from the camera.
    height: The height of the frame captured from the camera.
    num_threads: The number of CPU threads to run the model.
    enable_edgetpu: True/False whether the model is a EdgeTPU model.
  """

  # Variables to calculate FPS
  counter, fps = 0, 0
  start_time = time.time()

  # Start capturing video input from the camera
  cap = cv2.VideoCapture(camera_id)
  cap.set(cv2.CAP_PROP_FRAME_WIDTH, width)
  cap.set(cv2.CAP_PROP_FRAME_HEIGHT, height)

  # Visualization parameters
  row_size = 20  # pixels
  left_margin = 24  # pixels
  text_color = (0, 0, 255)  # red
  font_size = 1
  font_thickness = 1
  fps_avg_frame_count = 10

  # Initialize the object detection model
  base_options = core.BaseOptions(
      file_name=model, use_coral=enable_edgetpu, num_threads=num_threads)
  detection_options = processor.DetectionOptions(
      max_results=3, score_threshold=0.3)
  options = vision.ObjectDetectorOptions(
      base_options=base_options, detection_options=detection_options)
  detector = vision.ObjectDetector.create_from_options(options)
  
 # output_dir = 'output_images'
 # os.makedirs(output_dir, exist_ok=True)

  # Continuously capture images from the camera and run inference
  capture_image = False
  while cap.isOpened():
    success, image = cap.read()
    if not success:
      sys.exit(
          'ERROR: Unable to read from webcam. Please verify your webcam settings.'
      )
    
    counter += 1
    image = cv2.flip(image, 0)

    # Convert the image from BGR to RGB as required by the TFLite model.
    rgb_image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

    # Create a TensorImage object from the RGB image.
    input_tensor = vision.TensorImage.create_from_array(rgb_image)

    # Run object detection estimation using the model.
    detection_result = detector.detect(input_tensor)

    # Draw keypoints and edges on input image
    image = utils.visualize(image, detection_result)

    # Calculate the FPS
    if counter % fps_avg_frame_count == 0:
      end_time = time.time()
      fps = fps_avg_frame_count / (end_time - start_time)
      start_time = time.time()

    # Show the FPS
    fps_text = 'FPS = {:.1f}'.format(fps)
    text_location = (left_margin, row_size)
    cv2.putText(image, fps_text, text_location, cv2.FONT_HERSHEY_PLAIN,
                font_size, text_color, font_thickness)
        
    #Based on the object, take a picture and move the servo
    for detection in detection_result.detections:
        category = detection.categories[0]
        category_name = category.category_name
        
        
        if category_name == 'orange' and capture_image == False:
            cv2.imwrite('/home/rasberry/Desktop/orange.jpg', image)
            pwm.set_servo_pulsewidth( servo, 1300 ) ;
            time.sleep( 1 )  
            capture_image == True

        if category_name == 'banana' and capture_image == False:
            cv2.imwrite('/home/rasberry/Desktop/banana.jpg', image)
            pwm.set_servo_pulsewidth( servo, 1800 ) ;
            time.sleep( 1 )
            capture_image == True
            
    # Stop the program if the ESC key is pressed.
    if cv2.waitKey(1) == 27:
      break
    cv2.imshow('object_detector', image)

  cap.release()
  cv2.destroyAllWindows()


def main():
  parser = argparse.ArgumentParser(
      formatter_class=argparse.ArgumentDefaultsHelpFormatter)
  parser.add_argument(
      '--model',
      help='Path of the object detection model.',
      required=False,
      default='efficientdet_lite0.tflite')
  parser.add_argument(
      '--cameraId', help='Id of camera.', required=False, type=int, default=0)
  parser.add_argument(
      '--frameWidth',
      help='Width of frame to capture from camera.',
      required=False,
      type=int,
      default=640)
  parser.add_argument(
      '--frameHeight',
      help='Height of frame to capture from camera.',
      required=False,
      type=int,
      default=480)
  parser.add_argument(
      '--numThreads',
      help='Number of CPU threads to run the model.',
      required=False,
      type=int,
      default=4)
  parser.add_argument(
      '--enableEdgeTPU',
      help='Whether to run the model on EdgeTPU.',
      action='store_true',
      required=False,
      default=False)
  args = parser.parse_args()

  run(args.model, int(args.cameraId), args.frameWidth, args.frameHeight,
      int(args.numThreads), bool(args.enableEdgeTPU))


if __name__ == '__main__':
  main()
```
Utils.py:
```python
import cv2
import numpy as np
from tflite_support.task import processor

_MARGIN = 10  # pixels
_ROW_SIZE = 10  # pixels
_FONT_SIZE = 1
_FONT_THICKNESS = 1
_TEXT_COLOR = (0, 0, 255)  # red

flag = False 

def visualize(
    image: np.ndarray,
    detection_result: processor.DetectionResult,
) -> np.ndarray:
  """Draws bounding boxes on the input image and return it.

  Args:
    image: The input RGB image.
    detection_result: The list of all "Detection" entities to be visualize.

  Returns:
    Image with bounding boxes.
  """
  global flag
  for detection in detection_result.detections:
    # Draw bounding_box
    bbox = detection.bounding_box
    start_point = bbox.origin_x, bbox.origin_y
    end_point = bbox.origin_x + bbox.width, bbox.origin_y + bbox.height
    cv2.rectangle(image, start_point, end_point, _TEXT_COLOR, 3)

    # Draw label and score
    category = detection.categories[0]
    category_name = category.category_name
    probability = round(category.score, 2)
    result_text = category_name + ' (' + str(probability) + ')'
    text_location = (_MARGIN + bbox.origin_x,
                     _MARGIN + _ROW_SIZE + bbox.origin_y)
    cv2.putText(image, result_text, text_location, cv2.FONT_HERSHEY_PLAIN,
                _FONT_SIZE, _TEXT_COLOR, _FONT_THICKNESS)


    if category_name == "person" and flag == False:
        print('Found')
        flag = True
        
  return image
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Raspberry Pi | What the item is used for | $Price | <a href="https://www.amazon.com/GeeekPi-Raspberry-Pi-8GB-Kit/dp/B0B5KHJZP9/ref=sr_1_1_sspa?hvadid=570572414387&hvdev=c&hvlocphy=9031057&hvnetw=g&hvqmt=e&hvrand=2442289902254032771&hvtargid=kwd-296166721380&hydadcr=19137_13375058&keywords=how+much+is+a+raspberry+pi&qid=1689775120&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"> Link </a> |
| Raspberry Pi Camera | What the item is used for | $Price | <a href="https://www.amazon.com/Arducam-Megapixels-Sensor-OV5647-Raspberry/dp/B012V1HEP4/ref=sr_1_1_sspa?crid=3F4I9IV6329Y8&keywords=raspberry+pi+camera&qid=1689776668&sprefix=raspberry+pi+camera%2Caps%2C160&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"> Link </a> |
| Wireless Keyboard and Mouse | What the item is used for | $Price | <a href="https://www.amazon.com/Wireless-Keyboard-Cordless-Windows-Computer/dp/B0B1BQNCPR/ref=asc_df_B0B1BQNCPR/?tag=hyprod-20&linkCode=df0&hvadid=615968724865&hvpos=&hvnetw=g&hvrand=10613761028077811130&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9031057&hvtargid=pla-1721006500455&psc=1"> Link </a> |
| Servo | What the item is used for | $Price | <a href="https://www.amazon.com/Sipytoph-Helicopter-Airplane-Walking-Control/dp/B09185SC1W/ref=sr_1_10?crid=3W27277QBTU3Y&keywords=single+SG90+9G+Micro+Servo&qid=1689776859&sprefix=single+sg90+9g+micro+servo%2Caps%2C132&sr=8-10"> Link </a> |
