# Getting Started

1. **Connect the antenna.** Fit an active GNSS antenna to the U.FL connector RF1 (power off). The board supplies the antenna bias through L2 / R4.
2. **Wire the host.** Header H2 (2 × 5, 2.54 mm): pin 5 UART_TX → host RX, pin 7 UART_RX ← host TX, pin 9 GND, pin 1 VIN (3.3–5.5 V). The BMM350 magnetometer uses pins 6 / 8 / 10 (SCK, SDA, INT) on I²C.
3. **Use 3.3 V logic.** The NEO-M9N UART is 3.3 V; do not connect 5 V logic signals. Default UART1 setting is 38400 baud, NMEA output.
4. **Run the tests.** The [GNSS Receiver Test Tool](../tests/01-gnss-test-tool/README.md) checks the receiver from a Windows PC; the full procedure and acceptance limits are in its [guide](../tests/01-gnss-test-tool/SaturnVex_GPS_M9N_Test_Tool_Guide_EN.pdf). The [BMM350 test](../tests/02-bmm350-i2c/README.md) reads the magnetometer from a microcontroller over I²C.

[← Product home](../README.md)
