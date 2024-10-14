# e-paper-display-forHomeassistant
Files to configure a Waveshare 7.5" Display with Homeassistant.
This dashboaed is based on the great work of Markus Hottenrott https://www.it-adviser.net/home-assistant-75-e-paper-display-waveshare-mit-esphome-ansteuern-wetterstation/

![Waveshare e-Paper Display](https://github.com/mtbsteve/e-paper-display-forHomeassistant/blob/main/IMG_1116.jpg)

Required components:
- Waveshare 7.5" e-paper display
- Waveshare ESP32 Display driver
- A 13x18cm picture frame

You can purchase the Waveshare components at eg Amazon. Please notice that there are different versions available.
I ordered the V3 version which supports 3 colors (white/black/red). Unfortunately, if you try to use the red color, the refresh times raise up to 20 seconds with the current ESPhome drivers. You may check the developers discussion at: https://github.com/esphome/feature-requests/issues/239 for the latest status.

Steps to install:
1. make sure you have ESPhome installed in HA
2. Flash and add the ESP32 as described here: https://esphome.io/guides/getting_started_hassio.html
3. Install fonts. The display uses Google Gotham Rounded Font for text and Material Design Icon Font for the glyphs. Copy the font files into:  "config\esphome\fonts"
   Get the Book version here: https://fontsgeek.com/fonts/Gotham-Book
   Get the Bold version here: https://fontsgeek.com/fonts/Gotham-Rounded-Bold
   Get the Medium version here: https://fontsgeek.com/fonts/Gotham-Rounded-Medium
5. Add the template in the config/configuration.yaml file in your HA installation
6. Add the sensor.yaml file to your config/configuration.yaml file in your HA installation
7. Copy the epaper75_V2.yaml configuration file into the config/esphome directory.
8. In the ESPhome addon in HA, add the epaper75_V2.yaml integration by using the "Add Integration" button

Note that all sensors implemented in the epaper75_V2.yaml file need to be adapted to your configuration since I am referring to the following HA addons in my home:
- Tibber
- EMS-ESP (Bosch/Buderus heatpumps)
- Solaredge ModbusMulti
- SolaredgeCloud
- Solcast PV forecast
- and the default HA Weather Services (Meteorologisk institutt (Met.no))

Next Steps to implement:
- sleep mode, refresh only if data changes
- explore color options
