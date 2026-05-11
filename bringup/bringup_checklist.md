# Bring-up Checklist

## Before Power

- [ ] Visual inspection under microscope
- [ ] Check solder bridges around fine-pitch sensors and DRV8825
- [ ] Verify connector polarity
- [ ] Verify battery input polarity
- [ ] Verify dummy battery output polarity
- [ ] Check resistance from each power rail to GND
- [ ] Confirm no short between 8V and battery rail

## USB / Logic Bring-up

- [ ] Connect Teensy through USB only
- [ ] Confirm Teensy enumerates
- [ ] Confirm +3V3 rail
- [ ] Scan I2C bus
- [ ] Read BME280
- [ ] Read LSM6DS3
- [ ] Read LIS3MDL

## 12V / Motor Bring-up

- [ ] Apply 12V with current-limited supply
- [ ] Confirm DRV8825 VM voltage
- [ ] Confirm VREF voltage
- [ ] Confirm no overheating
- [ ] Test motor at low speed/current
- [ ] Verify direction and coil mapping

## 8V / Camera Power Bring-up

- [ ] Apply 8V with current limit
- [ ] Keep BATT_SW_EN OFF
- [ ] Toggle HS1_EN
- [ ] Measure NET_DUMMY_RAIL
- [ ] Confirm QOD/output discharge behavior

## Battery Path Bring-up

- [ ] Connect external battery through current-limited setup if possible
- [ ] Keep HS1_EN OFF
- [ ] Enable BATT_SW_EN
- [ ] Measure NET_DUMMY_RAIL
- [ ] Verify bidirectional path behavior

## Camera Interface Bring-up

- [ ] Test AQY212 SSR without camera first
- [ ] Verify open/short behavior on CAM SW connector
- [ ] Connect camera switch leads
- [ ] Test momentary ON/OFF pulse
- [ ] Test camera operation from 8V path
- [ ] Test camera operation from battery path
- [ ] Test camera USB-C charging behavior
