# Week 1 (5/21/2018-5/25/2018)

**Monday, May 21st**

Practiced using Arduino
* [Arduino Blink Practice](https://www.arduino.cc/en/Tutorial/Blink)

Realized that the proper board and port were not available. Found packages for additional boards compatible with Arduino IDE
* [Arduino Additional Packages](https://learn.adafruit.com/adafruit-arduino-ide-setup/arduino-1-dot-6-x-ide)

Was stuck on finding the port. Drivers are needed because the chips may not be made by the official Arduino company, and therefore need something to convert the port to something the computer can interpret:
* [Chinese driver for Chinese made Arduinos](http://www.wch.cn/product/CH340.html)
* [More info on drivers to install](http://metatek.blogspot.com/2016/02/setting-up-arduino-ide-on-mac-os-for.html)
* [FTDI Drivers](http://www.ftdichip.com/Drivers/VCP.htm)

Found accelerometer code to try:
* [Accelerometer code](https://learn.adafruit.com/adafruit-analog-accelerometer-breakouts/assembly)


**Tuesday, May 22nd**

Figured out USB port problem:
* [Driver needed for Mac OSX](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) **IS NOT SUPPORTED BY MAC OS X YOSEMITE** 

Found more accelerometer codes to try because the others were giving unrealistic values. May be because the pins were not soldered onto the ADLX335 chip:
* [Calibration and Programming](https://learn.adafruit.com/adafruit-analog-accelerometer-breakouts?view=all#calibration-and-programming) Consisted of a button that was not present for our setup. Discarded because it kept giving the same data points. Might be the result of not having the button.
* [Looked at but did not use code](http://www.instructables.com/id/Interfacing-ADXL335-with-ARDUINO/)
* [GitHub Accelerometer code](https://gist.github.com/nthdesign/407ea40ae035269dd3cfd7ec81402281) Used at first, but discarded because I was not sure how certain values were obtained and was not able to interpret.
* [Accelerometer code being used now](https://www.sunfounder.com/learn/lesson-15-adxl335-super-kit.html)

Started looking into SD card reader:
* [Adafruit Data Logging Shield](https://learn.adafruit.com/adafruit-data-logger-shield/overview) needs a circular battery at all times to use.

Plotting data from Arduino:
* [Need to sync MatLab and Arduino IDE](https://arduino.stackexchange.com/questions/17319/plotting-a-real-time-graph-of-sensor-data-from-arduino-on-processing-matlab-or)
* [MatLab-Arduino Code](https://www.mathworks.com/help/supportpkg/arduinoio/ref/arduino.html)
Most websites searched, there is no way to directly write data toa text file from Arduino IDE. A processing program or an SD card are the best options. Currently allowing some data to run and then copy-pasting to an Excel file to analyze and plot with MatLab.

***Wednesday's task: get SD card arduino to work and save data to analyze***

Things we learned. 

Adafruit drivers notes please! 

[Google](http://www.google.com)

* Hi
* There

*Italics*  **Bold** ***BOLD IT***

```
int x = 10;
```
