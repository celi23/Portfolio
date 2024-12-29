---
layout: page
title: Jacket Indicator
permalink: /jacketindicator/
exclude: true
---

# [See it in action!](https://www.youtube.com/watch?v=NSoUq3j5nXU&ab_channel=CeciliaLi)

In this project, we used an LED matrix to indicate if the user will need a jacket or not. With percise values of resistors, it allows the lights to light up differently as the thermistor attached reaches different temperatures. The circuit diagram is attached below, modeled in FALSTAD.

<div style="text-align: center">
  <img src="../assets/img/LED.jpg" alt="logo" height="300" />
</div>

Above shows the LED matrix simulation. We used 1kOhms resistors so that the first two blue LEDs represent range from about 0 to 10 degrees C, the red LED represents 10 to 15 degrees, the green LED represents 15 to 20 degrees and so on. 

<div style="text-align: center">
  <img src="../assets/img/wheatstone.jpg" alt="logo" height="300" />
  <img src="../assets/img/amp.jpg" alt="logo" height="300" />
</div>

Above on the left shows the wheatstone bridge that connects to the thermistor so we can have the desired voltage output to have appropriate voltage to the LED matrix. This allows voltage output from 0 to 3.37V from it. On the right shows the differential operational amplifier to connect the wheatstone bridge of thermistor to the input of the LEDs. This converets the 0 to 3.37v output to a desired 0 to 5V input for the LEDs. 

<div style="text-align: center">
  <img src="../assets/img/together.jpg" alt="logo" height="400" />
</div>

Above shows the circuit all put together. A resistor value of about 13kOhms, corresponding to about 17 degree Celcius, turns on 4 of the 7 lights. As seen in the video, it works as we expects. Because of time constraints, we were unable to put this breadboarded circuit into a protoboard. 

Credits to my teammate: Brayden Hedrick.