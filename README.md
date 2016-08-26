# Measuring temperature using an 1-wire temperature sensor using a Riffle

<img src="pics/one_wire_pic.png" width=400>

## 1-wire basics

The [1-wire](https://en.wikipedia.org/wiki/1-Wire) protocol allows for sensor readings to be retrieved using only a single signal line, along with power and ground lines.  Some 1-wire sensor variants also allow the signal line to serve as the power line, reducing the number of needed signal lines to two. It is a bus protocol, allowing more than one device to be connected in parallel; every 1-wire sensor has a unique identifier, so many can be placed on the same bus, spanning several meters of wire length. 

1-wire devices require that specialized code be loaded onto an Arduino or Riffle in order to allow for sensor readings.  Usually this is accomplished by loading a dedicated 1-wire library onto the microcontroller.  We'll be doing that in the guide below. 

## 1-wire temperature sensors.

1-wire temperature sensors are in wide use, as they are simple to use, and the bus configuration allows for many temperature sensors to be used at once, making e.g. distributed temperature measurements over an area.

We'll be using a waterproof version of the DS18B20, a popular 1-wire temperature sensor that comes in several varieties. Any chip or sensor labeled 'DS18B20' should work just as well.  

## i2c Circuit

As described above, we'll simply be connecting the 1-wire power and ground lines to the 3.3V and GND lines on the Riffle; we can connect the 1-wire signal line to any digital pin.

For 1-wire bus systems on 3.3V microcontrollers, a 4.7K 'pullup resistor' is required on the signal line -- i.e., we need to connect  the signal line to 3.3V via a 4.7K resistor.

<img src="pics/one_wire_schem.png">

## i2c Sensor connected to a Riffle Protoboard

Below is a picture of a simple voltage divider setup on the Riffle Protoboard which matches the schematic shown above.  Note that there is no 'polarity' to the thermistor, so either wire works in either position.  Also note that the 'columns' of pins on the Riffle Protoboard, as shown, are connected electrically by small traces -- this is what allows us to connect e.g. the red power line to one end of the resistor R1 by simply having the wires located in the same column.  

<img src="pics/one_wire_proto.png">

## Code for i2c Temperature Sensor Datalogging with a Riffle

The Arduino code [riffle_thermistor.ino] in this repository will measure temperature using analog pin A0 on the Riffle, and record it to a microSD card along with a timestamp. 

The data is output in "TSV" format, with tabs separating columns of data (timestamp in the first column, RTC temperature in the second column, thermistor temperature in the third column).



