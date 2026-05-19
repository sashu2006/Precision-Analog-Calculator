# Precision Continuous-Time Analog Calculator

## Overview
Modern edge-device applications demand fast, localized processing with strict constraints on power and memory. Traditional digital implementations struggle to compute non-linear functions (like logarithms) efficiently, wasting clock cycles and silicon area on memory-heavy approximations. 

This project presents a **Continuous-Time Analog Calculator** built entirely from discrete components (LM358P op-amps and 1N4148 diodes). By exploiting fundamental device physics, this analog ALU performs instantaneous, zero-latency math at the speed of electron flow—completely bypassing digital clocks and memory storage.

## Hardware Performance & Error Rates
The physical prototype was built across four solderless breadboards using 32 discrete op-amps. Despite the physical limitations of breadboard prototyping, the system drastically outperformed our initial 5% error constraint, achieving an **overall system average error of just 2.15%**.

| Computational Block | Data Inclusion Criteria | Average Error (%) |
| :--- | :--- | :--- |
| **Logarithmic Ratio** | Sub-1V Inputs Excluded | 0.95% |
| **Absolute Value** | All Values Included | 1.32% |
| **Analog Adder** | All Values Included | 1.58% |
| **Analog Multiplier** | Sub-1V Inputs Excluded | 2.48% |
| **Analog Subtractor** | All Values Included | 2.67% |
| **Analog Divider** | Sub-1V Inputs Excluded | 3.89% |

*(Note: Sub-1V inputs were excluded for non-linear modules as the op-amp drive current becomes comparable to inherent leakage current at those levels, skewing the physics).*

## Hardware Challenges Faced
Building a complex analog system from scratch presented several intense logistical and physical hurdles:
* **Power Supply Loading:** Powering 32 op-amps simultaneously from a single bench supply caused significant voltage sag and risked frying the ICs. We had to isolate the power rails to individual breadboards to stabilize the system.
* **Component Density & Wiring:** Routing 32 op-amps, 67 resistors, and 11 diodes required extreme cable management. Parasitic capacitance, breadboard contact resistance, and accidental short circuits were a constant debugging battle.
* **Calibration Limitations:** Physical resistors rarely match their theoretical math perfectly. We had to experimentally calculate "best-fit" scaling factors and create custom resistor values in series to force the hardware to match the math.
* **The Matched BJT Problem:** We initially designed a square root solver, but building it physically required perfectly matched Bipolar Junction Transistors (BJTs). Because commercially matched pairs were prohibitively expensive, we had to scrap that specific module.

## Future Improvements
* **Analog RAM:** Implementing sample-and-hold circuits to store computed voltages, preventing data loss the moment the inputs change.
* **Sequential Operations:** Chaining operations together so the output of one module feeds directly into the next, mimicking the "immediate-type" instruction execution of a digital CPU.
* **Edge Computing Integration:** Tuning these circuits for ultra-low-power IoT sensors, where instant, memory-free analog computation is vastly more efficient than pure decimal precision.
