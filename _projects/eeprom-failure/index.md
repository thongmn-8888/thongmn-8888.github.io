---
layout: post
title: EEPROM Failure Analysis (from Masimo Internship)
skills:
- Oscilloscope
- SPI Communication
- C Programming
- Soldering
main-image: /read-diagram.png
---

## Project Description
The Ethernet MAC address doesn’t show up during instrument testing for bad EEPROMs. The EEPROMs on failed boards appear to be damaged or corrupted, which disrupts 3-4% production rate of the instrument. Functional testing on failed boards illustrated at writing and reading on EEPROM. Imagine in an office building, ethernet connector is the front door, USB Hub is the receptionist, EEPROM is the receptionist’s badge/ID card, and MAC address is the receptionist’s employee ID number. 

## Investigation
I conducted a schematics review of the board to understand the board interactions with the EEPROM, which led to the MAC address being displayed on the instrument. I reviewed the EEPROM datasheet to identify the component communication requirements: how signals should be set to send commands and receive responses from the EEPROM. For example, the requirements for a read command include: CS (Chip Select) pin being toggle high at the beginning then low at the end, CLK continuously pulses for 27 times, and DI (Data In) bits contains the opcode for reading and address bits (data location). As I understood requirements for an EEPROM to function, I analyzed different techniques to communicate with the EEPROM: USB-Hub manufacturer-provided configuration software, Bus Pirate, and Nordic Dev Kit. 

For the first method, it requires using the software that comes with the USB Hub to communicate with the EEPROM. To do this, I solder wires from a USB-A port to the USB-Hub, which includes D+, D-, and GND. The length of these wires being exposed to the air, without copper wire around, needs to be as short as possible to prevent noises caused by electromagnetic fields. The software allows communication via command line and graphical interface. I tried communicating with the EEPROM using this technique, but neither works since there is an issue with the USB-Hub device enumeration. However, doing all this helps me confirm that the boards that I’m working with are failed ones because this is the same technique that test engineers used to communicate with the EEPROMs earlier.

Then, I decided to try using a Bus Pirate, which requires me learning how to set up hardware for SPI communication. As a result, I figured out that MISO pin (on Bus Pirate) → DO (on EEPROM), MOSI → DI, CLK → SCK, CS → CS. MISO is when the Master (Bus Pirate) is in and Slave (EEPROM) is out, so the Bus Pirate will receive the data from the EEPROM output pin. MOSI contains the instruction input bits Bus Pirate sends to EEPROM. This helps EEPROM know whether the device is trying to read, write, or erase, etc. CLK contains rising and falling edges to indicate when data is stable and when it transitions. The Bus Pirate method’s pros is it generates nice signals, so it is easy to decode the data. Its cons is that the clock can only generate 8 pulses per command, but we need up to 27 bits to fit in a write command. If we keep this, a write command can be broken into two clock cycles, which disrupts the communication. As a result, I need a better solution to increase the number of clock pulses.

With the third method, I utilized the Nordic Dev Kit to communicate with the EEPOM. I wrote codes in C to enable SPI communication between the Nordic microcontroller and EEPROM. As a result, I was able to send erase, write, and read commands on both bad and good EEPROMs. Since I wrote code on uVision IDE, I run the code in debugger mode to confirm the read data from EEPROM and compare it with the oscilloscope result, which ensures the data exchanges are accurate. Based on the oscilloscope result, which shows that the Data In signal transitions on rising edge, while the Data Out transitions on falling edges. This behavior is abnormal to my experiences with decoding data on clocks since it is usually the rising edges that matter. Thus, I reached out to the field application engineer from the EEPROM manufacturer to confirm this signal behavior.

## Timing Diagrams
<img src="/assets/images/eeprom-failure-project/read-timing.png" width="600">
<img src="/assets/images/eeprom-failure-project/write-timing.png" width="600">
<img src="/assets/images/eeprom-failure-project/eral-timing.png" width="600">

## Result
The failure is identified to be data corruption inside the EEPROM. Reprogrammed ‘bad’ EEPROM passed functional testing and displayed Ethernet MAC address using instrument testing.

## Takeaways
- Learned how to read the data via an oscilloscope signal.
- Set up trigger mode in the oscilloscope to capture the wanted signal.
- Set up a hardware communication between master (Bus Pirate & Nordic Kit) and slave devices (EEPROM).
- Reach out for help from different people.
- Solder components and wires
- Binary-Hex conversion
- Continuity testing using digital multimeter
- Schematics review
