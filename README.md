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
For boiler control, i am replacing the boiler coffee thermostat with a M4 PT100 3-wire thermocouple. To read the PT100 i am using a MAX31865 board with SPI communication. This is connected to the main controller over the SPI bus.

Thermostat power terminals are connected to a SSR 40-DA, solid state relay with zerocross function. This is important to ensure a smooth on and off to the boiler. SSR is driven by a esp relay board without the relay ( XD ) just because i was too lazy to do a proper driver with a transistor. Controller is driving that relay board with a slow PWM, controlling the SSR. The PWM value is set by a PID controller running in controller software.

Like the thermostat, boiler control is always ON since the machine is turned on.

### Pump Control
For pump control, i am not replacing anything of stock machine but adding things. First i am controlling the pump by pressure. I installed a pressure transducer 300 PSI after the pumo outlet. I disconnected the pump hose and installed a 3 way connector, with a hose that runs to the pressure transducer. Pressure sensor gives analog signal, which i read with an external ADS1115 board with i2c communication. I am not using the esp8266 adc, because ads1115 is faster, more accurate and gives you 4 ports for future expansion. I connected the ADS1115 to same i2c bus that connects the OLED screen.



I installed a Triac based controller board (Robotdyn AC dimmer 8A 400V) between the power line and pump. Triac is fired by the controller
