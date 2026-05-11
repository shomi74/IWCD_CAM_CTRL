# Validation Test Plan

## 1. Power Rail Validation

| Test | Measurement |
|---|---|
| 12V rail under motor motion | voltage stability / ripple |
| 8V rail during camera startup | voltage droop |
| Dummy rail in DC mode | voltage at camera connector |
| Dummy rail in battery mode | voltage at camera connector |
| Battery isolation in DC mode | current into battery path |

## 2. Switching Validation

- Measure HS1_EN to NET_DUMMY_RAIL response.
- Measure BATT_SW_EN to NET_DUMMY_RAIL response.
- Verify both paths are not enabled simultaneously.
- Verify QOD/output discharge behavior.

## 3. Camera Control Validation

- Verify SSR open/short behavior.
- Verify camera ON/OFF using pulse control.
- Verify operation from 8V DC.
- Verify operation from external battery.
- Verify charging behavior through USB-C path.

## 4. Motor Validation

- Confirm coil wiring.
- Confirm step direction.
- Test slow/fast/mixed decay jumper modes.
- Measure DRV8825 temperature during operation.

## 5. Sensor Validation

- I2C scan.
- BME280 readout.
- LSM6DS3 readout.
- LIS3MDL readout.
- Proximity sensor logic state test.

## Results to Capture

- Oscilloscope plots of dummy rail switching.
- Current draw in DC and battery modes.
- Thermal image or temperature measurement of DRV8825.
- Photos of test setup.
