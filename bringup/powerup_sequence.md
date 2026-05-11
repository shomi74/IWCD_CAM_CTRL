# Power-up Sequence

Recommended safe order:

1. USB/Teensy only
2. Sensors/I2C validation
3. 12V motor supply with motor disconnected
4. 12V motor supply with motor connected
5. 8V camera supply with dummy load
6. 8V camera supply with camera
7. External battery path with dummy load
8. External battery path with camera
9. Full camera and motor integration

Firmware must prevent `HS1_EN` and `BATT_SW_EN` being ON at the same time.
