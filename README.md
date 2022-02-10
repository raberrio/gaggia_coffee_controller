# gaggia_coffee_controller
This is my personal approach to make a controller for Gaggia Classic coffee machine. I have designed it from scratch integrating standard parts that can be found online. It main goal is to control boiler temperature and pump pressure, but actually i am adding more features as i have the time to implement it.

# The Basics
Here i will describe how this thing works, what i use and why.
## Software
The software is written in a yaml file which uses the ESPHOME platform. It is a really straightforward and easy tool to work with. I understand that maybe its better for control applications to program at low level but this thing is simple and works really well.

Also i am using Homeassistant in my home, i designed the UI there so i can access through my phone, tablet, pc or whatever. I use graphana plugins to analyze data if i need (tuning controllers or checking new features) and influxDB to store data.

## Hardware
As i decided to use esphome, i started using a WEMOS D1 MINI board with a ESP8266 chip. The rest of the hardware were been selected based on if it were supported in esphome or not.

### Core controller
For core controller i choosed a WEMOS D1 mini board. For display data, i am using a 0,96 dual color OLED screen with SSD1306 chip, i2c bus communication. Main power is provided by a HiLink 220V to 5VDC box with is connected to wemos usb port (it did not support direct power pin connection).

### Boiler control
