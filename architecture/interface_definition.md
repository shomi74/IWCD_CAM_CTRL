# Electrical Interface Definition

## Connectors

| Connector | Function | Selected Connector | Notes |
|---|---|---|---|
| J1 | 12V input from CM5 | Barrel jack / project-specific | Motor supply input |
| J2 | 8V input from CM5 | Barrel jack / project-specific | Camera DC supply input |
| J3 | External Sony battery input | Barrel jack / project-specific | Battery source |
| J4 | Camera switch | JST PH S2B-PH-K-S | Low-current switch leads |
| J5 | Dummy battery output | JST VH B2PS-VH | Camera power output |
| J6 | Proximity sensor | JST PH S3B-PH-K-S | 12V/GND/open-collector output |
| J7 | Stepper motor | JST VH B4PS-VH | 4-wire bipolar motor |

## Control Signals

| Signal | Direction | Purpose |
|---|---|---|
| HS1_EN | Teensy -> TPS22810 | Enables 8V camera DC path |
| BATT_SW_EN | Teensy -> 2N7002/AO4805 | Enables bidirectional battery path |
| CAM_SW_CTRL | Teensy -> AQY212 | Simulates camera ON/OFF switch |
| MOTOR_STEP | Teensy -> DRV8825 | Step input |
| MOTOR_DIR | Teensy -> DRV8825 | Direction input |
| MOTOR_EN_n | Teensy -> DRV8825 | Active-low motor enable |
| MODE0/1/2 | Teensy -> DRV8825 | Microstepping selection |
| HOME_SW_IN | Sensor -> Teensy | Proximity/home sensor input |
| MOTOR_nFAULT | DRV8825 -> Teensy | Fault status |
| MOTOR_nHOME | DRV8825 -> Teensy | Home/index status |

## Voltage Monitoring

| Signal | Source | Purpose |
|---|---|---|
| V_8V_SENSE | 8V rail divider | Detect 8V presence |
| V_BATT_SENSE | battery divider | Monitor external battery |
| V_DUMMY_SENSE | dummy rail divider | Monitor camera power rail |
