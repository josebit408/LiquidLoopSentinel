# LiquidLoopSentinel

LiquidLoopSentinel is a Raspberry Pi Pico-based printed circuit board designed to monitor coolant temperature, flow, leaks, and electrical conditions while providing visual and audible fault alerts.

## Overview

LiquidLoopSentinel is a custom monitoring printed circuit board intended for liquid-cooled computing systems and artificial intelligence hardware test benches.

The board integrates multiple sensors with a Raspberry Pi Pico to monitor the condition of a liquid-cooling loop and detect problems such as:

- Abnormal coolant temperature
- Reduced or interrupted coolant flow
- Liquid leakage
- Electrical power abnormalities

When the system detects a fault, it can provide visual status indications through light-emitting diodes and an audible warning through a buzzer.

## Features

- Raspberry Pi Pico controller
- Two temperature sensor inputs
- Coolant flow sensor input
- Leak sensor input
- INA219 voltage and current monitoring interface
- Inter-Integrated Circuit communication
- Flow sensor signal conditioning
- Leak sensor pull-up circuitry
- Three status indicators:
  - System operating normally
  - Warning condition
  - Leak detected
- Transistor-driven buzzer
- Dedicated test points
- Separate 5-volt flow sensor power input
- Ground plane
- Through-hole component design for prototyping and manual assembly

## System Architecture

```text
                    Liquid-Cooling Loop
                           |
          +----------------+----------------+
          |                |                |
     Temperature          Flow             Leak
       Sensors            Sensor           Sensor
          |                |                |
          +----------------+----------------+
                           |
                           v
                  Raspberry Pi Pico
                           |
                 System Health Analysis
                           |
             +-------------+-------------+
             |             |             |
             v             v             v
          OK LED       Warning LED    Leak LED
                                           |
                                        Buzzer
```

## Hardware

### Microcontroller

The system is designed around the **Raspberry Pi Pico**.

The Pico receives sensor signals, evaluates the condition of the cooling loop, and controls the board's visual and audible warning indicators.

### Temperature Monitoring

Two temperature sensor connections are provided:

- `TEMP_IN`
- `TEMP_OUT`

Both connections share the `TEMP_ONEWIRE` data bus and use a 4.7-kilohm pull-up resistor connected to 3.3 volts.

This configuration allows the system to measure coolant temperature at two locations within the cooling loop.

### Flow Monitoring

The flow sensor interface provides the following connections:

- `+5V_FLOW`
- `FLOW_SENSOR_RAW`
- `GND`

A resistor-divider network conditions the raw flow sensor signal before it reaches the Raspberry Pi Pico as `FLOW_PULSE`.

### Leak Detection

A dedicated leak sensor connector provides the following connections:

- `LEAK_DETECT`
- `GND`

A 100-kilohm pull-up resistor connects the leak detection signal to 3.3 volts.

### Electrical Monitoring

An INA219 interface provides the following connections:

- `+3V3`
- `GND`
- `I2C0_SDA`
- `I2C0_SCL`

This interface supports voltage, current, and power monitoring through a compatible INA219 module.

### Status Indicators

The printed circuit board includes three status indicators:

| Indicator | Purpose |
|---|---|
| `LED_OK` | Indicates normal operation |
| `LED_WARN` | Indicates a warning condition |
| `LED_LEAK` | Indicates that a leak has been detected |

Each light-emitting diode uses a 330-ohm current-limiting resistor.

### Audible Alert

A buzzer provides an audible warning when the system detects a fault.

The Raspberry Pi Pico controls the buzzer through an NPN transistor stage, preventing the microcontroller's general-purpose input and output pin from directly driving the buzzer load.

### Test Points

The board includes dedicated test points for the following signals:

- `+3V3`
- `GND`
- `FLOW_PULSE`
- `LEAK_DETECT`

These test points allow important system signals to be measured during testing, validation, and troubleshooting.

## Printed Circuit Board

The current hardware revision is:

**LiquidLoopSentinel Revision A**

The printed circuit board is currently in the prototype and design-validation stage.

Current design characteristics include:

- Two-layer printed circuit board
- Through-hole components
- Front and back copper routing
- Bottom-layer ground plane
- Raspberry Pi Pico socket headers
- Dedicated sensor connectors
- Dedicated test points

## Repository Structure

```text
LiquidLoopSentinel/
|
├── README.md
├── LICENSE
|
├── hardware/
│   └── kicad/
│       ├── LiquidLoopSentinel_RevA.kicad_pro
│       ├── LiquidLoopSentinel_RevA.kicad_sch
│       └── LiquidLoopSentinel_RevA.kicad_pcb
|
├── manufacturing/
│   └── RevA/
│       ├── gerbers/
│       ├── drill/
│       └── bom/
|
├── firmware/
│   └── pico/
|
├── docs/
│   └── images/
|
└── mechanical/
    └── 3d/
```

## Development Status

**Revision A: In Development**

Current progress:

- [x] System architecture
- [x] Schematic design
- [x] Printed circuit board component placement
- [x] Printed circuit board routing
- [x] Ground plane
- [x] Design Rules Check
- [x] Schematic and printed circuit board parity check
- [ ] Final component pinout verification
- [ ] Connector orientation verification
- [ ] Silkscreen cleanup
- [ ] Mounting holes
- [ ] Final manufacturing review
- [ ] Gerber file generation
- [ ] Printed circuit board fabrication
- [ ] Board assembly
- [ ] Hardware validation
- [ ] Raspberry Pi Pico firmware

## Project Goal

The goal of LiquidLoopSentinel is to create a low-cost, modular hardware monitoring platform that can detect cooling-system failures before they damage sensitive computing equipment.

## Development Tools

- KiCad 10
- Raspberry Pi Pico
- C, C++, or MicroPython
- Git
- GitHub

## Disclaimer

LiquidLoopSentinel Revision A is an experimental engineering prototype that has not yet completed hardware validation. It should not be used as the sole protection mechanism for safety-critical systems or high-value equipment.

## Author

**Jose Luis Zaragoza-Calderon Jr.**

Computer Engineering
