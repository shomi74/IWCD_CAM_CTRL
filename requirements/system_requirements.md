# System Requirements — IWCD_CAM_CTRL

## Purpose

Design a compact embedded camera control and power board for the IWCD photogrammetry camera system.

## Functional Requirements

1. Accept 12V input from CM5 carrier board for motor driver supply.
2. Accept 8V input from CM5 carrier board for camera DC operation.
3. Accept external Sony battery input.
4. Route either 8V DC or external battery to camera dummy-battery rail.
5. Allow external battery to be connected bidirectionally for battery operation and camera-based charging.
6. Provide electronic camera ON/OFF switch control through isolated dry-contact interface.
7. Drive a 4-wire bipolar stepper motor.
8. Read 12V Hall-effect proximity/home sensor safely using 3.3V MCU logic.
9. Read environmental/motion sensors over I2C.
10. Monitor key voltage rails through ADC dividers.

## Electrical Requirements

| Rail | Purpose |
|---|---|
| 12V | DRV8825 motor supply |
| 8V | Camera dummy-battery DC input |
| External battery | Sony battery externalized outside camera compartment |
| 3.3V | Teensy logic and sensors |

## Mechanical Requirements

- Board must fit inside constrained underwater camera housing.
- Avoid bulky screw terminals where possible.
- Use locking JST-style connectors.
- Place connectors for practical cable mating and serviceability.

## Safety / Control Requirements

- 8V path and battery path must not be enabled simultaneously.
- Camera switch control should be isolated from board ground.
- External battery path must be isolatable in DC operation mode.
- Power rails must be testable during bring-up.
