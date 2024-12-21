# INA219 Micropython driver

This driver is a clone of an early version of the Adafruit CircuitPython driver, when these were still readable and simple.

The only thing changed was the way of reading and writing to the I2C device.

## Class

```python
ina = INA219(i2c, *, address=0x40)
```

Create an instance of the ina219 object. 

```
Args:
  * i2c:      The I2C object used for communication.
  * address:  The I2C address. The default value is 0x40.
```

The INA219 device will be initialized with the range of 1A/32V.

## Methods and properties

### `current = ina.current`

Return the current though the shunt at the configured range.

### `bus_voltage = ina.bus_voltage`

Return the voltage between the shunt's V- connection and GND.

### `shunt_voltage = ina.shunt_voltage`

Return the voltage between the shunt's V+ and V- connections.

### `set_calibration_32V_2A()`

Set the measurement range to 32V and 2A.

### `set_calibration_32V_1A()`

Set the measurement range to 32V and 1A.

### `set_calibration_16V_400mA()`

Set the measurement range to 16V and 400mA.


## Example

```python
from machine import I2C
from ina219 import INA219
import time

# Depending on the port, the Pins for SDA and SCL must be specified.
# See the MicroPython documentation for your port.
# I2C requires pull-up resistors at SDA and SCL.

i2c = I2C(1)
ina = INA219(i2c)

set_calibration_32V_1A()

while True:
    current = ina.current
    voltage = ina.bus_voltage
    print(f"{current} mA  {voltage} V")
    time.sleep(1)
```
