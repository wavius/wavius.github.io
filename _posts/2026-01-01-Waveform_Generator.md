---
title: Waveform Generator
date: 2026-01-01 00:05:00 +/-TTTT
categories: [Hardware, PCB Design]
tags: [C, LTSpice, Altium Designer, Soldering, Oscilloscope, Waveform Generator, Digital Multimeter]
---

Earlier this year, as I started diving deeper into breadboarding and analog circuits, I realized I didn't have access to a bench power supply outside of the university lab.

To make Op-Amp circuit without the headache of DC biasing all the time, a simple 5V USB brick isn't enough. I needed positive and negative rails to handle analog signals, and that is exactly why I built this. My goal was to move away from lab equipment and design a portable power distribution board using USB-C Power Delivery. I was also hoping it would be cheaper than buying a bench supply, but it was a learning opportunity either way.

To handle the power negotiation, I used the IP2721 IC to communicate with 45W USB-C sources. This allowed the board to "request" the full power envelope from a standard charger block. From there, I designed a regulation network to provide four fixed digital rails (+12V, -12V, +5V, and +3.3V) and one highly configurable analog output.

To handle waveform generation, I integrated an STM32 microcontroller to control an AD9833 chip. By using a rotary encoder and a potentiometer, I can adjust the frequency, phase, and voltage offset of the analog output in real-time. I also included a dedicated LCD header and an STLINK interface, allowing me to debug the system and monitor parameters directly on the device.

![Waveform Generator PCB](../assets/img/posts/wfg/wfg_pcb.jpg)

This was my first 4-layer PCB design, and stepping up from 2 layers was a nice change. I've since used it to power many circuits up to 100mA without any issue. 

I have already programmed the LCD display, but I haven't yet had the time to fully implement the AD9833. I plan to do this in the very near future, and will add the results here.

As always, the files for this project are available on my [GitHub](https://github.com/wavius/PCB-Designs/tree/main).
