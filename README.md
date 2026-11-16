# Design and Simulation of an H-Bridge Inverter (PLECS + RT-Box)

- **Module:** EG7231 – Real Time Simulation for Industry 4.0
- **Institution:** University of Leicester, School of Engineering
- **Author:** Siddhant Satyawan Jagtap
- **Supervisor:** Dr. Yuan Gao

## Overview
A single-phase H-bridge DC-AC inverter modelled in PLECS and run in real time on a
Plexim RT-Box, with the output captured on a Tektronix TDS 2002 oscilloscope.
Two cases are compared:

1. **Without dead time** – ideal switching, both pulse generators in phase.
2. **With dead time** – 3 ms phase delay (15% of the 20 ms period) between the two pulse generators.

## Circuit
![H-bridge inverter circuit in PLECS](images/circuit.png)

*Four switches (S1–S4) in an H configuration, driven by two pulse generators through combinatorial logic and a gate demultiplexer, feeding an RL load (L1 = 1 mH, R1 = 1 Ω) from a 10 V DC source.*

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
- `Sid_Inverter.plecs` – PLECS model
- `Final R-TBox.pdf` – full written report
- `images/` – circuit diagram, PLECS scope plots and RT-Box oscilloscope captures
- `README.md` – this file

## Results

### Without dead time
Pulse generator settings (both identical, 0 s phase delay):

![Pulse generator parameters without dead time](images/pulse_generator_params_no_deadtime.png)

PLECS scope – load voltage (top) and currents I1, I2:

![PLECS scope without dead time](images/plecs_scope_no_deadtime.png)

RT-Box output on the oscilloscope:

![RT-Box oscilloscope without dead time](images/rtbox_oscilloscope_no_deadtime.png)

### With dead time (3 ms)
Pulse generator settings (Pulse Generator 2 delayed by 0.003 s):

![Pulse generator parameters with dead time](images/pulse_generator_params_with_deadtime.png)

PLECS scope – zero-voltage notches at each edge:

![PLECS scope with dead time](images/plecs_scope_with_deadtime.png)

RT-Box output on the oscilloscope:

![RT-Box oscilloscope with dead time](images/rtbox_oscilloscope_with_deadtime.png)

## How to run
1. Open `Sid_Inverter.plecs` in PLECS (Standalone or Blockset).
2. Run the simulation and inspect the Scope (load voltage, currents I1 and I2).
3. For real-time operation, build the model for the RT-Box target and connect
   Analog Out 1 to Channel 1 of the oscilloscope.

## Results summary
- No dead time: ideal ±10 V bipolar square wave, instantaneous transitions.
- With dead time: zero-voltage notches at each edge, reducing the effective
  fundamental voltage and preventing shoot-through.
- RT-Box oscilloscope output matched the PLECS simulation (≈50 Hz).

## References
- Mohan, Undeland and Robbins, *Power Electronics: Converters, Applications, and Design*, Wiley
- Plexim, PLECS User Manual and RT-Box User Manual
- Holmes and Lipo, *Pulse Width Modulation for Power Converters*, IEEE Press
- Rashid, *Power Electronics Handbook*
