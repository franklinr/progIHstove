# Programmable Induction (IH) Stove

<img src="https://github.com/franklinr/progIHstove/blob/e387c80c00e89c76ea5ebb6e7dbc109dc4d39371/img/stove.JPG" width="50%">

I wanted a programmable stove that could be used for multiple functions.  Most rice cookers are designed for white rice and brown rice requires a little bit longer cooking, so I wanted a stove that could have a special brown rice cooking function.  I also boil water multiple times a day, but I didn't want electric kettle just for that one function.  So I create a programmable induction stove using a simple one burner IH stove and an ESP32 controller.

I selected a IH stove with simple set of buttons that directly controlled each function. 

<img src="https://github.com/franklinr/progIHstove/blob/e387c80c00e89c76ea5ebb6e7dbc109dc4d39371/img/inside.JPG" width="50%">

I connect each button on the stove's green control board to a [5V module with 4 relays](https://www.amazon.co.jp/-/en/ELEGOO-Relay-Arduino-MEGA-STM32/dp/B0718WX35W). 

<img src="https://github.com/franklinr/progIHstove/blob/e387c80c00e89c76ea5ebb6e7dbc109dc4d39371/img/usb.JPG" width="50%">

It was possible to power the relays from the internal power of the stove, so I added a separate USB power input using a usb connector that I had.

If you connect the ESP32 to the relays, then toggling the relays will often reset the ESP32.  To understand it, read [this](https://forum.arduino.cc/t/rc-snubber-on-relay-controlling-motorized-ball-valves/964863/9).  The solution is to disconnect the jumper and make sure that ground of ESP32 is not connect to the relay GND, as shown [here by Paul B](https://forum.arduino.cc/t/rc-snubber-on-relay-controlling-motorized-ball-valves/964863/9). 

<img src="https://github.com/franklinr/progIHstove/blob/e387c80c00e89c76ea5ebb6e7dbc109dc4d39371/img/jumper.JPG" width="50%">

The USB 5V is connected to the JD-VCC at the jumper and USB GND is connected to the relay GND.
