# Input-Lag-Testing
Ok, this is a current culmination of numerous different projects and works. 

Input lag testing via changes in brightness on the screen is the ideal way to test various different aspects of input lag. 4K, 120hz, VRR are best analysed with this method.

What I have tried to do is to use an off the shelf Arduino (R4 Uno Wifi - https://docs.arduino.cc/hardware/uno-r4-wifi/) as the basis for this.

Attached to this is one or two photo transistors PCBs. These are fairly simple builds. I have uploaded my gerber files to oshpark. 

[https://oshpark.com/orders/mVjJh4Cv](https://oshpark.com/shared_projects/BHKJZvqN) $0.60

[https://oshpark.com/orders/arRn4V5Q](https://oshpark.com/shared_projects/4ZoogtEB) $0.60

These just need some header pin, I personally use right angled 3P header pin $0.50.

And a resistor, I use 50K $0.08

https://core-electronics.com.au/photo-transistor-light-sensor.html

The phototransistor I use is the Adafruit photo transistor $2.25. I belive the Adafruit ADA2831 would be equivalent world wide. 

This is connected to the arduino via 6 dupont wires ($2.18)

Now, I have been able to connect this directly to a Brook Gen5-X board, however if you want to include some electrical isolation between the arduino and the controller, you can use something like this.

https://oshpark.com/orders/CKJCaaRW $1.33

I use three PS2501-1 optocouplers ($0.30) and three resistors 220 ohm resistors ($0.25) and 19 blocks of header pin ($0.29).

Alright, having got all the equipment together, first you need to upload the UNOR4-new sketch https://github.com/noodalls/Input-Lag-Testing/blob/main/UNOR4_new

And that's almost it!

The arduino is divide into groups of pins, and I have maintained that division. 

Pins A0-A5 are used by the Phototransistors. Easiest way to line it up is put the A2 into A2 on the arduino so the PT faces out. 

Pins 8-13 are used to output commands to your controller. If you want to use the Optocoupler PCB to isolate your controller from the arduino you can just place it on these pins. 

Pins 2-7 are pins that INPUT commands to the arduino. 

Pressing a button attached to Pins 6-7 will run one test. It will display the results when complete. 

Holding a button attached to Pins 4-5 will run multiple tests (defaults to 999 tests) and display results when released. 



You will need to find some way to hold the PTs to the area of the screen that you want to test. 

https://www.tinkercad.com/things/brewJe0tQD4-ipt-40?sharecode=aONTb_KwSj6N_fUj6CD0jxkP25zALmoeUf3MJAB_Dmg

If you have access to a 3D printer you could use something like the above file to hold them in the right locations for an Inzone M3 monitor. 

Now, when you push the test button, for the first 100ms it will determine what the normal range of brightness values are - essentially zeroing itself to the normal status of the screen.

At the 100ms mark, pins 8 and 9 will be pressed, pins 12 and 13 will be released. Pins 10 and 11 are constantly pressed. 

From 100-499ms it will look for a brightness value not seen during the registration of normal values. This can be either brighter than or darker than the normal values. Of note - if you want to you can limit it to either one of these (e.g. if you knew that you're looking for a light to dark transition you can ignore all the dark-darker transitions via a input during startup). 

As mentioned, if button connceted to 6+7 is pressed this is a single trial this result will be shown immediately. 

If this is multiple trials by holding a button over pins 4+5, it will store the results until a summary is shown on button release. 

There are some other display features that are going on while this is happening. 

Firstly there is an LED that corresponds to what pin 13 is doing. This means that when pins 8 and 9 are activated (and conversley 12 and 13 are released) the LED will light up. The oppositve is also true. 


The arduino has an LED display of 8 rows of 12 leds. We can use this to display what is happening more meaningfully. 

For a single test - 

The first row will show the current brightness. The top rows is tens and the bottom row is ones. So 57 would appear as
00000.......
0000000.....
These values range from 0-127, which matches nicely with the LEDs range.

Rows 2 and 3 show the minimum value found.
Rows 4 and 5 show the maximum value found.

These will work when the button attached to pins 6 and 7 isn't pressed. When it is pressed, the min and max values will reset. 

From here 

### will come back to this!





