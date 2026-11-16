# Design and Simulation of an H-Bridge Inverter (PLECS + RT-Box)

**Module:** EG7231 – Real Time Simulation for Industry 4.0
**Institution:** University of Leicester, School of Engineering
**Author:** Siddhant Satyawan Jagtap
**Supervisor:** Dr. Yuan Gao

## Overview
A single-phase H-bridge DC-AC inverter modelled in PLECS and run in real time on a
Plexim RT-Box, with the output captured on a Tektronix TDS 2002 oscilloscope.
Two cases are compared:

1. **Without dead time** – ideal switching, both pulse generators in phase.
2. **With dead time** – 3 ms phase delay (15% of the 20 ms period) between the two pulse generators.

## Key parameters
| Parameter | Value |
|---|---|
| DC input (Vin) | 10 V |
| Switches | 4 × ideal N-channel MOSFET (S1–S4) |
| Load | R1 = 1 Ω, L1 = 1 mH (τ = 1 ms) |
| Switching frequency | 50 Hz (20 ms period) |
| Duty cycle | 50 % |
| Dead time | 0 ms / 3 ms |

## Repository contents
```
.
├── README.md
├── model/
│   └── Sid_Inverter.plecs        # PLECS model
├── report/
│   └── Final_R-TBox.pdf          # Full written report
└── images/                       # (optional) scope / oscilloscope screenshots
```

## How to run
1. Open `model/Sid_Inverter.plecs` in PLECS (Standalone or Blockset).
2. Run the simulation and inspect the Scope (load voltage, currents I1 and I2).
3. For real-time operation, build the model for the RT-Box target and connect
   Analog Out 1 to Channel 1 of the oscilloscope.

## Results summary
- No dead time: ideal ±10 V bipolar square wave, instantaneous transitions.
- With dead time: zero-voltage notches at each edge, reducing the effective
  fundamental voltage and preventing shoot-through.
- RT-Box oscilloscope output matched the PLECS simulation (≈50 Hz).

## References
Mohan et al., *Power Electronics*; Plexim PLECS and RT-Box manuals; Holmes & Lipo, *Pulse Width Modulation for Power Converters*; Rashid, *Power Electronics Handbook*.
