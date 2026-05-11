# System Architecture

## High-Level Concept

The IWCD camera control architecture separates compute, control, and power switching.

```text
CM5 Carrier Board
  ├── USB2 -> Teensy 4.0
  ├── 8V -> TPS22810 high-side switch -> dummy battery rail
  └── 12V -> DRV8825 motor driver

External Sony Battery
  └── Bidirectional P-MOSFET switch -> dummy battery rail

Teensy 4.0
  ├── Controls 8V high-side switch
  ├── Controls battery bidirectional switch
  ├── Controls camera switch SSR
  ├── Controls DRV8825 stepper driver
  ├── Reads proximity sensor
  ├── Reads I2C sensors
  └── Reads rail voltages through ADC dividers
```

## Key Design Decision

The original ideal-diode / one-way power mux concept was replaced with a bidirectional battery switch. This is required because the external Sony battery must both:

1. power the camera, and
2. receive charging current through the camera dummy-battery interface.

## Power Path Summary

| Mode | 8V HS Switch | Battery Switch | Camera Switch | Result |
|---|---:|---:|---:|---|
| Charging | OFF | ON | OFF | Camera USB-C charges external battery |
| Battery operation | OFF | ON | ON/pulse | Battery powers camera |
| DC operation | ON | OFF | ON/pulse | CM5 8V powers camera |

## Noise Partitioning

- Motor driver and motor connector are treated as noisy/high-current zone.
- Sensors and I2C bus are treated as quiet zone.
- Solid inner GND plane provides return current control.
- High-current camera and motor traces are routed wider than logic signals.
