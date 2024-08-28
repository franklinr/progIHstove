# Programmable Induction (IH) Stove

<img src="https://github.com/franklinr/progIHstove/blob/e387c80c00e89c76ea5ebb6e7dbc109dc4d39371/img/stove.JPG" width="50%">

I wanted a programmable stove that could be used for multiple functions.  Most rice cookers are designed for white rice and brown rice requires a little bit longer cooking, so I wanted a stove that could have a special brown rice cooking function.  I also boil water multiple times a day, but I didn't want electric kettle just for that one function.  So I create a programmable induction stove using a simple one burner IH stove and an ESP32 controller.

I selected a IH stove with simple set of buttons that directly controlled each function [Iris OHYAMA IH Stove 1000W IHK-T32](https://www.amazon.co.jp/IRIS-OHYAMA-stove-1000W-IHK-T32-B/dp/B017YARIXA). It has buttons for ON, OFF, HIGHER HEAT, and LOWER HEAT (there is also a button for keeping oil at a fixed temperature during deep frying).  I connect each button on the stove's green control board to a [5V module with 4 relays](https://www.amazon.co.jp/-/en/ELEGOO-Relay-Arduino-MEGA-STM32/dp/B0718WX35W). 

<p float="left">
<img src="https://github.com/franklinr/progIHstove/blob/2586dcae3c2a910aae263b45e9cf32c4718fc44b/img/inside.JPG" width="20%">
<img src="https://github.com/franklinr/progIHstove/blob/9e98dde0bea082a2186d8779b2eb4c8dfe6418aa/img/usb.JPG" width="20%">
<img src="https://github.com/franklinr/progIHstove/blob/9e98dde0bea082a2186d8779b2eb4c8dfe6418aa/img/jumper.JPG" width="20%">
</p>

It was possible to power the relays from the internal power of the stove, so I added a separate USB power input using a usb connector that I had.  

My ESP32 is compatible with WROOM-32, so this figure is very helpful.
<img src="https://github.com/franklinr/progIHstove/blob/2586dcae3c2a910aae263b45e9cf32c4718fc44b/img/inside.JPG" width="20%">

If you connect the ESP32 to the relays, then toggling the relays will often reset the ESP32.  To understand it, read [this](https://forum.arduino.cc/t/rc-snubber-on-relay-controlling-motorized-ball-valves/964863/9).  The solution is to disconnect the jumper and make sure that ground of ESP32 is not connect to the relay GND, as shown [here by Paul B](https://forum.arduino.cc/t/rc-snubber-on-relay-controlling-motorized-ball-valves/964863/9). The USB 5V is connected to the JD-VCC at the jumper and USB GND is connected to the relay GND.  Here are the pins on the ESP32 that are used to control the relay.
const int RELAY1LOWER = 15;  
const int RELAY2RAISE = 2;   
const int RELAY3ON = 4;      
const int RELAY4OFF = 16;  

I had a [Kuzyatech Sharp Memory Display](http://kuzyatech.com/sharp-memory-lcd-breakout-a2) laying around that I decided to use for the display. 
  I used these connections to the ESP32 pins.
#define SHARP_SCK 32   
#define SHARP_MOSI 33  
#define SHARP_SS 25    
#define EXTCOMIN 26    
#define DISP 27        
#define EXTMODE 14     
#define DISPGND 12     
#define DISPVIN 13    

I connected two pushbuttons to 34 and 35.  There is an extra LED that is used to illuminate the screen that is connected to 23.
const int BUTTON1 = 35;      
const int BUTTON2 = 34;      
const int DISPLAYLED = 23;
