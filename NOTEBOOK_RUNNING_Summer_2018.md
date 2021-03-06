# Week 6 (6/25/2018 - 6/29/2018)

**Monday, June 25th**

Going to test out all of the connections on the board to see if there are any cold solders that are responsible for the way that the device was working on Friday. May replace the solder joints with wires that connect to have more reliable connections.

Replaced the pins on a new (and our last) accelerometer so that they were not all connected together underneath to make it easier to remove the accelerometer in case something was not working right.

**Tuesday, June 26th**

Used a new solderable breadboard, the new accelerometer, and another push button to redo the entire circuit since it was noticed that there was no voltage going to the x pin on the last model. Replaced the solder connections with wires to simplify the connections and guarantee that there were no cold solder joints.

EVERYTHING WORKS PERFECTLY. Have to figure out how to calibrate the sensors correctly.

**Wednesday, June 27th**

Worked on the symposium poster for the day.

**Friday, June 29th**

The last day of research! Going over with Bellis last minute details on poster, and possible ways to continue this project for advanced lab.


# Week 5 (6/18/2018 - 6/22/2018)

**Monday, June 18th**

Analyzed data taken while at home. Tried to take data of a five year-old's movements, but the connections were disconnected while she was moving. 

Possible solderable breadboards to make the connetions to the accelerometer more permanent:
* [This one](https://www.amazon.com/dp/B01M7R5YIB/ref=sxbs_sxwds-stppvp_3?pf_rd_m=ATVPDKIKX0DER&pf_rd_p=6297546923292665688&pd_rd_wg=7BYmY&pf_rd_r=6E5VXVWSD5ZX54QF1ZC0&pf_rd_s=desktop-sx-bottom-slot&pf_rd_t=301&pd_rd_i=B01M7R5YIB&pd_rd_w=uSjmY&pf_rd_i=solderable+breadboard&pd_rd_r=643dff0e-8fc2-4f6c-86fa-a1c76526c67f&ie=UTF8&qid=1529334016&sr=3) (**Ended up ordering these ones**)
* Or [this](https://www.amazon.com/PRT-12070-Sparkfun-Solder-Able-Breadboard/dp/B06ZYY3SF3/ref=sr_1_5?s=hi&ie=UTF8&qid=1529334395&sr=1-5&keywords=solderable+breadboard)
* Or [these](https://www.amazon.com/5X10cm-Copper-Prototype-Single-Breadboard/dp/B072N4G2F8/ref=sr_1_10?s=hi&ie=UTF8&qid=1529334413&sr=1-10&keywords=solderable+breadboard)

**Tuesday, June 19th**

Starting analysis on computer identification of different walking styles.

**Wednesday, June 20th**

Got the solderable breadboards and attempted to connect the accelerometer and push button on it, but failed. Wasn't sure how to connect the components together with solder, so looked up a [video](https://www.youtube.com/watch?v=kROaQZOYNIw) on how to do it for practice on another of the smaller boards.

Shortened all of the wires on the Arduino board so that the device could be more compact.

**Thursday, June 21st**

Made a little diagram to see how I wanted the connections to go on the breadboard and then used a new one to make the connections. Have to get the accelerometer and push button out of the old one or might leave them in there and use different ones.

Gonna have to start making the design for the case on TinkerCAD somehow. Measurements for case:
* Width: 5.3 cm
* Length: 7 cm
* Height: 3.5 - 4 cm

**Friday, June 22nd**

Connected everything together and tested it out to record on to the SD card. Creates files and saves them, but the x acceleration is not recording what it should be possibly because of the connections that were soldered on. There's also a problem with it stopping recording when the button is pressed depending on how the new board is positioned; when it is loose and not held straight, pressing the button will make the program say "closing file" and stops recording, but when it is held straight and closer to the shield, it does not read out the "closing file" command when the button is pressed and instead just slows down the recording. Switching between holding the board flat and not makes it go between these two scenarios.


# Week 4 (6/11/2018 - 6/15/2018)

**Monday, June 11th**

Bellis fixed the opening-two-files problem on Friday. Have to figure out the push button and an extra accelerometer on the data shield now.

Met with Bellis to go over the [changing state of the push button](http://tymkrs.tumblr.com/post/19734219441/the-four-pin-switch-hooking-it-up) in order to get the onboard LED lights to flash and stop. Going to incorporate his code to try and make the red and green lights flash with different states, and then hopefully, get it to start and stop recording data onto the SD card.

Got Red/Green LED light state change to work! Time to get it to work with the SD card.

New code writes files to SD card, but creates two open files, and then closes the file before it begins printing accelerometer measurements. Stops/starts recording like it should after the initial run.

***Tasks for Tuesday: Meet with Bellis to figure out push button-SD card logic, start creating cases for the accelerometer to be 3d printed, work on academic poster, data analysis (maybe??)***

**Tuesday, June 12th**

Found out that when the button is pushed, it is actually in a low state, as opposed to a high state as thought!

Code not doing exactly what is expected because it may be getting disconnected when the button is pressed. However, [flush](https://www.arduino.cc/en/serial/flush) helps solve the problem of the files being empty.

***Tasks for Wednesday: Start designing case for the system, data analysis (maybe??), take more data points.***

**Wednesday, June 13th**

Connected the entire set up to a battery pack and walked around campus to collect several sets of data. Changed out some of the wires to make it more compact. Thinking of using a [solderable protoboard](https://www.sparkfun.com/products/12070) (not the exact one that will be used; just an example) to make the accelerometer/push button setup more permanent.

***Tasks for Thursday: Gather more data around the house with other members of the family, figure out how to analyze the data.***

**Thursday, June 14th**

Took various sets of data around the house and outside.

# Week 3 (6/4/2018 - 6/8/2018)

**Monday, June 4th**

Reevaluated approach to this project: abandoning the plotting-position-from-acceleration path and now focusing on solely acceleration. Going to figure out best way to implement two accelerometers (on feet or on hands?) and make the whole system portable with a battery pack.

* [Possible battery pack option](https://www.adafruit.com/product/1959) that is also the cheapest.
* [Another option](https://www.adafruit.com/product/1565), slightly more expensive.
**Found portable battery pack in lab, currently charging it.**

Based on last week's data, the accelerations recorded can show the footsteps that a person has taken. Knowing this, various walking styles will be recorded to analyze the accelerations in all directions and their magnitudes.

Attaching two accelerometers to the board, the board can be attached to a belt or in a pack? Then long wires from the board to the accelerometers can be ran through shirt sleeves and attached to the end?

***Unplugging the board from the computer once the program has been uploaded to connect to battery source... Wouldn't it reset the board??***
* [DC jack has an on/off switch](https://www.adafruit.com/product/2488) (first bullet point) which can supply the power while the program is being uploaded to the board!
* [USB-to-DC-jack attachment](https://www.adafruit.com/product/2697)
* [Ordering this attachment](https://www.amazon.com/HUACAM-HC05-Barrel-Power-Cable/dp/B01303TWZ2/ref=sr_1_3?ie=UTF8&qid=1528127502&sr=8-3&keywords=usb+to+barrel+jack) to use with the board.

Differentiating acceleration data yields the jerk of a system (according to Bellis [and this Wikipedia article](https://en.wikipedia.org/wiki/Jerk_(physics))). It also loses one value, thus it cannot be plotted with the times.
* Is it the first or last number that is removed?
* Is it possible to remove one time variable so that the number of items within each array are the same?

**Took the first and last entry of the time array and was able to get a plot. Not sure if that is the correct way to handle this.**

Looking into how to get serial readings (and eventually saved on SD card) from two accelerometers on one Metro board.
* [This](http://forum.arduino.cc/index.php?topic=312246.0) may have helped to get an idea of how to get readings from two accelerometers.

**[Fitbit SDK](https://dev.fitbit.com/)**

***Tasks for Tuesday: Figure out why two accelerometers on one board is not working, start comparing different walking styles on one graph, think ahead to how a computer would interpret different walking styles.***

**Tuesday, June 5th**

Was able to get the two accelerometers to work, but there must be a problem with the connection when both are hooked up because the X and Y accelerations for the second one are consistently 1023. When hooked up separately, they give values though. Looking up why that is.

Created graphs comparing the data collected when "stumbling" and walking. Have to figure out how a computer would be able to tell the difference between the two.

***Tasks for Wednesday: Continue figuring out connections/code for both accelerometers, ways to get a computer to tell the difference in walking styles, meet with Bellis if nothing still doesn't work.***

**Wednesday, June 6th**

Found out that the X and Y inputs were not giving readings because [SDA and SCL](https://learn.adafruit.com/adafruit-shield-compatibility/data-logging-shield-assembled) are connected to Analog Pins 4 and 5. Have to figure out how to get both on the logging shield so that both of their data can be collected onto the SD card.

Starting to add the push button to the system, that way recording and saving data can be easier.

***Tasks for Thursday: Figure out push button set up, try to see if there is a way to get two accelerometers on the data shield, continue to figure out data analysis.***

**Thursday, June 7th**

Realized I forgot a resistor that would help properly make the push button work, but found [this forum](http://www.instructables.com/id/Arduino-Button-with-no-resistor/) that gave a code without the resistor because Arduinos have internal pull-up resistors that can be used. [This schematic/circuit diagram](https://www.arduino.cc/en/Tutorial/Button) shows how to connect the push button.

Was able to get the push button to work solely on the Metro board, not when the data shield was attached. With the data shield, the program could not upload to the board for some reason.

Got the program to load onto the board when data shield is connected, but it does not work; all lights remain on.

Using the breadboard again just to figure out how to get it to save each new variable when the button is pressed. Trying to get it so that when it is first pushed, it starts logging data to the SD card, and when it is pressed again, it stops logging data. So far, I've tried:
* [Looked at this](https://www.arduino.cc/en/Tutorial/Switch), have not tried it yet, though I am.
* [This](http://forum.arduino.cc/index.php?topic=253093.0)
* [Actually tried this one](http://www.instructables.com/id/Most-Simplest-Toggle-Switch-With-Arduino/)
* [Tried this too](https://arduino.stackexchange.com/questions/3479/how-to-toggle-led-on-button-press)

Tried [this code](https://www.arduino.cc/en/Tutorial/Switch), but it gives the same results as the others that were tried: turns off the LEDs when the button is pressed and turns them on when the button is not. Not what we're aiming for... Maybe looking at this from the wrong perspective or not using the right terminology for what I am looking for...

***Tasks for Friday: Talk with Bellis about results from today, try to get push button to work, think about the two accelerometer problem, continue data analysis.***

# Week 2 (5/28/2018 - 6/1/2018)

**Tuesday, May 29th**

Last Friday, we were able to get the code to stop when a certain character was inputted into the Serial Monitor, but it did not close the file appropriately so none of the points were saved onto the SD card.

Going to try and integrate the data already collected, figure out if there is a manual way to calibrate the accelerometer or if a button is needed, and look up battery packs that could make the accelerometer portable.

Found that [calibrating the x, y, and z axes](https://forum.arduino.cc/index.php?topic=140494.0) consists of using the min and max values when the accelerometer is laying still to determine the Zero G value as well as the "resolution" (assuming this means the correction factor?) to calibrate the values.

* [This site](https://chionophilous.wordpress.com/2011/08/26/accelerometer-calibration-ii-simple-methods/) helped realize that there were certain values that were needed to find the Zero G value and not just random numbers.

Using the calibration method made certain values zero at certain alignments of the accelerometer. Need it to show that when it is not moving, all values must be zero.

* [The datasheet for the ADXL335](https://www.sparkfun.com/datasheets/Components/SMD/adxl335.pdf) to try and figure out whether the accelerometer is measuring accelerations or orientations of the accelerometer itself.

**Wednesday, May 30th**

Used the Python code to create an example of how to integrate acceleration to velocity to position.

Restructured the code so that when the accelerometer is not moving, the x and y points are relatively zero while the z points are at 9.8 m/s^2 (half of that at the moment). Still playing with the numbers to figure out what we actually want the serial monitor to show. Could not get the Arduino code to save the data points onto the SD card for some reason.

**NOTE: Arduino data files must have the file name in ALL CAPS and UNDER eight characters or it will not save correctly.**

***Thursday's Task:***
* Try to analyze data on SD card and integrate for velocity and position.
* Figure out accelerations for x, y, and z axes.

**Thursday, May 31st**

Saved some test data on the SD card, used the Jupyter notebook to analyze the data succesfully!

Took seven different trials doing various different speeds while walking and also different directions. Since the breadboard was forgotten in the lab, had to hold the accelerometer between fingers to keep it "steady." There was some wobbling when moving. Created graphs for all accelerations, velocities, and positions for each instance. Did not generate positon graphs as I had hoped they would, such as showing the path that the accelerometer took, instead they were straight lines. 

Might have to play around with the calibration again? 

Converted all of the times to seconds instead of milliseconds and the numbers look more believable now. Created 3D plots with the new data and still does not track the actual path taken.

***Tasks for Friday: Talk with Bellis about graphs generated, finish up remaining tasks on sheet (in lab), come up with new game plan for Week 3.***

**Friday, June 8th**

Received the USB-to-DC-jack cord and was able to power and work the push button with the power supply. Seems as though that any program that was uploaded to the board before being turned off is still on the board, so there is no concern that it would be wiped once it is taken off of the USB.

Maybe the push button can be used to stop logging data entries since there is a reset button that could restart the program to take new data points. Should make the code be able to create new files if one already exists instead of continuing to add on to the same one or manually.

Able to get the program to create separate new files each time, but it opens two at once and does not store any information.

**Friday, June 1st**

Looked at the graphs with Bellis and retook some of data to see where the accelerometer was picking up on my footsteps.

***Tasks for Monday: Regroup with Bellis to figure out a game plan. Half way done!!***

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

Found the corrections and updated the code from [this forum on Arduino](https://arduino.stackexchange.com/questions/3354/why-is-my-real-time-clock-getting-the-wrong-time-from-my-pc).

Once I made these changes, the code was able to be verified and then uploaded to the Metro board. Now running into an error with creating a file after the SD card is initialized.

Created an if-else statement for creating the file because, when creating the file, it would automatically jump to saying that it could not be made, so now it looks like:

```
 // Create a new file
  char filename[] = "Accel_SD00.csv";
  for (uint8_t i = 0; i < 100; i++) {
    filename[8] = i/10 + '0';
    filename[9] = i%10 + '0';
    if (! SD.exists(filename)){
      // Only open a new fiel if it doesn't exist
      logfile = SD.open(filename, FILE_WRITE);
      break; // Leaves the loop
  }
    else (! logfile); {
      error("Couldn't create file.");
  }
}
```

Once making this change, the file was able to be created, and data was collected in the Serial Monitor, and the LED light was indicating that it was also being transferred to the SD card. Still needs to be checked.

SD card had nothing stored on it. Tried adding:

```
logfile.close();
```
at the end of the logfile.prints. This did not help.

Tried the ReadWrite example on the IDE and it was able to succesfully store a test.txt file on the SD card, so it is the code and the placement of where everything is that's the problem. Playing around with the way in which the code is written to try and mimic the ReadWrite example.

***Five and a half hours later*** finally got the data to correctly place the data on the SD card! The card must be removed in between the Arduino taking data points (after each loop), otherwise the file will remain open and not save the data. When putting the SD card back in, the file continues writing to the same one instead of erasing it and rewriting new data points, even when the code is re-uploaded onto the arduino board.

**FINAL ARDUINO CODE**

```
#include <RTClib.h>
#include <Time.h>
#include <SPI.h>
#include <SD.h>
#include <Wire.h>
#include "RTClib.h"

#define LOG_INTERVAL 1000 // mills between entries
#define SYNC_INTERVAL 1000 // mills between calls to write data to card
uint32_t syncTime = 0; // Time of last sync()

#define ECHO_TO_SERIAL 1 // Echo data to serial port
#define WAIT_TO_START 0 // Wait for serial input in setup()

#define greenLEDpin 2 // Digital pins connected to LEDs
#define redLEDpin 3

const int xPin = A2;  // Where the x-coordinate is connected to the board
const int yPin = A1;  // Where the y-coordinate is connected to the board
const int zPin = A0;  // Where the z-coordinate is connected to the board

RTC_PCF8523 RTC; // Define the Real Time Clock object
const int chipSelect = 10; // Digital Pin 10 is connected to the SD card

File logfile;  // Defines the variable for the file

void error(char *str)
{
  Serial.print("error: ");
  Serial.println(str);

  digitalWrite(redLEDpin, HIGH); // Turns on when there is an error

  while(1);
}

void setup() {
  Serial.begin(9600);
  Wire.begin();
  RTC.begin();
  Serial.println();

  //Initialize the SD Card
  Serial.print("Initializing SD card...");
  pinMode(10, OUTPUT);  // Always set for OUTPUT
  if (!SD.begin(chipSelect)) {
    Serial.println("Card failed, or not present");

    return;
  }
  Serial.println("Card initialized.");

  pinMode(redLEDpin, OUTPUT); 
  pinMode(greenLEDpin, OUTPUT);
}

void loop() {
  DateTime now = RTC.now();  // Defines the date and time at that instant
  
  delay((LOG_INTERVAL -1) - (millis() % LOG_INTERVAL));  // Delays when the board takes points
  digitalWrite(greenLEDpin, HIGH);  // Each data point collected turns on the green LED

  // Log milliseconds since starting
  uint32_t m = millis();
  logfile.print(m);
  logfile.print(", ");
#if ECHO_TO_SERIAL  // ECHO_TO_SERIAL reiterates the data being written to the file to the serial monitor
  Serial.print(m);
  Serial.print(", ");
#endif
  
  int x = analogRead(xPin);
  delay(1);
  int y = analogRead(yPin);
  delay(1);
  int z = analogRead(zPin);

  float zero_G = 512.0; // ADC is 0 ~ 1023, the zero G output
  // equals to Vs / 2

  float scale = 102.3; // Accelerometer sensitivity is 330mv/g

  logfile = SD.open("Accel_SD.csv", FILE_WRITE);

if (logfile) {
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
    logfile.print(" ");
  #if ECHO_TO_SERIAL
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
    Serial.print(" ");
  #endif
  }

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

  digitalWrite(greenLEDpin, LOW);  // Turns off green LED when the data has been written

  logfile.close();
}
```

I feel like the numbers used when determining the x, y, and z values can be changed to calibrate the accelerometer to create a localized "origin."

***Friday's task: Convert MatLab code to Python, get comfortable with Git (including creating the repo), and start looking into battery packs to power Adafruit Metro for portable accelerometer readings.***

**Friday, May 25th**

With Bellis' help, python code was created to analyze the .csv file created. Looking at the [Newton-Cotes Formulas](https://en.wikipedia.org/wiki/Newton%E2%80%93Cotes_formulas) to get an idea on how to start integrating the data to get velocity and position from acceleration.

Created code that tried to integrate data. Will find easier way to do so with Python.

Seeing if using the "WAIT_TO_SERIAL" call that would start the setup can be used to close the file manually in order to remove the SD card using [sample code from this forum](http://forum.arduino.cc/index.php?topic=43860.0) to have the call react to the input and [this one](https://stackoverflow.com/questions/23096366/how-to-stop-a-loop-arduino) to exit the loop. Bellis was able to help rearrange the code to make it actually work.

Things we learned. 

Adafruit drivers notes please! 

[Google](http://www.google.com)

* Hi
* There

*Italics*  **Bold** ***BOLD IT***

```
int x = 10;
```
