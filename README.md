# Micro-Foundry-XC6194A-Discrete-Logic-RGB-Expansion-PCB
Information about the XC6194A Expansion PCB based on discrete logic to drive 3 LEDs and provide voltage translation

## Description
The Micro Foundry XC6194A Discrete Logic RGB Expansion PCB provides the ability to drive RGB Momentary switch (with common annode) in addition to offering voltage translation where the XC6194A switched VCC differs from MCU VCC. 

## Features
- 3 Channels of RGB switching with 32mA sink capability utilizing Open Drain Inverters
- An additional channel to provide a sink to LED channel 1 when XC6194 is in Off State. (can be disabled)
- Voltage translation on SW (Switch) output -> MCU input with Schmitt-Trigger input/inverted output
- Annode series resistor to provide global LED current control
- On-board micro switch for additional XC6194A control
- Mount holes will accept Wurth Electronics SMT Standoffs

## Pinouts
### Switch

| Pin | Function | Description | Voltage Potential |
| --- | -------- | ----------- | ---------- |
| 1 | SW | Momentary Switch Input (Active LOW) | XC6194A VIn |
| 2 | GND | Ground | |
| 3 | ANN |Common LED Annode | XC6194A VIn |
| 4 | LED1 | LED 1 Cathode | |
| 5 | LED2 | LED 2 Cathode | |
| 6 | LED3 | LED 3 Cathode | |

### IO (to MCU)

| Pin | Function | Description | Voltage Potential |
| --- | -------- | ----------- | ---------- |
| 1 | GND | Ground | GND |
| 2 | VCC | Voltage In | MCU VCC |
| 3 | SW | Switch Pressed input (Active HIGH) | MCU VCC |
| 4 | SHDN | Shutdown Output (Active HIGH) | MCU VCC |
| 5 | PG | Power Good Output (Active HIGH) **See NOTE-1** | XC6194A VIn |
| 6 | LED1 | LED 1 Driver Output (Active HIGH) | MCU VCC |
| 7 | LED2 | LED 2 Driver Output (Active HIGH) | MCU VCC |
| 8 | LED3 | LED 3 Driver Output (Active HIGH) | MCU VCC |

**NOTE-1:** The Power Good Output is traditionally uitilized to enable a downstream power supply, therefore the output operates at XC6194A VIn Potential. Please verify voltage compatability before connecting.

### Expansion

| Pin | Function | Description | Voltage Potential |
| --- | -------- | ----------- | ---------- |
| 1 | VIn | XC6194A Switched Voltage In | XC6194A VIn |
| 2 | GND | Ground | GND |
| 3 | VOut | XC6194A Switched Voltage Out | XC6194A VOut |
| 4 | SW | XC6194A Momentary Switch Input (Active LOW) | XC6194A VIn |
| 5 | PG | XC6194A Power Good Output (Active HIGH) | XC6194A VIn |
| 6 | SHDN | XC6194A Shutdown Input (Active HIGH) **See NOTE-2** | GND |

**NOTE-2:** Circuit is pulled to GND via pull-down resistor. XC6149A datasheet specifies a voltage level above 1.1v will trigger shutdown. Some MCUs may exihibit an output glitch on the SHDN during power-up and XC6194 may immediately shutdown. If so, a user implemented RC filter might possibly eliminate the issue.


