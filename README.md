# Micro-Foundry-XC6194A-Discrete-Logic-RGB-Expansion-PCB
Information about the XC6194A Expansion PCB based on discrete logic to drive 3 LEDs and provide voltage translation

## Description
The Micro Foundry XC6194A Discrete Logic RGB Expansion PCB provides the ability to drive RGB Momentary switch (with common annode) in addition to offering voltage translation where the XC6194A switched VCC differs from MCU VCC. 

## Features
- 3 Channels of RGB switching with 32mA sink capability utilizing Open Drain Inverters
- An additional channel to provide a sink to LED channel 1 when XC6194 is in Off State. (can be disabled)
- Voltage translation on SW (Switch) output -> MCU input with Schmitt-Trigger input
- Annode series resistor to provide global LED current control
- On-board micro switch for additional XC6194A control
