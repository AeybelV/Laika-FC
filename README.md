# Laika

A compact, Linux-based avionics computer module for drones & rocketry.

## Overview

This project is a small-form-factor flight computer built around the 
[Milk-V Duo Module 01](https://milkv.io/duo-module-01). It is designed for 
both drone and rocketry applications and provides a Linux capable "brain" with
essential sensors and connectivity for control, telemetry, and logging.

Many flight controllers are built around MCU's, which are typically limited in
compute, memory, and application flexibility. For all intents and purposes this
satisfies most usecases. However modern SoC's have reach a point where they are both
cost effective and small package size that they can compete with these MCU platforms,
and being "overkill" wont affect weight, price, and size that much.

This project uses the Milk-V Module 01 to create a Linux-capable flight computer,
enabling a much richer software stack. This opens doors for high-level autonomy,
advanced navigation algorithms, onboard mapping,
real-time logging, networking, etc. Running Linux also allows leveraging mature tooling,
filesystems, telemetry stacks, services. The ease of bringing up custom flight software
is indespenable.

## Project Status

### Rev A

- [x] Requirements defined
- [ ] Schematic draft
- [ ] PCB Laayout
- [ ] Prototype fabrication
- [ ] Bring-up & Validation
- [ ] Flight tests

### Rev B

- Pending Rev A flight validation

## Revision 1

### Core Module

- Milk-V Duo Module 01
  - Sophgo SG2000 SoC
    - 1x RV64GCV C906@1GHz / Cortex-A53@1GHz
    - 1x RV64GC C906@700MHz
    - 1x 8051 Core
  - 512MB DRAM
  - 0.5TOPS INT8 TPU
  - ISP 5M@30fps
  - 4L or 2L+2L MIPI CSI 5M@30fps
  - H.265/H.264 Decoding and Encoding
- 8GB eMMC
- SD Card Slot (System or for Data Logging)
- 1x USB-C
- UART Breakout
- Reset and Boot Buttons
- Power / Status / Heartbeat LED's

### Flight Sensors

- 9-DoF IMU (Gyro, Accelerometer, Magnetometer)
- Barometric Pressure Sensor
- High G Accelerometer (optional)

### Communications

- Onboard Reyax RYLR993 LoRa Module
- GPS (External Module, UART hreader)

### Interfaces

- STEMMA/Qwiic-compatible I2C connectors
- Generic UART Header
- Broken out PWM/GPIO

### Power

The board can be powered two ways:

- USB-C
- Flight Power Connector

A toggle switch selects USB or flight power

Voltage input is 5-12V, and a onboard regulator will create 3.3V to
power the flight computer.

### Data Logging

microSD Card Slot on the top of the flight computer. If the system image
is flashed to the Milk-V's onboard eMMC, this SD card slot can be used for
data logging. Joining the `SD_BOOT` jumper will instead cause the Milk-V to
boot the image off the SD card.

### Misc

The board also contains a small piezo buzzer for simple tone generation.

## Planned Rev B Features

These are *intentionally omitted* from RevA to simplify layout and bringup

- Onboard GPS module
- RC/Remote input
- Reworked power selection and monitoring.

## Development Flow

### Branch Strategy

- `main`: Stable builds
- `revX.X`: Where X.X is the revision number. These are development branches for board revisions
- `feat/<name>`: Feature branches which and integrated/merged in "rev" branches

### Tags

- `revX.X-init`: The starting commit of a revision
- `revX.X-schematic-draft-X`: A schematic draft/pass for a revision where all blocks exist
- `revX.X-schematic-freeze`: Schematic freeze, ready to start layout
- `revX.X-pre-fab`: Final ERC/DRC and final checks.
- `revX.X-release`: Release commit sent to the fab. Merged into `main` branch.

## License

Copyright © 2025 Aeybel Varghese

Laika is open source and released under the CERN Open Hardware Licence Version 2
Contributions, bug reports, and feature requests are welcome.

See the [LICENSE](LICENSE) file for full details.
