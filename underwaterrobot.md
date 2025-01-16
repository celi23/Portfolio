---
layout: page
title: Underwater Robot
permalink: /underwaterrobot/
exclude: true
---

The project focuses on creating a underwater robot that can detect depth using sonar. With that data, GPS, and thermistor, the team's goal was to produce a map of the ocean at deployment with its depth and temperature gradient. 

The team first decided on the placement of each of the sensors. In order to measure the temprature gradient, one thermistor is emerged in water and another is supended in the air. For the sonar system, we expected a range of about 20 feet for the seafloor. Hence, the robot had a speaker that transmitted a sine wave down below with a 3D printed cone that directed the sound waves downwards. With that, a microphone needs to be equipted. It is offsetted by about 10cm from the speaker to avoid feedback. With that, a GPS module is attached to the top of the robot on the motherboard, allowing the robot to use locational and path information. 

## Sensor Selection

The team decided on a Murata NXFT15WB473FA2B150 thermistor for the top and the bottom of the robot. This was because of its simple implementation and our predicted temperature ranges. The circuit design of the Murata thermistor is shown below.

<div style="text-align: center">
  <img src="../assets/img/water/thermistor.png" alt="logo" height="300" />
</div>

The Daytona Audio DAEX25W-8 audio exciter was chosen to used as the transmission speaker. This was because it fits in our budget and was previous used in other labs. It was driven by a 5 Watt LM 384 integrated circuit amplifier. A CME-1538-100LB CUI Devices Microphone was used as a microphone that recieves the echoing signal from the speaker. It was chosen because it was a waterproof speaker that is easily accessible. Lastly, the Adafruit ultimate GPS v3 was usedc to provide location to the robot. This was chosen because our previous experience with it. It can update its locatyion at a frequency of 10Hz and interafaces digitally with the Teensy microcontroller.

## Robot Design

### Circuit Design

All sensors interfaced with a Teensy 3.2 microcontroller onboard a costum motherboard designed for the underwater robot. Some parts of the motherboard include an SD card, a GPS module, and a header for the Teensy microcontroller. The Teensy sampled all sensors at a rate of 10Hz and logged the results to the SD-card. Using a 12.6V, 3 cell LiPo battery, two linear voltage regulartors each supplied a 5V rail to the thermistor circuit voltage dividers and operational amplifiers and a 1.8V source to the microphone.

The thermistors were each put into a voltage divider circuit in order to determine the resistance of the thermistors by observing a change in the output voltage. After finding the nominal resistance at standard temperature, the team decided to put in a unity gain buffer to avoid clipping by the Teensy. This also improved the accuracy of the voltage measurements by decoupling the voltage divider impedance from the input impedance. 

The speaker circuit was built following the reference design in the LM384 datasheet, which is shown below.

<div style="text-align: center">
  <img src="../assets/img/water/tx.png" alt="logo" height="300" />
</div>

In the sending end of the sonar system, a MATLAB script was used to generate the pulse. The audio input source was the digital to analog converter (DAC) on the Teensy. 

In the recieving end of the sonar system, a amplifier chain consisting of 3 op-amps was designed to provide up to 100dB of variable gain from the microphone. The bottom of the ocean can be muddy and uneven, so huge amounts of gain is implemented in order to read the signal clearly. The schamatic of recieving end is shown below. 

<div style="text-align: center">
  <img src="../assets/img/water/rx.png" alt="logo" height="300" />
</div>

### Mechanical Design

With the sensors in mind, the team opted for a dual layer PVC robot frame. The top layer of the frame includes the motherboard, GPS module, and a thermistor above water. The top down view shows the positions of those components, shown below.

<div style="text-align: center">
  <img src="../assets/img/water/mechtop.png" alt="logo" height="300" />
</div>

The second layer, which is submerged, has the audio exciter, the microphone, a second thermistor, and two motors about 25 cm below water. The speaker and the microphone are positioned far from the motors to reduce potential noise. The image below shows the side view of the front of the robot. The image on the right shows the housing of the motor.

<div style="text-align: center">
  <img src="../assets/img/water/mechleft.png" alt="logo" height="300" />
</div>

## Results from deployment

Due to a cold joint on the grund header pin on the GPS module, very limited locational data is collected, shown below. However, the location logged closely align with the robot's true location.

<div style="text-align: center">
  <img src="../assets/img/water/log020_pon.png" alt="logo" height="300" />
</div>

Dispite the loss of locational data, some temperature data was retrieved from the deployment. After calibrating the data from voltage to fahrenheit, we discovered the temperature data was unstable. The graph of the data versus time is shown below. 

<div style="text-align: center">
  <img src="../assets/img/water/log009_temp.png" alt="logo" height="300" />
</div>

This was because of the salinity of the salt water has shorted a junction. When out of the salt water, the thermistors works fine. The team dunked the thermistor into beakers of different temperature water on site, and the data shows the thermistor working perfectly, as shown below. Once the thermistor is dunked in water, the temperature changes accordingly. 

<div style="text-align: center">
  <img src="../assets/img/water/log011_temp.png" alt="logo" height="300" />
</div>

The team was unable to determine the depth of the ocean floor due to the errors in the design of the recieving circuit that filted out frequencies of interest. When designing the recieving circuit, the team failed to consider the 0.1uF capacitor included in the analog channel. Hence, the amplification chain had a total voltage attenuation of 50x. Since the output of the amplification chain was limited to a maximum amplitude of 2.5 V, no signal at that frequency could exceed an amplitude of 50 mV, which is small and almost impossible to detect. The sound data during deployment is shown below.

<div style="text-align: center">
  <img src="../assets/img/water/log042_mic.png" alt="logo" height="300" />
</div>

More specific numbers and results are shown [here](https://drive.google.com/file/d/11uuXs4T48eU59VO8Ra9-wTbZR-kKCBl_/view?usp=sharing).

Credits to my teammate: Marcos Ng Carrion, Alec Vercruysse, and Ruby Foxall.