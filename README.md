Weather Sensors
===============

### Arduino ProMini, 433MhzRx and Oregon Scientific
### Temperature and Humidity Sensor THGR122NX

This project allows the 433MHz signals from an Oregon Scientific Temperature and Humidity Sensor (THGR122NX) to be intercepted, decoded and displayed on an LCD using an Arduino Uno. It is highly recommended to use a Super Superheterodyne Receiver to get better noise rejection and sensitivity.

The Hardware

![alt text](images/front.jpg?raw=true "Oregon Scientific Temperature and Humidity Sensor (THGR122NX)")

The red LED flashes every time a transmission is made. 

![alt text](images/back.jpg?raw=true "Oregon Scientific Temperature and Humidity Sensor (THGR122NX)")

Note the switch to choose one of three sensor ID's.

![alt text](images/arduino+433Rx.jpg?raw=true "Arduino Pro-Mini, 433MHz SuperHet Rx, I2C Interface+LCD")

Arduino Pro-Mini, 433MHz SuperHet Rx, I2C Interface+LCD

The Arduino listens continually for the 433MHz signals on Pin8 and decodes the Manchester Protocol.  The protocol for this sensor differs from the OS WMR86 Weather Station that the polarity is reversed and the bit-rate is about half the WMR86 V3.0 frequency.  Fortunately the Oregon Scientific data packet structure is identical to the WMR86.  This initially caused considerable confusion as it was thought the THGR122NX would have the same V3 protocol as the WMR86, but with no results forthcoming, it was obvious something was different.  Changing the polarity of the Manchester decoding was tried first but no avail, and then the bit rate was doubled and, and messages began to appear.  A little bit of fine tuning around the bit rate and processing the packets gave a steady stream of Temperature and Humidity readings. It would be great to be able elaborate on a difficult and clever analysis that revealed this required adjustment, but it was just a gut guess, and only took a couple of guesses and it was working! Adding an LCD display to verify it was working in a practical way confirmed the initial test.

The Temperature and Humidity Sensor THGR122NX is a nice bit of Oregon Scientific kit. They are relatively expensive, but a robust design that runs a long time on two AAA Cells.  Designing and making the low power sensor that powers a 433MHz wireless Tx for many months (years?) is normally a very hard part of this sort of project to do from scratch.  However the addition of a professional sensor to an Arduino project still has all the goodies for experimenters on the Arduino side of things. This particular sensor also has a direct LCD readout of the Temperature and Humidity on the outside and is a handy way to double check the Arduino is working properly and reporting the Temp and Hum correctly.

The other model that has been tested as well is the THGN132N Temperature and Humidity Sensor from Oregon Scientific.  It does not have the luxury of the LCD display, but only requires a single AA Battery.  A third "temperature only" model is the Oregon THN132N Thermo Sensor, which is also water proof, so probably very rugged.  However This latter model has not been tested with this software.  The OS website does mention that it is compatible with the Oregon Scientific weather stations using 2.2 Protocol sensors (Compatible With RAR813, RAR213HG, BAR218HG).  This is mentioned for all the above sensors so this last sensor is most likely compatible too.

Some variation was discovered between the two Temp/Hum sensors tested when displaying the Humidity, and up to 6-9% difference was observed. Just remember the Humidity sensors in these systems are not extremely accurate and may need some sort of conversion factor applied to correct for a particular sensor.

All the sensors discussed above have a switch in the battery compartment that allocates a station number of 1,2 or 3.  So it would be quite easy to identify up to three sensors in the program.  This has been tested, but is commented out in its present state. A mixture of the sensors could be used if desired.  

These robust and well designed units from Oregon Scientific are highly recommended, but there is no financial benefit to me if you purchase one.

For a detailed explanation of the Manchester Protocol and structure of OS data packets please read https://github.com/robwlakes/ArduinoWeatherOS 
