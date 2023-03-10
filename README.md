# Micro-Foundry-XC6194A-Discrete-Logic-RGB-Expansion-PCB
Information about the XC6194A Expansion PCB based on discrete logic to drive 3 LEDs and provide voltage translation

## Why?
I utilize the TOREX XC6194A in various projects and some have the extra IO to drive the RGB LEDs. So I rolled up the design into an accessory to complement the XC6194 breakout, including a few additional features.

## Description
The Micro Foundry XC6194A Discrete Logic RGB Expansion PCB provides the ability to drive a RGB LED illuminated Momentary switch or up to 3 individual LED indicators (with common anode) in addition to offering voltage translation where the XC6194A switched VCC differs from MCU VCC. 

**Please NOTE:** Color representation is totally dependent on the LEDs utilized. Therefore, there are no guarantees this LED driver will have the ability to produce the accurate color representation possible with 3x LEDs.

## Features
- 3 Channels of LED switching with 32mA at 5v (24mA at 3.3v) sink capability per channel utilizing Open Drain Inverters 
- An additional "Power State" channel to provide a sink to LED channel 1 when XC6194 is in Off State. (more details [below](/README.md#power-state-channel))
- Voltage translation on SW (Switch) output -> MCU input with Schmitt-Trigger input/inverted output
- Anode series resistor to provide global LED current control (more details [below](/README.md#anode-series-resistor))
- On-board micro switch for additional XC6194A control
- Mount holes will accept Wurth Electronics SMT Standoffs

## Pinouts
### Switch

| Pin | Function | Description | Voltage Potential |
| --- | -------- | ----------- | ---------- |
| 1 | SW | Momentary Switch Input (Active LOW) | XC6194A VIn |
| 2 | GND | Ground | |
| 3 | ANN |Common LED Anode | XC6194A VIn |
| 4 | LED1 | LED 1 Cathode | |
| 5 | LED2 | LED 2 Cathode | |
| 6 | LED3 | LED 3 Cathode | |

### IO (to MCU)

| Pin | Function | Description | MCU IO | Voltage Potential |
| --- | -------- | ----------- | ------ | ---------- |
| 1 | GND | Ground | | GND |
| 2 | VCC | Voltage In | | MCU VCC |
| 3 | SW | Switch Pressed | Input (Active HIGH) | MCU VCC |
| 4 | SHDN | Shutdown | Output (Active HIGH) | MCU VCC |
| 5 | PG | Power Good | Output (Active HIGH) **See NOTE-1** | XC6194A VIn |
| 6 | LED1 | LED 1 Driver | Output (Active HIGH) | MCU VCC |
| 7 | LED2 | LED 2 Driver | Output (Active HIGH) | MCU VCC |
| 8 | LED3 | LED 3 Driver | Output (Active HIGH) | MCU VCC |

**NOTE-1:** The Power Good output is traditionally utilized to enable a downstream power supply, therefore the output operates at XC6194A VIn Potential. Please verify voltage compatibility before connecting.

### Expansion

| Pin | Function | Description | XC6194A IO | Voltage Potential |
| --- | -------- | ----------- | ---------- | ---------- |
| 1 | VIn | XC6194A Switched Voltage In | | XC6194A VIn |
| 2 | GND | Ground | | GND |
| 3 | VOut | XC6194A Switched Voltage Out | | XC6194A VOut |
| 4 | SW | XC6194A Momentary Switch | Input (Active LOW) | XC6194A VIn |
| 5 | PG | XC6194A Power Good | Output (Active HIGH) | XC6194A VIn |
| 6 | SHDN | XC6194A Shutdown | Input (Active HIGH) **See NOTE-2** | GND |

**NOTE-2:** Circuit is pulled to GND via pull-down resistor. XC6149A datasheet specifies a voltage level above 1.1v will trigger shutdown. Some MCUs may exhibit an output glitch on the SHDN during power-up and the XC6194 may immediately shutdown. If this is experienced, a user implemented RC filter could possibly eliminate the issue.

## Power State Channel
Channel 1 LED has a secondary open-drain buffer with its input referenced to VOut. When the XC6194A is in its off-state, the logic will illuminate the Channel 1 LED. This can be useful to provide a vsual indicator that the power is off. When the XC6194A is in its on-state, the secondary open-drain output is in a high-z state and the primary Channel 1 LED open-drain inverter is free to drive the LED. If there is no desire to have the Channel 1 LED illuminated when the power is off, this feature can be disabled by removing the resistor as indicated in the following image:

**TODO:** Add image to indicate R2 removal...

## Anode Series Resistor
The resistor noted in the following image offers global current control via the common anode pin. The default value as manufactured is 0 Ohms (Zero) and can be replaced if necessary.

**TODO:** Add image to indicate R3 location...

## XC6194A Breakout PCB Variants
- [Micro Foundry XC6194A JST PH Style Breakout PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-PH-Breakout-PCB)
- [Micro Foundry XC6194A Micro USB Breakout PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-Micro-USB-Breakout-PCB)
- [Micro Foundry XC6194A USB-C Breakout PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-USB-C-Breakout-PCB)

## XC6194A Expansion PCBs
- [Micro Foundry XC6194A Discrete Logic RGB Expansion PCB](https://github.com/microfoundry/Micro-Foundry-XC6194A-Discrete-Logic-RGB-Expansion-PCB)
- [Micro Foundry XC6194A WS2811 RGB Expansion PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-WS2811-Expansion-PCB)
- [Micro Foundry XC6194A IS31FL3193 RGB Expansion PCB](https://github.com/microfoundry/MicroFoundry-XC6194A-IS31FL3193-Expansion-PCB)
