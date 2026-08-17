---
layout: post
title: Pitch Detector
skills:
- KiCAD
- Circuitry design
- Layout design
main-image: /3d-view.png
---

## Project Description
The Pitch Detector project focused on developing a portable system that identifies the pitch of an audio input signal and displays the closest musical note in real time. The system was designed with a modular schematic architecture consisting of two hierarchical sheets: Power and Audio Input, enabling clearer separation of functionality and easier debugging. The power subsystem supports operation from a lithium-ion battery while allowing charging through a USB-C connection. A battery charger IC with Dynamic Power Path Management enables the device to run directly from USB power while simultaneously charging the battery, and to automatically switch to battery operation when unplugged. A step-down converter regulates the charger output to 3.3 V to safely power the ESP32 microcontroller. Component selection was guided by datasheet analysis to ensure adequate voltage and current margins. The PCB layout was collaboratively developed and refined to meet Bay Area Circuits manufacturing constraints, including trace width, via dimensions, and annular ring requirements, with DRC issues resolved through iterative adjustments. Embedded firmware was implemented to initialize the display and manage pitch data.

## Top-level schematics
<img src="/assets/images/pitch-detector-project/top-level.png" width="600">

## Power schematics
<img src="/assets/images/pitch-detector-project/power.png" width="600">

## Layout
<img src="/assets/images/pitch-detector-project/layout.png" width="600">

### 3D View
<img src="/assets/images/pitch-detector-project/3d-view.png" width="600">

### Board after soldering
<img src="/assets/images/pitch-detector-project/solder.png" width="600">
