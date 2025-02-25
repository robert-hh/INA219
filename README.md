# INA219 MicroPython driver

This driver is a clone of an early version of the Adafruit CircuitPython driver, when these were still readable and simple.

The only thing changed was the way of reading and writing to the I2C device.

## Class

```python
ina = INA219(i2c, *, addr=0x40)
```

Create an instance of the ina219 object. 

```
Args:
  * i2c_device: The I2C object used for communication.
  * addr:       The I2C address. The default value is 0x40 (with pin configuration A0=A1=GND).
```

The INA219 device will be initialized with the range of 1A/32V.

## Methods and properties

### `current_mA: float = ina.current`

Return the current (in mA) though the shunt at the configured range.

Assumes the shunt resistance is 0.1 ohm.

### `bus_voltage_V: float = ina.bus_voltage`

Return the voltage (in volts) between the shunt's V- connection and GND.

### `shunt_voltage_V: float = ina.shunt_voltage`

Return the voltage (in volts) between the shunt's V+ and V- connections.

### `set_calibration_32V_2A()`

Set the measurement range to 32V (max bus voltage) and 2A (max current, assuming a 0.1 ohm shunt resistor).

### `set_calibration_32V_1A()`

Set the measurement range to 32V (max bus voltage) and 1A (max current, assuming a 0.1 ohm shunt resistor).

### `set_calibration_16V_400mA()`

Set the measurement range to 16V (max bus voltage) and 400mA (max current, assuming a 0.1 ohm shunt resistor).

In this mode, the maximum shunt voltage is 40mV.

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
    current_mA = ina.current
    voltage_V = ina.bus_voltage
    print("{} mA  {} V".format(current_mA, voltage_V))
    time.sleep(1)
```
