\# Control and Monitoring System for Interconnected Water Tanks



\## Introduction



This project aims to describe the design and implementation of an embedded system for the remote monitoring and control of a network of interconnected water tanks. The proposed system is designed to continuously monitor the water level and operational status of the tanks, enabling efficient management and early detection of potential issues.



\[Water tanks setup.](images/TankConfiguration.png?raw=true "Figure 1”)



The system collects data from an ultrasonic sensor that measures the water level inside the tanks. These measurements are processed locally by a microcontroller, which analyzes the data and evaluates the current operating conditions of the system. Based on this analysis, the system can determine whether the tanks are functioning correctly and detect abnormal conditions such as low or excessive water levels.



\[Scheme of the system](images/SystemScheme.png?raw=true "Figure 2”)



The processed information, including water level measurements and system status indicators, is then transmitted to the Measurify framework through an Application Programming Interface (API) whenever an Internet connection is available. This allows the data to be stored, accessed, and monitored remotely.



Finally, the collected information is presented through a graphical user interface (GUI), which provides a clear and intuitive visualization of the system’s state. This interface enables users to easily interpret the data and monitor the system in real time, supporting more effective supervision and management of the interconnected tank system.



\## Quick Start



\### Control System and Parameters

To try the system presented in this thesis, you'll need two microcontrollers that support Wi-Fi and BLE. The lab experiments were conducted using ESP32-WROOM-32.

The embedded code has different files and headers, including the .ino file. The only file you should change in order to setup the system is "config.h" which is inside a folder called "config".

config.h defines the system parameters, which are listed below:

* SUP\_TRIG\_PIN: pin number of the ultrasonic trigger (sends an ultrasonic signal).
* SUP\_ECHO\_PIN: pin number of the ultrasonic echo (receives the ultrasonic signal reflected on the water surface)
* MEASURE\_NUM: the number of measurements to be made to have a stable reading (calculates the mean between all of the measurements)(higher numbers offer more stability but costs time).
* PUMP\_PIN: the number of th epin connected to the pump (or relay)
* SUP\_SENSOR\_LO: distance between the water surface and the sesnor when the tank is full.
* SUP\_SENSOR\_HI: distance between the bottom of the tank and the sensor (distance between sensor and water when tank is empty).
* MIN\_INF\_TO\_PUMP: the minimum acceptable percentage of the lower tank before pumping.
* SUP\_ACC\_LEVEL: the acceptable percentage of water level in the main tank.
* TIME\_TO\_CHECK: in ms, time between pump function check. Interval for checking whether the pumo is functining correctly.
* TIME\_TO\_UPDATE: in ms, time interval to upload the data to the cloud (Measurify).
* SENSOR\_TOLERANCE: in %, the margin to avoid fault sensor errors.



In case you need to change the SSID, Password, UUID, URL and other stuff for WiFi and BLE, you need to modify the variables in the file gloabalVariables.h and globalVariables.cpp.



One time you finish setting up the previously mentioned parameters, you're ready to mount the microcontroller and sensor on your tanks.



\### Mobile App

A user interface was designed and developped using flutter. If you're and android user you just open the file in VS Code and get the app\_release.apk file which you'll find in the following path:

water\_monitor>build>app>outputs>apk>release



If you're using IOS you'll need a MacOS system to configure and export your application...



The application has 3 pages, accessible from the bottom navigation bar:

* Home Page: displays the percentage and status.
* History Page: displays the variation of the percentage in time (graph), as well as the last date in which the data was updated form the microcontroller.
* Setting Page: (under developement) can include additional options and features.
