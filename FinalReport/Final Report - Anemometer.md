Weather Anemometer Report

By Joshua Schmidt, Lorie Rosado, and Angelina Contreras

May 3, 2018

E-122-S Engineering Design II

Group 3

*I pledge my honor that I have abided by the Stevens Honor System.*

X_____________________Lorie Rosado______________________

______________________Angelina Contreras_______________________

_____________________Joshua Schmidt______________________

[[TOC]]

# Abstract

In Engineering Design II, students are expected to design, build, and code a weather station that is able to collect data such as wind speed, temperature, and humidity. This report goes over how the team planned and executed their ideas in order to meet the requirements of Engineering Design II. This includes the mechanical design, electrical wiring design, software design, as well as the trials and tribulations faced while making this design as efficient as possible. In conclusion, this report encompasses the group’s efforts and creative ability to build a weather station. 

# Table of Contents

[[TOC]]

# Discussion

## Requirements

	This project focuses on the creation of a field-ready weather station. The weather station is to be equipped with temperature, humidity, and wind speed sensors. The wind speed sensor, anemometer, which is designed by the students should read between 5-25 miles per hour, within a ± 1 mph accuracy. The temperature sensor should read between  0 and 110 °F within a ± 4 °F accuracy. Lastly, the humidity sensor should read between 20 and 80 % within a ± 5 % accuracy.

This weather station must be operable for at least seven days, and fit into a 12" (304.8 mm) x 12” x 12” envelope including the 4” dia x 6” tall PVC pipe where all components that need to be protected from the elements are contained. Using LabView as a graphical user interface (GUI), the following data will be neatly recorded:

* Time interval selection

* Time history of wind speeds, humidity, and temperature (instantaneous and historical)

* High and low values for selected time periods

Besides this, the weather station must be easily maintainable and able to withstand the following environmental conditions:

* Temperature range between -10  and 120 °F

* Wind gusts of up to 50 mph

* Include a picture of the entire thing outside

* Picture of our Labview 

## System Design (ANG will do this)

1. Write a detailed report with block  diagrams detailing the functionality of each subsystem. Use a top-down approach (system, subsystem, component) to describe mechanical, electrical and software components. Identify all connections and interfaces (mechanical, electrical, and data) 

1. Discuss the overall evolution of your system design. Discuss the steps taken and the results obtained. Much of this information can be found in the various submissions you generated during the course of the semester.

2. Provide details of your final design. Include both a system block diagram showing the various major system components and the interface between those components.

* Include picture of ???

## Mechanical Design (LORIE will do this)

A completed SolidWorks model of the assembly and all parts  (submit as Zip file)  with appropriate part numbering. Follow a part file naming protocol that identifies your section, team number, and the part number. Eg. E122M_5_M555-2.sldprt indicating section M, team 5 with mechanical part number M555-2. 

    1. Bill of Materials: Include Quantities and Associated costs (if applicable).

    2. Show exploded view and views of components in the Appendix. 

*   Provide the details of your system’s mechanical design. What materials were used? What were the major components and how were they produced? Include CAD drawings for any components that were 3D printed or laser cut.

* Include picture of previous designs, find them submitted 

* Include picture of final design

* Include key parts of final design

    * All the brackets and shit

* Explain how we didn’t need the PVC pipe

## Electrical and Wiring Design

### Overview

When deciding the electrical and wiring design, the team focused on creating a system that is scalable and includes the features required for this project, while also providing the ability to complete remote data analysis and analytics. At the core of the system is the Wemos D1 R2 development board, which completes the initial data acquisition from the integrated sensors of the weather station. The sensors themselves are the next entity, and the BMP-180 and DHT-22 were used to gather the necessary weather data. Additionally, a rotary encoder was used for the wind-speed anemometer apparatus. A raspberry pi was responsible for the main data collection and processing, and an off-the-grid system provided power to the whole apparatus. This system ensures that sensors can easily be attached to the wemos and integrated into the weather station, without much modification to the code or circuits. Additionally, the system can be run indefinitely because it is reliant on a solar panel for power. Therefore, this approach was arguably the best for this project, as it enables the weather station to be utilized in many different ways in various situations.

### Wemos D1 R2

#### ESP8266

The Wemos D1 R2 is based on the ESP8266 chip, which is a low-cost wifi microchip and microcontroller produced by Shanghai-based manufacturer, Espressif Systems. It has a 32-bit processor running at 80 MHz with 32 KiB of RAM, 32 KiB of cache, 80 KiB of user data RAM, and 16 KiB of system data RAM. The processor is a Tensilica L106 32-bit RISC microprocessor. The datasheets for this microchip, in addition to the general schematic of the ESP8266, can be found here: [https://goo.gl/gqzxCk](https://goo.gl/gqzxCk), [http://bit.ly/ESP8266EX](http://bit.ly/ESP8266EX). The ESP8266 Technical reference, instruction set, and command examples can be found here: [http://bit.ly/ESP8266-TechRef](http://bit.ly/ESP8266-TechRef), [http://bit.ly/ESP8266-AT-Insts](http://bit.ly/ESP8266-AT-Insts), [http://bit.ly/ESP8266-AT-CmdEx](http://bit.ly/ESP8266-AT-CmdEx).

#### Wemos

Wemos is a small company based out of Shenzhen, China, and creates the Wemos D1 R2 in addition to the D1 mini, D1 mini pro, D1 mini lite, and others. These boards are primarily based on the same processor - the ESP8266EX. For more information on the company go to [https://www.wemos.cc/](https://www.wemos.cc/).

#### D1 R2

The Wemos D1 R2, is a wifi capable microcontroller-based development board based on the ESP8266EX, in the form of an Arduino UNO. It can be programmed via the Arduino IDE, as it was in this project, and features an on-board switching power supply that can take from 5 - 12 V. In this case the input power was 5V. It is a 3.3V device, so only sensors with 3.3V logic work, unless a logic-level converter is used.

Wemos D1 R2 Schematic ([http://bit.ly/D1-R2-Schematic](http://bit.ly/D1-R2-Schematic)):

![image alt text](image_0.png)

### The Sensors

#### The Anemometer rotary encoder

The Anemometer rotary encoder was created using a disc with 32 hole cut-outs, in addition to a H21A1/2/3 phototransistor optical interrupter switch. Also known as a break beam sensor, this sensor would return a HIGH or LOW if there is a something blocking the sensor or if the sensor reads an opening. In the mechanical design, the encoder reads a wheel with uniform holes punched on the outer rim, so if the encoder reads an opening, at that specific time the encoder would return a 1. And if there is no opening, the encoder would return a 0. Using the encoder as a digital input pin, the program can convert this data into mph, or another unit of wind speed. The datasheet can be found here: [https://goo.gl/RhPdLA](https://goo.gl/RhPdLA). 

#### The DHT-22

The DHT-22 sensor measures temperature and wind-speed, and sends this data via a digital GPIO pin. It does not require i2c because it is not an analog signal, and it does not start outputting its status until it receives a pulse from the MCU host. If it was hooked up to an i2c ADC, the sensor would not output anything. The datasheet for the DHT-22 can be found here: [https://goo.gl/PWb9US](https://goo.gl/PWb9US). 

#### The BMP-180

The BMP-180 sensor measures pressure, altitude, and temperature. This sensor was not required for this project, but was added on anyway because it is ubiquitous for this weather-data gathering purpose. This sensor uses I2C for data transfer. I2C is great because it only requires 2 wires, unlike SPI, which requires 5, and it can support up to 1000 devices. Additionally, this system can have multiple masters on the same bus. See [https://goo.gl/Y5ewC4](https://goo.gl/Y5ewC4) for more information. The datasheet for this sensor can be found here: [https://goo.gl/YBRBK4](https://goo.gl/YBRBK4). 

### Wemos and Sensors Connections

The physical Wemos pins are different from the digital logic pins of the board, primarily because the library used to compile the code for the ESP8266 is generalized for all development boards that use that microchip, and not for Wemos in particular. Therefore, the following chart was utilized when converting from the physical pinout of the Wemos to the programming logic:

![image alt text](image_1.png)

The DHT-22 temperature and humidity sensor was connected to GPIO0, which on the Wemos pinout is D3. The DHT-22 uses the DHT library, which is standard for Arduino libraries and is a submodule in the github repo, linked in the programming section of this report. The anemometer encoder uses GPIO 14, which is D5 on the physical wemos. The BMP 180 uses the SCL and SDA pins on the Wemos, which is D1 and D2, or GPIO5 and GPIO4, respectively. The circuit diagram for the sensors can be found below:

CIRCUIT DIAGRAM FOR SENSORS:

### The Power System

#### The Solar Panel

The solar panel used was a 12-inch 10-watt 12V panel. This was used for the off-the-grid regeneration aspect. The product page can be found here: [http://a.co/03zslCS](http://a.co/03zslCS).

#### The Battery Charging Circuit

The circuit used to charge the battery was a USB DC Solar Lithium Ion charger v2 from Adafruit. It has a 6V input, so a voltage divider was used between the solar panel and the charging circuit, dropping the voltage from 12V to 6V. The product page can be found here: [https://www.adafruit.com/product/390](https://www.adafruit.com/product/390). The charging rate of the battery was increased to 1A by soldering a 1kOhm resistor on the relevant pads, as per the documentation, and a 10K NTC thermistor was added to add temperature - shutoff protection if the battery gets too hot at any time. The datasheets can be found here: [https://goo.gl/T4BmQ8](https://goo.gl/T4BmQ8). Below are the circuit diagrams and schematics:

![image alt text](image_2.png)

![image alt text](image_3.png)

#### The Battery

The battery used was a 6600mAh lithium ion battery pack, at 3.7V, composed of 3 standard 18650 battery cells made by Samsung, each at 2200mAh. Each cell can provide 0.5C (1.1A) of current at peak loads of over 3.3A. It uses a JST jack, making good compatibility with the charging circuit above. The battery pack includes over-charging and voltage protection. See the product page here: [https://www.adafruit.com/product/353](https://www.adafruit.com/product/353).

#### USB female buck converter

A female usb buck converter was used to convert the 5V output of the battery charging circuit to a female USB port at a constant 2A to provide a good supply of power for the raspberry pi to run off of. The USB was connected directly to the charging circuit output, and the product page can be found here: [http://a.co/8t7NNjP](http://a.co/8t7NNjP). 

#### Power Consumption

Power consumption for the Raspberry Pi (below) and the Wemos (above) were calculated to be 120 mA and 80 mA at max, or 200 mA total. Sources: [https://goo.gl/nfo96S](https://goo.gl/nfo96S), [https://goo.gl/anSQF3](https://goo.gl/anSQF3). So with this current draw, and the battery of 6600 mAh, this circuit would theoretically last for 33 hours, or 24 hours to be safe. And the solar panel produces 10 watts every hour, and at 12V that produces 833 mA per hour. So this solar panel is producing far more energy at peak production than is required, and at 500 mA accounting for energy loss. So this panel will theoretically allow for the pi to run indefinitely, as it can produce more than twice the energy needed, preventing cloudy days and the inevitable sunset from also shutting down the data collection. Since the battery circuit never shuts down and the difference in energy consumption from the code is negligible, few steps were taken to reduce energy consumption. One step that was taken was to send data to the github repo every 15 minutes, and refresh the e-ink display every 30 minutes, instead of refreshing them every time the program loops.

### The Raspberry Pi

The last step of the equation is the raspberry pi, essentially connecting this entire project together. The pi gets power from the USB buck converter, as a micro-usb input, and then outputs that power via a micro-usb to micro-usb cable to the Wemos board. Data is transferred through this same between the Pi and the WeMos.

The Raspberry Pi used was a Raspberry Pi Zero, mainly because the processing power did not have to be very high for this project, and the power draw is very low, at about 120 mA at peak use.

The Raspberry Pi Zero W is essentially a low-power, low-cost arm-based computer, and the configuration used runs linux Raspbian, software designed specifically for the raspberry pi. The Pi is powered by a single-core 1GHz ARM v7 system on a chip (SoC), and 512 MB of RAM. Again, this is not a large amount of processing power, but it is sufficient for this project. Full schematics and documentation about the board can be found here: [https://goo.gl/f639zk](https://goo.gl/f639zk). 

#### Raspberry Pi Schematic

![image alt text](image_4.png)

The Raspberry Pi was chosen for this project to process the data coming from the Wemos via the usb cable and save it to a database. The database data was then sent to a github profile, where a simple Github pages website shows the data. This process is further explained in the software design and coding section below, but essentially having the pi allows for the data to be saved to the cloud and then shown concisely in a webpage.

#### The E-Ink Display

One more feature the Raspberry Pi enables is to have different displays and input on the weather station itself. The display used was a 2.9 inch e-ink display created by Waveshare, which has 298x128 resolution, and uses SPI interface to communicate with the Pi. The product page can be found here: [http://a.co/hb4rQ3Y](http://a.co/hb4rQ3Y). The datasheet and more information about using the module can be found here: [https://www.waveshare.com/wiki/2.9inch_e-Paper_Module](https://www.waveshare.com/wiki/2.9inch_e-Paper_Module). The hardware connection to the Pi is as per the following pinout:

![image alt text](image_5.png)

The hardware pins on the Raspberry Pi 3B and Zero W are the same.

#### Push Button

A waterproof push button was also used as input to the raspberry pi, mainly as an on and off switch for the entire station. This was wired to GPIO pins 5 and 6 of the PI, which when shorted turns on the Pi. Part of the python script shown in the programming section uses GPIO pin 5 as input so when the button is pressed, a script is started that saves the data to the cloud and shuts down the Pi safely.

#### Raspberry Pi Pinout

![image alt text](image_6.png)

#### Conclusion

None of this extra functionality - the website, the data-collection and storage in a mysql database, would have been possible without the Pi. And the Pi added amazing functionality to this weather station, adding a display, tactile inputs, and many sensors that could be modularly added to the system. And the off-the-grid circuit with the solar panel allows for data collection from anywhere, at anytime. Even if there is no wifi, the data is stored on the Pi, to be uploaded in the future, with up to 16Gb of storage in remote locations. This system, as implemented, is the best way to create a mobile weather station.

## Software Design and Coding

The software is arguably the integral part of this project, allowing for the data to be collected, processed and then distributed and visualized. To that end, there were four mediums in which software was written. Software was created for the Wemos development board to get the sensor data and send it, for the Raspberry Pi Zero W to interpret that data and distribute it, for the Github pages Bootstrap Javascript webpage for visualization, and on NI Labview for visualization.

These software aspects are discrete in that they take data from one and send it to the next, meaning they were developed independently and integrated afterwards. All of the code that will be referred to is copied in the appendix but is originally on this Github page: [https://github.com/jschmidtnj/MobileWeatherStation](https://github.com/jschmidtnj/MobileWeatherStation). 

### Github

Github is a cloud storage solution for git, which is a software-revision platform. Github was used to allow for collaboration when developing the code, and to allow for the most up-to-date code to be on all of the components of this project. Each time the Pi loads, it runs a script (startup.sh), which creates a fresh copy of this github repository. This ensures that the Pi always has the newest code (read more about git and github here: [https://goo.gl/FHmTgf](https://goo.gl/FHmTgf)).

#### Github Pages

Additionally, Github has a service called Github pages, which allows for Github to act as a web-server for static websites - that is, websites that have discrete html documents which do not change for each user. The website created for showing the data for this project is hosted on Github under the "docs" folder, and can be accessed from the domain [https://anemometer.ml](https://anemometer.ml). Github pages is great because it allows for all of the code for this project to be stored in one place - on that same Github repo, even though the code is comprised of many different systems and parts, as per above.

The only aspect not included in this github repository that is software is the NI Labview application. It would not make sense to include this application because it is not text-based code, so every time there would be a git commit it would just store the file. Github would essentially act like cloud storage at that point, as opposed to a revision-based management system. Therefore the Labview application was stored separately.

### The Flow

![image alt text](image_7.png)

This is essentially the flow of these systems. The sensors send data to the Wemos, and over the USB cable it gets transmitted to the Raspberry Pi. The Data is also sent to a local storage system on the Stevens network, where it is parsed to a csv file. The Raspberry Pi processes the data and saves it to a mySQL database, and a script then saves that data to a csv file. The csv file is uploaded to Github. When people open the website, [https://anemometer.ml](https://anemometer.ml), the javascript file scripts.js runs and processes the data from the csv file on github, adding the data to graphs that are compiled and placed in the html document index.html, on the user’s computer. As the data refreshes every 15 minutes, the website refreshes and users can see the updated data coming in. That way, the data shown is always up-to-date. Finally, a csv document can either be downloaded directly from the Github page or from Stevens servers, to be inputted to the Labview environment. There users can see the data in different graphical forms, and can interpret the data in different ways.

### Wemos code

In this report, the code will be read from top to bottom, following the logic of the program as opposed to the order it was written in, and explained in detail. The best way to follow along is to view the code on github: [https://goo.gl/w8TTPE](https://goo.gl/w8TTPE) as it is explained. In lines 19-28, the various libraries necessary are initialized. ESP8266wifi is self explanatory, PubSubClient and info are for connecting with the Stevens servers to send data, DHT and SFE_BMP180 are for the two sensors, and Wire is for the I2C protocol mentioned in the wiring section. The Running Median library was used to calculate a median of the wind speed, so there are no outliers in the data. The reason why this was not calculated manually was because the C that the Arduino IDE uses does not allow for array lists, and initializing an array each time a value needs to be added would be memory-intensive. This running median library does what is needed with the smallest overhead possible.

The constants on lines 35 and 36 are for the id and password of the Stevens Network. On lines 42-44, the Stevens mySQL server settings that the wemos is accessing to enter the data are initialized. Magic Word is also needed. Lines 50-52 include constants that are used later in the program for publishing delays. Lines 62-65 set up the DHT sensor to pin 0, and on line 73 the anemometer sensor pin is initialized (see electronics section). Lines 76-84 are constants used for interpreting the anemometer data, in the RunningMedian loop (lines 341-361). Lines 86-88 are constants used throughout the program. Line 86, num_loop, is the number of times the wind-speed is calculated and added to the running-median data set. The mult_constant is the calibration constant for the anemometer, and was found by dividing the actual wind-speed (gained from a professional anemometer) by the reading from the custom anemometer sensor created for this project. The delay_in_between is used for the delay between anemometer readings in the loop to gain wind speed readings. Without this variable, the readings would be taken nearly instantaneously, at the clock-speed of the Wemos, which is much faster than the encoder wheel can ever spin. This is measured in milliseconds.

Lines 101-107 initialize self-explanatory values for each of the sensors, and on 109 the current altitude of Hoboken, NJ, is recorded in meters. Lines 146-153 are the configuration of the wificlient and mysql topic, used to communicate and send data to the Stevens server. Lines 154-156 initialize the sensor data variables to be sent to the Stevens server, as do lines 157 and 158. 

#### Setup Function

After this initialization the program goes into the void setup() loop, on lines 250-269. On lines 251 and 252, the built-in LED is initialized as an output and the anemometer pin is initialized as an input. The Serial communication is started on line 253, at a baud rate of 115200. Then on line 264 the setup_wifi() function is called, which starts the wifi connection to the Stevens server. This will not be gone into much detail because it was preconfigured. Then on line 265 the program enters the setup_alt_temp function, which starts the BMP180 sensor. Line 266 starts the DHT sensor, and lines 267-268 wait for a callback from the Stevens server. After the setup loop, the program goes into the main void loop () to be run repeatedly (lines 271-318.

#### Loop Function

The loop function starts on lines 273-276 by checking if the Stevens server is connected, and if not, reconnects to the server. Lines 278-279 check if the time between the last message and the current time is greater than the publish delay, and if it is it publishes the data in the if statement. Line 282 re-initializes the lastMsg variable, and lines 283-284 are where the temperature and humidity read by the DHT sensor is read and stored. Next line 285 goes into the loop_alt_temp function, lines 289-557, which stores the pressure, altitude, and temperature from the BMP180 sensor, and stores the values. Lines 286-295 are for publishing the data to the Stevens mySQL database. In line 298, the wind_speed_samples variable, of type RunningMedian, is created from the get_speed function (lines 341-361).

#### get_speed Function

In the get_speed function, the wind-speed read by the anemometer is calculated. This is done by comparing two modes - mode_1_speed and mode_2_speed, which are both boolean values. mode_1_speed is defined by the digital reading of the anemometer signal pin, so if the two modes are equal, there has been one movement from a hole to the next hole. The current time that this occurs is recorded on line 349, in microseconds since the program started. And if the print_now variable is true, which occurs every second time the program goes through the if statement on line 350. Then on line 352, the value of the wind_speed_sample is stored in the RunningMedian type variable. The multiplication constant is used to account for the physical errors of creating the anemometer - its inertia and friction in the system, and was calculated as explained earlier through experiment. The wind_speed was calculated by dividing the circumference of the wheel (in miles) by the time it took for the movement in the encoder. This time is in microseconds, so it was converted to hours. The multiplication constant takes care of any logical errors in the calculation, to ensure the data gathered from the anemometer is accurate.

#### The loop again

On lines 297-300, the wind_speed_samples are found and averaged. The average is found using the for loop. Then the average temperature from the BMP180 and DHT22 sensors was calculated on line 302. In lines 310 and 311, the temperature and humidity are printed to Serial, and on line 312 the string of data the Pi will interpret is sent to the Serial, at a baud rate of 115200. This data then goes through the USB cable to the Pi, where is it processed (see below for an explanation of this process). Finally, the loop function sleeps for the length of the SLEEP_DELAY (in milliseconds).

#### Flow Chart

![image alt text](image_8.png)

### The Pi

Now that the Wemos data collection code is explained, it is necessary to explain how the Raspberry Pi Zero works in this equation. When the Raspberry Pi starts up, it is configured so that in shell it runs the startup script (./startup.sh). 

#### startup.sh

In this script, as you can see in the appendix or here: [https://goo.gl/NCVAXu](https://goo.gl/NCVAXu), the pi accesses the directory of the github repository, in the Desktop "MobileWeatherStation" (line 1). One line 2, the Pi pulls the newest code from the github repository, ensuring that the programs that are on the pi are up to date. Lien 3 creates a variable called ip4 that stores the ip address of the pi at that moment, and line 4 adds that variable to a new line in the file ip-address.txt, also in the MobileWeatherStation directory. The purpose of this step, of saving the ip address to the github repository, is to allow for me to access the pi via ssh (secure shell, read more here: [https://www.ssh.com/ssh/](https://www.ssh.com/ssh/)). The Stevens network uses dynamic ip addresses, meaning every day or so the ip-address of the Pi changes on the network, especially if the Pi was off and then was turned on. By saving the ip address, I can look at this ip-addresses.txt file on github and see the current ip before ssh-ing to the Pi (the file is located here: [https://goo.gl/MjDMhS](https://goo.gl/MjDMhS), and you can see how the ip changes sometimes). Lines 5-7 add, commit, and push these changes to the ip address to the online github repository. Line 8 starts the python script testdisplay.py, which is used to test the weather station’s e-ink display. And after that python script is done, the script app.py runs, which does all of the data processing and display of the data from the Wemos.

#### testdisplay.py

The testdisplay.py python script is a heavily modified python script originally created by waveshare to test this display (see the code here: [https://goo.gl/vVnTNx](https://goo.gl/vVnTNx)). It prints the labels of the data - "Anemometer Data: “, “Wind Speed: “, “Humidity: ", “Temp 1: ”, and “Temp 2: ” to the screen. Lines 27-31 are import statements for the necessary python scripts, as provided by Waveshare. On lines 122-123, the function enters the main loop. In the main loop, the e-ink display is initialized as a 2.9 inch display on line 32. And then updated on line 35. Line 60 initializes the font for the text, and line 61 creates the image to be sent to the the e-ink display. Lines 63-64 create the character width and height of the lines of text, and lines 66 through 74 create the text as per above and draw the text to the image. Line 78 clears the memory of the display, and line 79 sets the memory of the frame to be the rotated image 270 degrees, because the display is mounted in the weather station upside-down. Finally line 80 displays the frame that was created in lines 60-74. At the end of this python script, the labels of the e-ink display are printed, and the display is verified as tested and working.

#### app.py

After the testdisplay.py the Pi enters the app.py python script, written again in python 3 (see [https://www.python.org/doc/essays/blurb/](https://www.python.org/doc/essays/blurb/) for more information about python). I will again go line by line, so be sure to follow along at this link: [https://goo.gl/Eq4B6u](https://goo.gl/Eq4B6u) or in the appendix. Lines 27-38 are import functions for the various libraries used in this script. Note that the same libraries used in testdisplay.py were used here as well. Lines 41-43 initialize the physical on-off button for the weather station, and lines 44-45 create a variable state_1 that is the initial state of the switch. The variables for wind speed, temperature, humidity, altitude and pressure are defined on lines 46-59 as global variables, meaning they can be accessed by any function, and the variable for the e-ink display is initialized in lines 62-64, also as a global variable, in the same fashion as in the testdisplay.py script. Lines 66-74 are where global variables for different functions, such as the current time, the delay between each screen refresh, and the delay between each data push, are initialized. Lines 77-78 define the mySQL database used - "WeatherStationData", with the user being “station” and the password being “data” for the database. The delay time on line 80 is the delay in between each loop of the main() function (lines 197-259).

#### Peewee Library and Class

The Peewee library is used for inputting mySQL database information via a python script. Lines 82-93 create a class called Data that creates the character fields for each of the data-points that are inputted into the mySQL database, in the "Data" table. The class Meta initializes the database to default to the name db. For more information on Peewee, see [http://docs.peewee-orm.com/](http://docs.peewee-orm.com/). Line 95 creates the Data table in the WeatherStationData database, with the charfield parameters for each of the data-points. 

Lines 97-100 create the serial connection to the Wemos device through the usb port, with the baud rate of 115200, and flush the input. On lines 261-263, the main() loop (lines 197-259) is called forever, using a while True: statement. 

#### main loop

The main loop starts by initializing the priorly-created global variables on lines 198-210. Then on line 214 the state of the button is recorded, and if it different from the initial state, the Pi sends the data to the github repo via the send_data() function on line 220. The send_data function (lines 102-106) uses the os and evoy libraries to run the end-script.sh script.

##### end.sh script

The end.sh script ([https://goo.gl/cLZtGd](https://goo.gl/cLZtGd)) starts by starting the squ-to-csv.sql mySQL script on line 4 ([https://goo.gl/NonnHp](https://goo.gl/NonnHp)). This mySQL script takes the WeatherStationData mySQL database and selects all of the data, outputting it into a csv file called data.csv in the directory /tmp/. Then lines 5 and 6 change the file permissions, and line 7 goes into the tmp directory. Lines 8-10 create a new filename for the data.csv file from the current date, time, year, etc., and line 11 moves this new file to the data folder of the WeatherStationData git repository. Line 12 clears the file current_data_file.csv of its data, and line 13 fills that file with the data from the newly created file, and puts the current_data_file.csv in the git repository. Lines 14-17 navigate into the git repository, add all of the changes, commit the changes with the message "added data files", and push these files to github.

##### main loop

After the end_script.sh script is called on line 106, the program returns to the main loop, and on lines 221-222 the Pi shuts down. If the button was not pressed, the program does not go into the if-statement on lines 218-222 and instead records the current button state on line 223. On line 225, the program reads the incoming data from the serial port, connected to the Wemos. Line 227 splits this data into an array by comma, and lines 228 through 242 save this data into the discrete variable for each data point. The program checks if the datapoint is equal to "nan" and “0.00” because sometimes the sensors do not register an accurate value, and instead return “nan”. Through this method, every time the sensors do not produce an accurate reading, the data stays the same as it was before.

Lines 244-245 add the data to the mySQL database, and line 247 updates the current_time variable. Lines 249-251 send the data to the screen using the show_on_screen function, if the time delay is larger than the variable screen_delay (in minutes). The show_on_screen function (lines 109-195) is very similar to the code used for the testdisplay.py script explained above, but substituting the actual values of the current data-points.

Finally lines 253-255 send the data to the mysql database, and to the github repository, through the same method, using a time delay of "data_delay". Then on line 259 the program sleeps for delay_time, in milliseconds. 

##### conclusion

With app.py explained, all of the python programs are now finished describing. The Wemos reads sensor data and sends it to the Pi over the USB cable, where app.py sends the data to the database and to the e-ink display after a time delay, and every time the method loops to the mySQL database. Now the next aspect of the software that has not been explained yet is the website.

### The Website

In the appendix, and under the "docs" folder of the github repository ([https://goo.gl/rsnV4i](https://goo.gl/rsnV4i)), there is the file index.html. This is the main html file for the website, [https://anemometer.ml/](https://anemometer.ml/). When you enter anemometer.ml into your browser, the domain name service (DNS) Freenom, through which the domain name was registered, redirects the nameservers to Cloudflare (read more here: [https://goo.gl/2sR1um](https://goo.gl/2sR1um)), where Cloudflare attaches an ssl certificate (read more here: [https://goo.gl/k8RC3C](https://goo.gl/k8RC3C)) and redirects the user to the github pages repository, linked above in the docs folder. The index.html page is loaded, and this page is rendered to display all of the weather station data.

This page uses bootstrap ([https://goo.gl/xRMvFi](https://goo.gl/xRMvFi)) as the library framework, making it easy to create material-design ui styling ([https://material.io/guidelines/](https://material.io/guidelines/)) and advanced, modern elements. I will not go into extreme detail about how the html page was created, because it is fairly self-explanatory if you know html. Html is a writing language, not a programming language. I do use Javascript, located in the js folder as scripts.js ([https://goo.gl/p3REAK](https://goo.gl/p3REAK)), and in the appendix under the same name. The scripts.js function is called in line 19 of the index.html file. Javascript is a programming language, and it was used for a few features on the website.

#### Contact us

The first was, on the bottom of the web-page, for taking the contact info of people who want to get in touch, and sending it to a Google Sheets document ([https://goo.gl/QCG6FF](https://goo.gl/QCG6FF)). When people enter their information at the bottom of the webpage and click submit, the information would be sent to the Google Sheet. The javascript program for this is on lines 138-149 of index.html, and essentially the data is entered to a script published online through Google’s form api ([https://goo.gl/AY86yV](https://goo.gl/AY86yV)). The script is saved as the scriptURL variable on line 140, and if there is a response from Google sheet then it worked (line 146).

#### Styling

The styling is located in the custom.css document in the appendix and the github repository, under the css folder: [https://goo.gl/skLZcH](https://goo.gl/skLZcH). Again, this styling is just in css and is not a programming language, so I will not go over how it functions. But in scripts.js, in lines 212-222, there is a function that modifies the css in javascript. This function constantly loops and checks if the user scrolled down past 2000 pixels of the window, and if so, makes the navigation bar transparent. This small styling function makes the website more responsive and look better.

#### scripts.js

The rest of scripts.js is all dedicated to creating the graphs for the data. On line 1, window.onload, the function starts when the user first loads the html document. The graphs are all compiled on the client side, not the server side, in order to make the website static. Lines 4-20 initialize the function "getDataPointsFromCSV", which takes a url for the csv and the column that the data is in, and pushes datapoints for the y and x axis. On line 6, the function uses regex ([https://goo.gl/YD4wXB](https://goo.gl/YD4wXB)) to split the csv into each of the lines, saved as an array, and the for loop from lines 7-18 iterates through the csvlines. Line 11 ignores any “NaN” data, or data that is invalid. Finally, on line 19 the dataPoints are returned.

The rest of the functions in scripts.js are exactly the same, but modify different divs in the html document - different graphs. The graph api used is taucharts ([https://www.taucharts.com/](https://www.taucharts.com/)), which makes it very easy to add beautiful graphs to an html document. Following the documentation, the graphs are created and then rendered to each div (ex. Line 46 to the windspeed div). jQuery.get() is used to get the datapoints from the csv file, and each of the code blocks uses the getDataPointsFromCSV function to get the datapoints for that specific graph (line 25). Rawgit urls are used to ensure the csv file from github is in its raw form, so it can be accessed ([https://rawgit.com/](https://rawgit.com/)). The tooltip plugin is used to allow the user to pan the graph for specific point values (line 43).

#### Conclusion

With the scripts.js file explained, that is essentially how the website works. The website has a static index.html file, served from Github pages, Cloudflare, and Freenom, and uses the custom.css and scripts.js files to render the styling and graphs on the client-side. The result is an intuitive, interactive way of looking at the data coming from the weather station, in real-time.

#### Screen-shots

![image alt text](image_9.png)

![image alt text](image_10.png)

![image alt text](image_11.png)

![image alt text](image_12.png)

![image alt text](image_13.png)

![image alt text](image_14.png)

## Final Evaluation:

1. Discuss the overall performance / field results.

2. Provide a complete analysis of the data captured during fielding.

3. Detail the analysis and the analysis software tools (LabView VIs and Excel based) employed to complete that analysis

# Conclusions and Recommendations

* Describe the results in terms of accomplishments, successful or unsuccessful. Provide recommendations to improve your system. Provide recommendations with regard to  improving  the  project in terms of enhancing  students basic knowledge gained.Describe any lessons learned and their applicability to your future design activities.

# Attachments

## Organization Chart with Roles and Responsibilities

## Supporting CAD drawings

## The Code

See [https://github.com/jschmidtnj/MobileWeatherStation](https://github.com/jschmidtnj/MobileWeatherStation) and [https://anemometer.ml/](https://anemometer.ml/) for the code in a more readable form.

### Wemos

```c++

/*

```

### Raspberry Pi App Code (python)

```python

##

```

### Raspberry Pi Startup Script:

```shell

cd /home/pi/Desktop/MobileWeatherStation

```

### Raspberry Pi End script send data:

```shell

#!/bin/sh

```

### Send data to csv file from mysql

```mysql

use WeatherStationData;

```

### Website index.html: 

```html

<!DOCTYPE html>

```html

### Website Custom Javascript for loading graphs:

```javascript

window.onload = function() {

;```

### Custom CSS

```css

.graph_styling {





```
