---
layout: page
title: Underwater Robot
permalink: /underwaterrobot/
exclude: true
---

# Work in progress 

The project focuses on creating a underwater robot that can detect depth using sonar. With that data, GPS, and thermistor, the team's goal was to produce a map of the ocean at deployment with its depth and temperature gradient. 

The team first decided on the placement of each of the sensors. In order to measure the temprature gradient, one thermistor is emerged in water and another is supended in the air. For the sonar system, we expected a range of about 20 feet for the seafloor. Hence, the robot had a speaker that transmitted a sine wave down below with a 3D printed cone that directed the sound waves downwards. With that, a microphone needs to be equipted. It is offsetted by about 10cm from the speaker to avoid feedback. With that, a GPS module is attached to the top of the robot on the motherboard, allowing the robot to use locational and path information. 

## Sensor Selection

The team decided on a Murata NXFT15WB473FA2B150 thermistor for the top and the bottom of the robot. This was because of its simple implementation and our predicted temperature ranges. The circuit design of the Murata thermistor is shown below.

<div style="text-align: center">
  <img src="../assets/img/LED.jpg" alt="logo" height="300" />
</div>

The Daytona Audio DAEX25W-8 audio exciter was chosen to used as the transmission speaker. This was because it fits in our budget and was previous used in other labs. It was driven by a 5 Watt LM 384 integrated circuit amplifier. A CME-1538-100LB CUI Devices Microphone was used as a microphone that recieves the echoing signal from the speaker. It was chosen because it was a waterproof speaker that is easily accessible. Lastly, the Adafruit ultimate GPS v3 was usedc to provide location to the robot. This was chosen because our previous experience with it. It can update its locatyion at a frequency of 10Hz and interafaces digitally with the Teensy microcontroller.

## Robot Design

### Circuit Design

All sensors interfaced with a Teensy 3.2 microcontroller onboard a costum motherboard designed for the underwater robot. Some parts of the motherboard include an SD card, a GPS module, and a header for the Teensy microcontroller. The Teensy sampled all sensors at a rate of 10Hz and logged the results to the SD-card. Using a 12.6V, 3 cell LiPo battery, two linear voltage regulartors each supplied a 5V rail to the thermistor circuit voltage dividers and operational amplifiers and a 1.8V source to the microphone.

The thermistors were each put into a voltage divider circuit in order to determine the resistance of the thermistors by observing a change in the output voltage. After finding the nominal resistance at standard temperature, the team decided to put in a unity gain buffer to avoid clipping by the Teensy. This also improved the accuracy of the voltage measurements by decoupling the voltage divider impedance from the input impedance. 

The speaker circuit was built following the reference design in the LM384 datasheet, which is shown below.

<div style="text-align: center">
  <img src="../assets/img/LED.jpg" alt="logo" height="300" />
</div>

In the sending end of the sonar system, a MATLAB script was used to generate the pulse. The audio input source was the digital to analog converter (DAC) on the Teensy. 

In the recieving end of the sonar system, a amplifier chain consisting of 3 op-amps was designed to provide up to 100dB of variable gain from the microphone. The bottom of the ocean can be muddy and uneven, so huge amounts of gain is implemented in order to read the signal clearly. The schamatic of recieving end is shown below. 

<div style="text-align: center">
  <img src="../assets/img/LED.jpg" alt="logo" height="300" />
</div>

### Mechanical Design


More specific numbers and results are shown[here](https://drive.google.com/file/d/11uuXs4T48eU59VO8Ra9-wTbZR-kKCBl_/view?usp=sharing).

Credits to my teammate: Marcos Ng Carrion, Alec Vercruysse, and Ruby Foxall.