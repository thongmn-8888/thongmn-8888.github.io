---
layout: post
title: MX-11 Tester Kit Calibration (from Masimo Internship) 
skills:
- Oscilloscope
- Circuitry analysis
- PADs Layout Software
main-image: /scope.jpg
---

## Project Description
MX-11 Tester Kit is used to test MX-11 (Device Under Test) circuit boards. The tester kit is the assembly result of MX-11 Base Board, the MX-11 Adapter Board, the Connector Test Kit, and the Ingun Frame. My task is to complete writing up the calibration procedure for the tester kit. 

## Investigation
Writing up the calibration procedure involves making a test spreadsheet, which contains lower and upper limits for each test value. To understand and provide the correct test limits for test engineers, I reviewed the base and adapter boards’ schematics, which are 11-sheet long. During this review, I also identified several parts of the circuit that have not been tested, and added in testing procedures for the thermistor and pins of 3 connectors. The reason for this is to ensure the current conduct well across the connector, making sure the DUT is well connected to the adapter test board. After completing writing up the calibration procedure, I performed the testing myself to ensure the test boards passed all my expected test limits. Then, I realize the frequency test for one of the clock signals inside the DUT on the adapter board produces incorrect results. I further investigated this matter by tracing the circuit that connects to this test point on the adapter board. I measured the signal at this test point on the oscilloscope in two scenarios: with and without the circuit connection on base boards, which resulted in very different results. The one without the connection produces nice and smooth sinusoidal waves, but the other one has distortion. As a result, the circuit of the DUT is fine, but there is a circuit concern with the base board. This frequency test point is shared by two circuits from 2 different boards. When I physically cut the connection with the “problem” circuit, the tested frequency becomes correct as expected. This “problem” circuit is a negative feedback op-amp circuit, whose input voltage is ground and output is connected to a capacitor. In AC, this capacitor creates a huge impedance load that drains more output current than the op-amp can handle, which results in the signal distortion across this section. 

## Result
- Documented the rework for test engineers to remove the connection to the “problem” circuit before performing calibration on the tester kit.
- Completed writing up the calibration procedure and did a dry run.

## Takeaways
- Circuit analysis skills to ensure all test ranges makes sense.
- Learned how to use PADs software to view the circuit board layout for testing purposes.
