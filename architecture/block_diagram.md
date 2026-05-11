# Block Diagram

```text
            +-------------------+
            |   CM5 Carrier     |
            | USB2 / 8V / 12V   |
            +---+----------+----+
                |          |
              USB2        8V ----------------+
                |                             |
        +-------v------+              +-------v-------+
        |  Teensy 4.0  |--HS1_EN----->| TPS22810 HS   |
        | Control MCU  |              | 8V Switch     |
        +---+---+---+--+              +-------+-------+
            |   |   |                         |
            |   |   |                         v
            |   |   |                 +---------------+
            |   |   +--CAM_SW_CTRL--->| AQY212 SSR    |
            |   |                     | Camera Switch |
            |   |                     +---------------+
            |   |
            |   +--BATT_SW_EN---> +------------------------+
            |                     | Back-to-back P-MOSFET  |
            |                     | Bidirectional Battery  |
            |                     +-----------+------------+
            |                                 |
            |                                 v
            |                          NET_DUMMY_RAIL
            |                                 |
            |                                 v
            |                        Camera Dummy Battery
            |
            +--STEP/DIR/EN----> DRV8825 ----> Stepper Motor
            |
            +--I2C------------> BME280 / LSM6DS3 / LIS3MDL
            |
            +--HOME_SW_IN<---- Proximity Sensor Interface
```
