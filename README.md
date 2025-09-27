# Input-Lag-Testing
Ok, this is a current culmination of numerous different projects and works. 

Input lag testing via changes in brightness on the screen is the ideal way to test various different aspects of input lag. 4K, 120hz, VRR are best analysed with this method.

What I have tried to do is to use an off the shelf Arduino (R4 Nano - [https://docs.arduino.cc/hardware/uno-r4-wifi/](https://docs.arduino.cc/hardware/nano-r4/)) as the basis for this.
A number of different boards would likely be suitable for this project. 
I prefer the Nano R4 because 
It is relatively small. 
It is USB-C.
It has analog pins on the board and adequate overall pins. 
It has an EEPROM allowing me to save settings between power cycles. 
It has a coloured LED allowing me to communicate externally what is happening (allows independent validation on videos). 
I got serial communication working on this first. 
My first ever board was an arduino. 

Attached to this is a simple PCB. The gerber files are here.

https://oshpark.com/shared_projects/lQj04fDf

This needs four buttons, two 15P female header pin and one 2x10 female header pin soldered to it. 

This connects directly to the arduino and also a brook UFB (or similar). 

Next is the phototransistors. I will make the PCBS available once more.

https://oshpark.com/shared_projects/JK7VrIcf

The photo transistor itself really only needs 3 pins and about 10x10mm, however I have built these so that an OLED screen can clip on top (with 270 degrees of orientation available). 

The OLED I used is https://www.amazon.com.au/dp/B0D2RMQQHR?ref=ppx_yo2ov_dt_b_fed_asin_title

Of all the components, I've definitely spent the most time fighting with the OLEDs. 

To note, I've spent lots of time trying to find alternatives to the Phototransistor I started with, but have had limited success. 

I have therefore returned to Adafruit's phototransistor for all of my projects.

https://core-electronics.com.au/photo-transistor-light-sensor.html

A 50K resistor is also required. The orientation of the phototransistor is important, I will upload some images to twitter to demonstrate this. 

Now, I've spent a lot of time designing the input lag testing device so that it can work independently from a PC. Indeed, you can clip the arduino onto the brook UFB and it will be powered from there directly. 

The buttons are left, right, confirm and cancel. Confirm button will enter the mode selected. Across all modes cancel will stop any current testing. 

The modes are 
- reset = this will remove all data. Generally reset with the button on the arduino after this to fully wipe the current options
- test = this will run a single test. Results will be displayed on the OLED.
- test multiple = this will run a set number of tests in a row. Results are displayed after each test. 
- compare P1 P2 = this actually does the same as test multiple, however the display focuses on when the phototransistors responded. 
- OPT1_history = will display values read by the phototransistor for the last trial. Pushing confirm again will actually alter the result for the most recent test. 
- OPT2_history = same, but for the other phototransistor
- LOG = this will show all the results. Pushing the confirm button again will select that trial if you needed to rerecord.

  There afterwards all the timing and other options can be adjusted.

  Finally, I have included a python script that will collate all the data. All of the display settings are shown here, and can be altered across the serial communication.

  Pressing enter will save the current data, including a summary of all the phototransistor values, all of the results, a screenshot of the results and also update a .csv file with all the results collated. 


To finish, I use a 3D printed jig which interfaces with a standard ruler (300mm x 4mm x 27mm) with M3 screws holding it in place (M8 at the top). 

https://www.tinkercad.com/things/iO7gp0xDDsG-phototransistor-jig-inzone-m3?sharecode=JK81W8gAVO4LallxmTrtQG838HGUcDdwp9wht1RR6cU

I also have a sheet to make it easy to work out how far down the screen the phototransistor is. 

https://docs.google.com/spreadsheets/d/1O-7BZr7TG51Z4-GlDccAVijA5lLIsb9UZGs8u0alwic/edit?usp=sharing






