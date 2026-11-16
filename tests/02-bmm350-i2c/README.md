# BMM350 Magnetometer (I²C) Test

**Board:** `SVX-GPS-M9N-001` · **Sensor:** Bosch BMM350 three-axis magnetometer · **Host:** microcontroller with I²C (reference: `SVX-MCU-STM32G474-001`)

Verifies the BMM350 on this board: I²C communication, sensor initialization, three-axis magnetic-field readings and the data-ready interrupt (INT). The BMM350 is not reachable from a PC USB-UART adapter, so the test runs on a host microcontroller.

## Reference code

The communication code is the SaturnVex STM32G474 BMM350 example. Use its guide and STM32CubeIDE project without changes:

- [SVX-MCU-STM32G474-001 · Test 08 — BMM350 I2C2 Magnetometer](https://github.com/SaturnVex/SVX-MCU-STM32G474-001/tree/main/tests/08-bmm350-i2c2)
- [Test guide (PDF)](https://github.com/SaturnVex/SVX-MCU-STM32G474-001/blob/main/tests/08-bmm350-i2c2/SaturnVex_STM32G474_BMM350_Test_Guide_EN.pdf)
- [STM32CubeIDE source project (ZIP)](https://github.com/SaturnVex/SVX-MCU-STM32G474-001/raw/main/tests/08-bmm350-i2c2/STM32G474_BMM350_I2C2_SaturnVex.zip)

The project uses the Bosch BMM350 SensorAPI with a HAL I²C port layer (`bmm350_port.c`), probes I²C addresses 0x14 / 0x15, enables the data-ready interrupt and reads the sensor at 25 Hz. The port layer can be reused on other microcontrollers by replacing the I²C read / write and delay functions.

## Connections

| SVX-GPS-M9N-001 header H2 | Signal | SVX-MCU-STM32G474-001 |
|---|---|---|
| 6 | BMM_SCK (I²C SCL) | I2C2_SCL — PA9 |
| 8 | BMM_SDA (I²C SDA) | I2C2_SDA — PA8 |
| 10 | BMM_INT (data ready) | IO_4 — PB6 (EXTI6) |
| 9 (or 2) | GND | GND |
| 1 (or 3) | VIN, 3.3–5.5 V | 3.3 V or 5 V supply |

- The BMM350 runs from the board's 3.3 V / 1.8 V regulators; SCK, SDA and INT have 3.3 V pull-ups on the board. Use a 3.3 V logic host.
- ADSEL is tied to GND, so the 7-bit I²C address is **0x14**.
- The GNSS UART (pins 5 / 7) is independent and can be tested at the same time with [Test 01](../01-gnss-test-tool/README.md).

## Run this test

1. Power off both boards and make the connections above with short wires.
2. Import, build and flash the STM32G474 BMM350 project as described in its guide.
3. Open a 115200-baud terminal on the STM32G474 USART2 (PB3 TX).
4. Check the output against the acceptance criteria below.

## Acceptance

Example output (field values depend on orientation and the magnetic environment):

```
=== STM32G474 BMM350 I2C2 ===
I2C2 SCL=PA9 SDA=PA8; BMM INT=PB6 (IO_4)
I2C device ACK at 0x14
BMM350 init result = 0
BMM350 X/Y/Z (milli-uT): 51122 -30305 27500  reads=25 errors=0 INT=25
```

**PASS:** ACK at 0x14, `init result = 0`, X/Y/Z values change when the board is rotated, `errors=0`, and about 25 data-ready interrupts per second.

The STM32G474 project keeps its own licenses: SaturnVex files under BSD-3-Clause, Bosch BMM350 SensorAPI (BSD-3-Clause), STMicroelectronics HAL and Arm CMSIS under their own terms.

[← All tests](../README.md) · [← Product home](../../README.md)
