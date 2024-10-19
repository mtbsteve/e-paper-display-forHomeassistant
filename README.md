# e-paper-display-forHomeassistant
Files to configure a Waveshare 7.5" Display with Homeassistant.
This dashboaed is based on the great work of Markus Hottenrott https://www.it-adviser.net/home-assistant-75-e-paper-display-waveshare-mit-esphome-ansteuern-wetterstation/ and the work of trip5 https://github.com/trip5/ESPHome-eInk-Boards/tree/main

Version 3 of the yaml file adds 3 colors (black, white, red) and battery power supply. Furthermore the display update can be externally triggered from Homeassistant, eg. by using a motion sensor.

![Waveshare e-Paper Display](https://github.com/mtbsteve/e-paper-display-forHomeassistant/blob/main/IMG_1116.jpg)

Required components:
- Waveshare 7.5" e-paper display
- Waveshare ESP32 Display driver
- A 13x18cm picture frame, best is the IKEA Rödalm frame
- Optional: a motion sensor like from Sonoff (Amazon)

You can purchase the Waveshare components at eg Amazon. Please notice that there are different versions available.
I ordered the V3 version which supports 3 colors (white/black/red). Unfortunately, if you try to use the red color, the refresh times raise up to 10 seconds with the current ESPhome drivers. You may check the developers discussion at: https://github.com/esphome/feature-requests/issues/239 for the latest status. V3 of the yaml has the red color implemented, it works, but requires a longer refresh time.

Steps to install:
1. make sure you have ESPhome installed in HA
2. Flash and add the ESP32 as described here: https://esphome.io/guides/getting_started_hassio.html
3. Install fonts. The display uses Google Gotham Rounded Font for text and Material Design Icon Font for the glyphs. Copy the font files into:  "config\esphome\fonts"
   Get the Book version here: https://fontsgeek.com/fonts/Gotham-Book
   Get the Bold version here: https://fontsgeek.com/fonts/Gotham-Rounded-Bold
   Get the Medium version here: https://fontsgeek.com/fonts/Gotham-Rounded-Medium
5. Add the template in the config/configuration.yaml file in your HA installation
6. Add the sensor.yaml file to your config/configuration.yaml file in your HA installation
7. Copy the epaper75_V2.yaml configuration file or the V3 config file into the config/esphome directory.
8. In the ESPhome addon in HA, add the epaper75_V2.yaml integration (or V3) by using the "Add Integration" button

For the glyphs codes, you may use this overview: https://pictogrammers.github.io/@mdi/font/6.5.95/
Note that all sensors implemented in the epaper75_V2.yaml file need to be adapted to your configuration since I am referring to the following HA addons in my home:
- Tibber
- EMS-ESP (Bosch/Buderus heatpumps)
- Solaredge ModbusMulti
- SolaredgeCloud
- Solcast PV forecast
- and the default HA Weather Services (Meteorologisk institutt (Met.no))

For battery power supply, I am using 3x1.5V AA Lithium non-rechargable batteries which fit nicely on the back of the frame.  
For the voltage measurement, I am using the built-in DAC of the ESP32. The input for the DAC is 3.3V, if you use 3x1.5V batteries you need to add a voltage divider.
I am using a 100k Ohm resistor solderd between the DAC pin and ground, and a 6K Ohm resistor soldered between the 5V input pin and the DAC pin.
Depending on your power source of choice, you may need to adjust the resistor values accordingly and adjust the scaling factor as documented in the yaml accordingly.
In addition to stabilize the battery I added a 1000uF capacitor between 5V input and ground.



Next Steps to implement:
- sleep mode, refresh only if data changes
- explore NiMh rechargeable battreries
