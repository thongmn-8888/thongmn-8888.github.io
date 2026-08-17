---
layout: post
title: Battery Management System
description:  This project focuses on the design of a Battery Management System (BMS) for a 12s4p lithium-ion battery pack using 18650 cells for electric vehicle applications. The BMS monitors individual cell voltages and temperatures, performs cell balancing during charging, and communicates battery data to external systems. An STM32F446 microcontroller is used as the main controller due to its integrated ADCs and peripheral support. Because series-connected cells naturally develop voltage imbalance, each cell voltage is measured independently using the MCU’s ADC. A passive balancing circuit is implemented using bleeding resistors and MOSFETs to safely discharge higher-voltage cells and equalize the pack.
skills: 
- KiCAD
main-image: /bms.png
<p float="left">
  <img src="/assets/images/bms-project/top-level.png" width="300" />
  <img src="/assets/images/bms-project/voltage-subtractor.png" width="300" /> 
  <img src="/assets/images/bms-project/power-rail.png" width="300" />
</p>
---
