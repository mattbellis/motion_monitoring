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
* [Adafruit Data Logging Shield](https://learn.adafruit.com/adafruit-data-logger-shield/overview) needs a circular battery at all times to keep the internal clock up-to-date, whether it works or not (but is said to last for five years). Removing the battery resets the clock and needs [this](https://learn.adafruit.com/adafruit-data-logger-shield/using-the-real-time-clock) to reset it.

Plotting data from Arduino:
* [Need to sync MatLab and Arduino IDE](https://arduino.stackexchange.com/questions/17319/plotting-a-real-time-graph-of-sensor-data-from-arduino-on-processing-matlab-or)
* [MatLab-Arduino Code](https://www.mathworks.com/help/supportpkg/arduinoio/ref/arduino.html)
Most websites searched, there is no way to directly write data toa text file from Arduino IDE. A processing program or an SD card are the best options. Currently allowing some data to run and then copy-pasting to an Excel file to analyze and plot with MatLab.

***Wednesday's task: get SD card arduino to work and save data to analyze***

**Wednesday, May 23rd**

Searched for the [Adafruit Data Logging Shield Battery](https://www.adafruit.com/product/1141) at several different stores, Bellis finds them in 10 minutes...

Working on allowing the accelerometer to take data points over a period of time and manually transferring the data to a .txt file in order to use MatLab to analyze it.

```
%% Read in CSV file
Accelerometer_Data = 'Accelerometer_Data.csv';

%% Divide columns into variables
xData = csvread('Accelerometer_Data.csv',0,0,[0 0 67 0]);
yData = csvread('Accelerometer_Data.csv',0,1,[0 1 67 1]);
zData = csvread('Accelerometer_Data.csv',0,2,[0 2 67 2]);

%% Plot Data
figure(1)
plot3(xData,yData,zData)
title('X, Y, and Z Accelerometer Coordinates')
xlabel('X Coordinates')
ylabel('Y Coordinates')
zlabel('Z Coordinates')
```

Created just to look at the graph it gives. Need to think of a more useful and practical way to analyze the data and what it would mean. Need to incorporate time stamps in order to analyze how long one particular coordinate the accelerometer was at. Will convert to Python soon.

***NOTE*** When using SD Cards, always check with the CardInfo sketch on the IDE to see if it is a FAT32 or FAT16 type and size of memory. This also helps check if the card is a legit one and good to use, otherwise an error will appear asking if the card is inserted.

Tried connecting the accelerometer to the SD card arduino using the [Build It!](https://learn.adafruit.com/adafruit-data-logger-shield/light-and-temperature-logger-use-it) part of the data logging shield tutorial, then used [Use It!](https://learn.adafruit.com/adafruit-data-logger-shield/using-the-real-time-clock-2) to try and compile both codes, but started getting values that did not resemble what was originally obtained. Values were much higher than originally and not constant when the accelerometer was at rest. Possible that my own interpretation of the wiring is the cause.

Reverted original pins for the accelerometer on the data loggin shield and it gave the original data sets (thanks Bellis!).

[Code combining accelerometer and shield](https://learn.adafruit.com/adafruit-data-logger-shield/using-the-real-time-clock-3) is giving some errors, specifically that certain functions were not "members" of what was being called (*"class DateTime' has no member named 'get'*). Troubleshooting this now.

```
#include <SPI.h>
#include <SD.h>
#include <Wire.h>
#include "RTClib.h"

#define LOG_INTERVAL 1000 // mills between entries
#define SYNC_INTERVAL 1000 // mills between calls to write data to card
uint32_t syncTime = 0; // Time of last sync()

#define ECHO_TO_SERIAL 1 // Echo data to serial port
#define WAIT_TO_START 0 // Wait for serial input in setup()

#define redLEDpin 2 // Digital pins connected to LEDs
#define greenLEDpin 3

const int xPin = A2;
const int yPin = A1;
const int zPin = A0;

RTC_PCF8523 RTC; // Define the Real Time Clock object
const int chipSelect = 10; // Digital Pin 10 is connected to the SD card

File logfile;

void error(char *str)
{
  Serial.print("error: ");
  Serial.println(str);

  digitalWrite(redLEDpin, HIGH); // Turns on when there is an error

  while(1);
}

void setup(void)
{
  Serial.begin(9600);
  Serial.println();

  #if WAIT_TO_START
    Serial.println("Type any character to start");
    while(!Serial.available());
  #endif

  //Initialize the SD Card
  Serial.print("Initializing SD card...");
  pinMode(10, OUTPUT);
  if (!SD.begin(chipSelect)) {
    Serial.println("Card failed, or not present");

    return;
  }
  Serial.println("Card initialized.");

  // Create a new file
  char filename[] = "Accel_SD00.csv";
  for (uint8_t i = 0; i < 100; i++) {
    filename[6] = i/10 + '0';
    filename[7] = i%10 + '0';
    if (! SD.exists(filename)){
      // Only open a new fiel if it doesn't exist
      logfile = SD.open(filename, FILE_WRITE);
      break; // Leaves the loop
  }
}

  if (! logfile) {
    error("Couldn't create file.");
  }

  Serial.print("Logging to: ");
  Serial.println(filename);

  Wire.begin();
  if (!RTC.begin()) {
    logfile.println("RTC failed.");
#if ECHO_TO_SERIAL
  Serial.println("RTC failed.");
#endif
  }

  logfile.println("mills,time,xData,yData,ZData");
#if ECHO_TO_SERIAL
  Serial.print("millis,time,xData,yData,zData");
#endif
/*
#if ECHO_TO_SERIAL
  if (logfile.writeError || !logfile.sync()) {
    error("write header");
#endif
  }
 */
  pinMode(redLEDpin, OUTPUT);
  pinMode(greenLEDpin, OUTPUT);
}


void loop(void)
{
  DateTime now;

  delay((LOG_INTERVAL -1) - (millis() % LOG_INTERVAL));
  digitalWrite(greenLEDpin, HIGH);

  // Log milliseconds since starting
  uint32_t m = millis();
  logfile.print(m);
  logfile.print(", ");
#if ECHO_TO_SERIAL
  Serial.print(m);
  Serial.print(", ");
#endif

  now = RTC.now(); <-------- ERROR HERE ----------
  logfile.print(now.get());
  logfile.print(", ");
  logfile.print(now.year(), DEC);
  logfile.print("/");
  logfile.print(now.month(), DEC);
  logfile.print("/");
  logfile.print(now.day(), DEC);
  logfile.print(" ");
  logfile.print(now.hour(), DEC);
  logfile.print(":");
  logfile.print(now.minute(), DEC);
  logfile.print(":");
  logfile.print(now.second(), DEC);
#if ECHO_TO_SERIAL
  Serial.print(now.get());
  Serial.print(", ");
  Serial.print(now.year(), DEC):
  Serial.print("/");
  Serial.print(now.month(), DEC);
  Serial.print("/");
  Serial.print(now.day(), DEC);
  Serial.print(" ");
  Serial.print(now.hour(), DEC);
  Serial.print(":");
  Serial.print(now.minute(), DEC);
  Serial.print(":");
  Serial.print(now.second(), DEC);
#endif

  int x = analogRead(xPin);
  delay(1);
  int y = analogRead(yPin);
  delay(1);
  int z = analogRead(zPin);

  float zero_G = 512.0; // ADC is 0 ~ 1023, the zero G output
  // equals to Vs / 2

  float scale = 102.3; // Accelerometer sensitivity is 330mv/g

  logfile.print(((float)x - 331.5) / 65 * 9.8);
  logfile.print("\t");
  logfile.print(((float)y - 329.5) / 68.5 * 9.8);
  logfile.print("\t");
  logfile.print(((float)z - 340) / 68 * 9.8);
  logfile.print("\n");
#if ECHO_TO_SERIAL
  Serial.print(((float)x - 331.5) / 65 * 9.8);
  Serial.print("\t");
  Serial.print(((float)y - 329.5) / 68.5 * 9.8);
  Serial.print("\t");
  Serial.print(((float)z - 340) / 68 * 9.8);
  Serial.print("\n");
 #endif

  digitalWrite(greenLEDpin, LOW);
}
```

***Thurdsay's task: Troubleshoot code and try to save data onto the SD card.***

**Thursday, May 24th**

Fixed error in Arduino code

```
include <Time.h>        <---------- Included this -----------
#include <SPI.h>
#include <SD.h>
#include <Wire.h>       <---------- Included this -----------
#include "RTClib.h"     <---------- Included this -----------

#define LOG_INTERVAL 1000 // mills between entries
#define SYNC_INTERVAL 1000 // mills between calls to write data to card
uint32_t syncTime = 0; // Time of last sync()

#define ECHO_TO_SERIAL 1 // Echo data to serial port
#define WAIT_TO_START 0 // Wait for serial input in setup()

#define greenLEDpin 2 // Digital pins connected to LEDs         <---------- Changed variable (green is LED 1) ---------
#define redLEDpin 3                                             <---------- Changed variable (red is LED 2) -----------

const int xPin = A2;
const int yPin = A1;
const int zPin = A0;

RTC_PCF8523 RTC; // Define the Real Time Clock object
const int chipSelect = 10; // Digital Pin 10 is connected to the SD card

File logfile;

void error(char *str)
{
  Serial.print("error: ");
  Serial.println(str);

  digitalWrite(redLEDpin, HIGH); // Turns on when there is an error

  while(1);
}

void setup(void)
{
  Serial.begin(9600);
  Wire.begin();               <-------------- Included this ------------
  RTC.begin();                <-------------- Included this ------------
  Serial.println();

  #if WAIT_TO_START
    Serial.println("Type any character to start");
    while(!Serial.available());
  #endif

  //Initialize the SD Card
  Serial.print("Initializing SD card...");
  pinMode(10, OUTPUT);
  if (!SD.begin(chipSelect)) {
    Serial.println("Card failed, or not present");

    return;
  }
  Serial.println("Card initialized.");

  // Create a new file
  char filename[] = "Accel_SD00.csv";
  for (uint8_t i = 0; i < 100; i++) {
    filename[6] = i/10 + '0';
    filename[7] = i%10 + '0';
    if (! SD.exists(filename)){
      // Only open a new fiel if it doesn't exist
      logfile = SD.open(filename, FILE_WRITE);
      break; // Leaves the loop
  }
}

  if (! logfile) {
    error("Couldn't create file.");
  }

  Serial.print("Logging to: ");
  Serial.println(filename);

  Wire.begin();
  if (!RTC.begin()) {
    logfile.println("RTC failed.");
#if ECHO_TO_SERIAL
  Serial.println("RTC failed.");
#endif
  }

  logfile.println("mills,time,xData,yData,ZData");
#if ECHO_TO_SERIAL
  Serial.print("millis,time,xData,yData,zData");
#endif
/*
#if ECHO_TO_SERIAL
  if (logfile.writeError || !logfile.sync()) {
    error("write header");
#endif
  }
 */
  pinMode(redLEDpin, OUTPUT);
  pinMode(greenLEDpin, OUTPUT);
}


void loop(void)
{
  DateTime now = RTC.now();           <-------------- Changed DateTime now; to this --------------

  delay((LOG_INTERVAL -1) - (millis() % LOG_INTERVAL));
  digitalWrite(greenLEDpin, HIGH);

  // Log milliseconds since starting
  uint32_t m = millis();
  logfile.print(m);
  logfile.print(", ");
#if ECHO_TO_SERIAL
  Serial.print(m);
  Serial.print(", ");
#endif

//  logfile.print(now.get());             <------------- Commented out this line and the next -------------
//  logfile.print(", ");                  <------------- because it was not needed for the code -----------
  logfile.print(now.year(), DEC);
  logfile.print("/");
  logfile.print(now.month(), DEC);
  logfile.print("/");
  logfile.print(now.day(), DEC);
  logfile.print(" ");
  logfile.print(now.hour(), DEC);
  logfile.print(":");
  logfile.print(now.minute(), DEC);
  logfile.print(":");
  logfile.print(now.second(), DEC);
#if ECHO_TO_SERIAL
//  Serial.print(now.get());              <----------- Did the same for this line and the next ------------
//  Serial.print(", ");                   <-------------------- for the same reason -----------------------
  Serial.print(now.year(), DEC);
  Serial.print("/");
  Serial.print(now.month(), DEC);
  Serial.print("/");
  Serial.print(now.day(), DEC);
  Serial.print(" ");
  Serial.print(now.hour(), DEC);
  Serial.print(":");
  Serial.print(now.minute(), DEC);
  Serial.print(":");
  Serial.print(now.second(), DEC);
#endif

  int x = analogRead(xPin);
  delay(1);
  int y = analogRead(yPin);
  delay(1);
  int z = analogRead(zPin);

  float zero_G = 512.0; // ADC is 0 ~ 1023, the zero G output
  // equals to Vs / 2

  float scale = 102.3; // Accelerometer sensitivity is 330mv/g

  logfile.print(((float)x - 331.5) / 65 * 9.8);
  logfile.print("\t");
  logfile.print(((float)y - 329.5) / 68.5 * 9.8);
  logfile.print("\t");
  logfile.print(((float)z - 340) / 68 * 9.8);
  logfile.print("\n");
#if ECHO_TO_SERIAL
  Serial.print(((float)x - 331.5) / 65 * 9.8);
  Serial.print("\t");
  Serial.print(((float)y - 329.5) / 68.5 * 9.8);
  Serial.print("\t");
  Serial.print(((float)z - 340) / 68 * 9.8);
  Serial.print("\n");
 #endif

  digitalWrite(greenLEDpin, LOW);
}
```

Found the corrections and updated the code from [this forum on Arduino](https://arduino.stackexchange.com/questions/3354/why-is-my-real-time-clock-getting-the-wrong-time-from-my-pc)

Once I made these changes, the code was able to be verified and then uploaded to the Metro board. Now running into an error with creating a file after the SD card is initialized.


Things we learned. 

Adafruit drivers notes please! 

[Google](http://www.google.com)

* Hi
* There

*Italics*  **Bold** ***BOLD IT***

```
int x = 10;
```
