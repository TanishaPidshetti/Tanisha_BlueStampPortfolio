# Object Detection with Tenserflow and Raspberry PI
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Tanisha P | Cypress High School | Aerospace Engineering | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For my final milestone, my goal was to implement changes to the code that would allow me to use the data of the detected object. However, before I could start, I had to gain a better understanding of the code. The program utilized OpenCV, a Python library for computer vision, and tflite, a flexible machine learning model library. It performed object detection on camera-captured images, visualizing results with red boxes, labels, and confidence markers. Objects below a confidence threshold of 0.3 were ignored. To get a hands-on understanding, I aimed to add a simple command, printing "Found" when the desired object was detected. Once I felt more confident with the code, my next step was to take a picture once the desired object was found. I used flags to ensure all conditions were met to prevent repition and saved each image to the desktop. I then attempted to connect the servo motor to the Raspberry Pi. Unfortunaly, I faced serveal challenges with servo jitter. I later learned that changing the pin factory would help prevent this issue. I tried several versions of pin factory before finding a combination of a certain pin factory and the use of pulses rather than degrees worked better. Wiht everything set, I created a boc to hole the setup and make it look more presentable. After facing numerous challenges and enduring through various obstacles, I was finally able to succefuly modify and create someting of what I had learned. I



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/HtWDvuXD1FE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

With the Raspberry Pi setup complete, it was time for my second milestone of building the base project. I started with creating a virtual envornment to keep installed libraries adn packages sperate from my main terminal envornment. Once I activated the new virtual envornment, I began to download different libraries to allow OpenCV in proccessing images and videos, the TensorFlow Lite backend, and GUI processing. I faced many challenges during this step as many of the libraries I needed to download was not availble and I had to find replacements. When the errors and issues still persisted, I attempted to approach this projet differently. 
I installed the TenserFlow Lite runtime directly onto my Raspberry Pi and downloaded the files with the data and code the object detection program would use onto my virtual envornonment. I faced new issues with downloading the setup files, however was soon able to figure it out. With all the libraries, disprecenscies, and packages set, I was able to run the program on my Raspberry Pi. A video feed in realtime would open up and have red boxes outline each detected object with the name  as well as a confidence marker. With the base project successful, I was ready for the nect milestone. 


# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZvWyMmIaHKc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone was setting up the Raspbery Pi harware and software. With all the parts of the Raspberry Pi present, I began to assemble the phycial components. Since the circuit easily overheats, I attached heatsinks to the CPU, RAM, and the USB controller as well as a fan. In addition, I attatched a Raspberry Pi Camera Module 2 due to my project's need of a camera. Once this step was completed, I inputted the SD card and connected the cabling, one to a power source and an HDMI to an external monitor. A raspberry pi interface opened up and once I completed setting the configurations and updates, it was finally time to move to the next step. However before I could start, it later came to my attention that I needed the Raspberry Pi OS directly downloaded to my SD card. This step would require wiping the SD card including all my previous steps and restarting everything. After resetting the configurations and reupdating, the Raspberry Pi setup was finally completed and ready for the next milestone. 


# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```python
import os
import pigpio
import time

"""Setting the Servo"""
servo = 18
pwm = pigpio.pi ()
pwm. set_ mode (servo, pigpio.OUTPUT) pwm. set_PWM_ frequency ( servo, 50 ) #servo
= AngularServo (18, min_ pulse _width=0.0006, max_pulse width=0.0023)

""""Main script to run the object detection routine."""
import argparse
import sys
import time

import cv2
from tflite support. task import core
from tflite support.task import processor
from tflite _support.task import vision import utils

pwm. set servo pulsewidth( servo, 500 ) ;
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

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
