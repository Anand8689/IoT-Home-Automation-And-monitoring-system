# IoT Home Automation and Monitoring System
![image alt](https://raw.githubusercontent.com/Anand8689/IoT-Home-Automation-And-monitoring-system/98380f182f38c96788b867e42e601984c997b2ef/Screenshot%20(32).png)
An ESP32 and Blynk-based smart home automation project that allows users to control and monitor appliances remotely using a mobile app.

## Features
- Remote control of home appliances using mobile app
- Real-time sensor monitoring (PIR / IR / Ultrasonic)             
- WiFi-based IoT connectivity using ESP32
- Simple and user-friendly Blynk dashboard

## Components Used
- ESP32 Microcontroller
- Relay Module
- PIR / IR / Ultrasonic Sensors (as applicable)
- Blynk IoT App
- WiFi Connection

## Working Principle
The ESP32 connects to a WiFi network and communicates with the Blynk cloud. The mobile app sends commands to ESP32, which controls relays connected to appliances. Sensors send real-time data back to the app for monitoring.

## Setup Instructions
1. Install Arduino IDE and ESP32 board package
2. Install Blynk library
3. Configure Blynk app and get Auth Token
4. Upload code to ESP32
5. Connect hardware and power on system

## Author
Anand Pandey
