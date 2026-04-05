---
title: "Subsystem A: RX Filter and Quadrature Mixer"
date: 2026-04-04 00:05:00 +/-TTTT
categories: [Hardware, Analog Design]
tags: [LTSpice, Altium Designer, Soldering, Oscilloscope, Waveform Generator, Digital Multimeter]
---

Subsystem A is the analog front-end for a larger receiver system, handling critical frequency selection and down-conversion. This project was a deep dive into discrete analog design, centered around a high-order RX filter and a quadrature mixer implemented with a discrete Gilbert Cell.

## Analog Design & Simulation

The design was heavily Iterated in **LTSpice** to ensure the mathematical models for the discrete components held up before moving to physical hardware.

### Multi-Pole RX Filter
The signal chain begins with a multi-pole active bandpass filter. I designed this stage to provide sharp roll-off to suppress out-of-band interference while maintaining a flat passband for signal integrity. AC analysis was used to fine-tune the 3dB cutoff points, ensuring the Q-factor was optimized for the target 45MHz RF input.

### Discrete Gilbert Cell Mixer
The heart of the subsystem is a **discrete Gilbert Cell** used for quadrature down-conversion. By building the mixer from discrete BJTs rather than an integrated IC, I had to manage several low-level analog challenges:

* **Transistor Matching & Biasing:** To achieve high conversion gain and minimize port-to-port feedthrough, the differential pairs required precise DC biasing. I utilized the +12V / -12V rails from my custom **USB-C Power Supply** to provide the necessary headroom and stability.
* **Quadrature Generation:** The Local Oscillator (LO) signal is split into In-phase (I) and Quadrature (Q) components with a 90° phase shift. This relationship is critical; any phase error directly degrades the system's image rejection capabilities.


## Layout & Hardware Implementation

Translating the discrete design to a PCB in **Altium Designer** required strict adherence to RF layout principles to prevent parasitic effects from detuning the sensitive analog stages.

* **Symmetric Trace Routing:** I manually routed the I and Q signal paths to be perfectly symmetrical. Length matching these traces was essential to maintain the 90° phase relationship established in the quadrature generation stage.
* **Ground Plane Integrity:** A solid ground plane was used to provide a low-impedance return path, which is vital for reducing noise floor in high-frequency analog circuits.
* **Discrete Assembly:** The board was hand-soldered, which required careful thermal management to avoid damaging the discrete SMT transistors during the assembly of the Gilbert Cell.


## Testing & Bench Validation

Validation was performed at my workbench to verify the time-domain performance of the discrete mixer:

* **Waveform Generator:** Injected a 45MHz RF signal and a synchronized LO.
* **Oscilloscope:** Used to capture the I and Q outputs simultaneously. I specifically monitored the quadrature relationship to ensure the 90° shift was maintained across the passband.
* **Digital Multimeter:** Verified DC bias points for all discrete transistors during initial bring-up.

### Interface Control Document (ICD) Snippet
To ensure compatibility with the rest of the receiver, the subsystem adheres to the following interface specs:
* **Input:** 45MHz RF (SMA), 50Ω Impedance.
* **Local Oscillator:** 45.455MHz (SMA).
* **Output:** Baseband I/Q (Header), 0-5V swing.
* **Power:** +12V / -12V DC input.

This project was a major lesson in how component tolerances and layout parasitics affect a theoretical discrete design, reinforcing the importance of rigorous simulation and matched routing.