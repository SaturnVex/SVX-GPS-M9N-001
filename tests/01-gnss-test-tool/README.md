# GNSS Receiver Test Tool

**Board:** `SVX-GPS-M9N-001` · **Receiver:** u-blox NEO-M9N · **PC:** Windows 10 / 11 with a 3.3 V USB-UART adapter

Command-line tool that reads the NMEA and UBX output of the NEO-M9N over UART and shows fix status, position, DOP, accuracy estimates, satellites per constellation with C/N0, TTFF (cold / warm / hot start) and position stability (CEP50, CEP95, 2DRMS). Every epoch is logged to a CSV file.

## Files

- [Test setup, connections, commands and acceptance guide (PDF)](SaturnVex_GPS_M9N_Test_Tool_Guide_EN.pdf)
- [Test package (ZIP)](GPS_M9N_Test_Tool_SaturnVex.zip?raw=true)

## Run this test

1. Read the PDF guide and wire header H2 to a 3.3 V USB-UART adapter (TX → RX, RX → TX, GND, VIN). Connect an active GNSS antenna to the U.FL connector.
2. Download and extract `GPS_M9N_Test_Tool_SaturnVex.zip` on the PC.
3. Run `setup.bat` once (Python check and offline pyserial install), then `run.bat` with the antenna under open sky.
4. Verify the results using the PDF acceptance criteria and record them in the test record.

SaturnVex files are provided under the BSD-3-Clause license (`LICENSE.txt`). Python and the bundled pyserial wheel keep their own licenses (`NOTICE.txt`).

[← All tests](../README.md) · [← Product home](../../README.md)
