# IWCD_CAM_CTRL

## IWCD Camera Control and Power Board

Embedded camera control and power-management platform developed for the IWCD / Hyper-K photogrammetry imaging infrastructure.

The project implements a distributed embedded control architecture intended to replace legacy long-distance USB/HDMI extender-based imaging systems with a more reliable local embedded compute and supervisory-control solution.

The board is designed to operate inside a constrained underwater detector enclosure where:
- remote operation is required
- connector accessibility is limited
- long cable runs are undesirable
- power integrity and grounding are critical
- reliable deployment is necessary

---

# Project Overview

The IWCD_CAM_CTRL board acts as the hardware control and power-management interface between:

- CM5 embedded compute platform
- Teensy 4.0 supervisory controller
- Sony A7R IV camera dummy-battery interface
- external Sony battery
- stepper motor subsystem
- proximity/home sensor
- environmental and motion sensors

The system integrates:
- camera power-path management
- remote camera ON/OFF control
- stepper motor control
- sensor acquisition
- embedded supervisory logic
- deployment-oriented connector infrastructure

The project is being developed using an industrial-style hardware workflow covering:
- requirements definition
- system architecture
- schematic capture
- PCB layout
- manufacturing preparation
- bring-up planning
- validation methodology
- deployment considerations

---

# Main Design Goals

## 1. Embedded Architecture Migration

Replace unreliable long-distance USB/HDMI extender infrastructure with:
- embedded compute
- local hardware control
- distributed instrumentation architecture

This reduces:
- cable complexity
- extender reliability issues
- long-distance signal integrity problems

while improving:
- deployment reliability
- serviceability
- modularity
- embedded control capability

---

## 2. Camera Power Management

Provide controlled camera operation using either:
- regulated 8V DC supplied from CM5-side infrastructure
- external Sony battery

The architecture supports controlled power-path selection using embedded logic and switching circuitry.

---

## 3. Battery Charging Support

Allow charging of the external Sony battery through the camera/dummy-battery interface path when enabled.

The design supports:
- external battery operation
- external battery charging
- DC-powered operation

without manual rewiring.

---

## 4. Remote Camera Control

Provide electronic ON/OFF and shutter control of the Sony A7R IV using:
- PhotoMOS relay interface
- dry-contact emulation
- embedded GPIO control

This allows remote operation without mechanical interaction with the camera body.

---

## 5. Motion and Sensor Integration

Integrate:
- bipolar stepper motor control
- proximity/home sensing
- environmental sensing
- orientation and IMU sensing

inside the same embedded control platform.

---

## 6. Industrial Hardware Workflow

Develop the project using a workflow suitable for:
- fabrication
- assembly
- bring-up
- debugging
- validation
- deployment
- future revision management

The repository structure is intended to reflect the complete hardware product-development lifecycle, not just PCB files.

---

# System Architecture

The platform is divided into multiple functional subsystems.

| Subsystem | Description |
|---|---|
| Embedded Control | Teensy-based supervisory controller |
| Compute Layer | CM5 embedded compute integration |
| Camera Power Path | 8V DC and external battery switching |
| Camera Control | SSR-based electronic switch interface |
| Motion Control | DRV8825 stepper motor subsystem |
| Sensor Subsystem | Environmental + IMU + magnetometer |
| Deployment Interface | External connectors and wiring infrastructure |

---

# Embedded Control Architecture

A Teensy 4.0 acts as the primary embedded supervisory controller.

The Teensy manages:
- power switching logic
- sensor acquisition
- motor control signals
- camera switch control
- safety interlocks
- operational state management

The controller interfaces with:
- sensor subsystem
- motor driver
- camera control circuitry
- power switching subsystem
- external deployment connectors

---

# Camera Power Architecture

The board supports multiple operating modes using controlled power-path switching.

The power architecture combines:
- regulated 8V DC input
- external Sony battery input
- dummy battery interface
- controlled switching logic

to create a flexible camera power-management system.

---

# Operating Modes

## 1. Charging Mode

### Control State

```
HS1_EN       = OFF
BATT_SW_EN   = ON
CAM_SW_CTRL  = OFF
```

### External Condition

```
USB-C connected to camera
```

### Power Path

```
USB-C
  -> camera internal charger
      -> dummy battery rail
          -> bidirectional battery switch
              -> external Sony battery
```

### Purpose

Allows charging of the external Sony battery through the camera charging path.

---

## 2. Battery Operation Mode

### Control State

```
HS1_EN       = OFF
BATT_SW_EN   = ON
CAM_SW_CTRL  = ON / pulse
```

### Power Path

```
External Sony battery
  -> bidirectional battery switch
      -> dummy battery rail
          -> camera
```

### Purpose

Allows the camera to operate directly from the external Sony battery.

---

## 3. DC Operation Mode

### Control State

```
HS1_EN       = ON
BATT_SW_EN   = OFF
CAM_SW_CTRL  = ON / pulse
```

### Power Path

```
8V from CM5 infrastructure
  -> high-side switch
      -> dummy battery rail
          -> camera
```

### Purpose

Allows operation from externally supplied regulated DC power.

---

# Firmware Safety Rules

The firmware must prevent simultaneous activation of:
- external battery path
- regulated DC path

The following condition must never occur:

```
HS1_EN = ON
AND
BATT_SW_EN = ON
```

This prevents:
- unintended cross-powering
- reverse current conditions
- potential power-path conflicts

---

# Key Hardware Blocks

| Block | Function |
|---|---|
| Teensy 4.0 | Main embedded supervisory controller |
| TPS22810 | 8V high-side load switch for camera DC path |
| AO4805 + 2N7002 | Bidirectional battery switch using back-to-back P-channel MOSFETs |
| AQY212G2SX | Camera switch dry-contact PhotoMOS interface |
| DRV8825 | Bipolar stepper motor driver with current regulation |
| BME280 | Temperature / humidity / pressure sensing |
| LSM6DS3 | IMU / accelerometer / gyroscope |
| LIS3MDL | Magnetometer |
| NJK-5002C Interface | 12V Hall-effect proximity/home sensor interface |

---

# Sensor Subsystem

The board integrates multiple sensors for environmental and positional monitoring.

## Environmental Sensor

### BME280

Provides:
- temperature sensing
- humidity sensing
- pressure sensing

Useful for:
- enclosure monitoring
- environmental characterization
- deployment diagnostics

---

## IMU Subsystem

### LSM6DS3

Provides:
- accelerometer
- gyroscope

Useful for:
- motion characterization
- orientation tracking
- deployment diagnostics

---

## Magnetometer

### LIS3MDL

Provides:
- magnetic field sensing
- orientation support

Useful for:
- positional monitoring
- environmental characterization

---

# Motion Control Subsystem

The motion-control subsystem is based on the DRV8825 bipolar stepper motor driver.

Features:
- STEP/DIR interface
- current regulation
- microstepping capability
- integrated H-bridge control

The motor subsystem interfaces with:
- external motor connector
- proximity/home sensor
- Teensy supervisory controller

---

# Camera Control Subsystem

The camera ON/OFF control is implemented using:
- AQY212G2SX PhotoMOS relay
- dry-contact electronic switching

The architecture emulates the original camera switch behavior electronically while maintaining electrical isolation between:
- camera interface
- embedded controller

---

# PCB Design Strategy

## PCB Stack-up

The board uses a 4-layer architecture.

| Layer | Function |
|---|---|
| L1 | Components + primary routing |
| L2 | Continuous solid GND plane |
| L3 | Power routing and support signals |
| L4 | Secondary signal routing + GND pour |

---

## Grounding Strategy

The PCB uses:
- continuous internal GND plane
- GND stitching vias
- localized decoupling
- mixed-signal partitioning

to improve:
- return-current continuity
- EMI behavior
- sensor stability
- mixed-signal integrity

---

## Routing Strategy

Special routing considerations include:
- motor-current isolation
- sensor noise reduction
- controlled return-current paths
- short switching loops
- thermal via usage
- decoupling capacitor placement

---

## Connector Strategy

Connector selection was driven by:
- enclosure accessibility
- cable retention
- current capability
- deployment reliability

### Selected Connectors

| Connector Type | Application |
|---|---|
| JST PH | Low-current signal interfaces |
| JST VH | Power and motor interfaces |

The project migrated away from screw terminals due to:
- limited enclosure accessibility
- mating difficulty inside underwater housing
- cable-management concerns

---

# Repository Structure

```
requirements/       System requirements and specifications
architecture/       System architecture and interface definitions
docs/               Design review, deployment, and manufacturing documentation
images/             Schematic, PCB, assembly, and validation images
bringup/            Bring-up checklist and debug workflow
validation/         Validation plans and measurement results
papers/             Abstracts and publication drafts
firmware/           Public firmware notes and interface documentation
manufacturing/      Public manufacturing notes and workflow documentation
hardware/           Public hardware overview and private repo linkage
```

---

# Private Engineering Repository

This public repository documents:
- requirements
- architecture
- validation methodology
- deployment workflow
- engineering process

Implementation-level engineering files are maintained separately in:


- [IWCD_CAM_CTRL_ENGINEERING](https://github.com/shomi74/IWCD_CAM_CTRL_ENGINEERING)


The private engineering repository contains:
- KiCad source files
- manufacturing outputs
- fabrication package
- hardware BOM
- firmware source
- procurement tracking
- internal design iterations
- debug and troubleshooting notes
- stack-up and routing notes
- assembly documentation

---

# Engineering Workflow

The project documents the complete hardware-development lifecycle:

1. Requirements definition
2. System architecture
3. Interface definition
4. Power architecture development
5. Schematic capture
6. Multi-layer PCB layout
7. Connector and deployment optimization
8. Manufacturing preparation
9. Bring-up planning
10. Validation planning
11. Deployment considerations
12. Revision tracking

---

# Current Status

| Area | Status |
|---|---|
| Requirements Definition | Complete |
| System Architecture | Complete |
| Schematic Design | Complete / under review |
| PCB Layout | First routed revision completed |
| Connector Migration | Completed |
| Stack-up Definition | Completed |
| Manufacturing Planning | In progress |
| Bring-up Planning | In progress |
| Validation Planning | In progress |

---

# Next Steps

- Final DRC verification
- Footprint validation
- Manufacturing output generation
- Assembly review
- Hardware fabrication
- Initial bring-up
- Validation measurements
- Deployment testing

---

# Applications

This platform and workflow are applicable to:
- underwater detector imaging
- scientific instrumentation
- embedded camera systems
- mixed-signal instrumentation electronics
- distributed embedded control systems
- remote imaging infrastructure

---

# Acknowledgements

Developed as part of the IWCD / Hyper-K photogrammetry and detector imaging infrastructure development effort.
