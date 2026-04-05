---
title: Step Sequencer
date: 2025-11-15 00:05:00 +/-TTTT
categories: [Hardware, Digital Systems]
tags: [Verilog, Quartus, ModelSim]
---

For the final project in my Digital Systems class, I implemented a Step Sequencer on the DE1-SoC. This class was my introduction to Verilog and FPGA development, and I wanted to diverge from the common games most others made. 

My first idea for this project was to create a waveform generator where you could actually "draw" a wave on the VGA display and have the FPGA output that exact analog signal. However, after talking it over with one of my TAs, I realized that the DE1-SoC doesn't have a built-in DAC. Without a Digital-to-Analog Converter, generating a raw analog voltage for a custom wave wasn't going to be easily feasible.

My TA suggested that instead of a pure analog output, I could pivot to audio and output a signal to a speaker, which was much more feasible for the board's hardware. After thinking about it some more, I decided to move toward a Step Sequencer. 

![Step Sequencer](../assets/img/posts/step_sequencer/step_sequencer.png)

In this version, I built a grid on the VGA display representing the middle C octave of a piano, shown in the image on the left. Users can interact with the grid to select specific notes, which the FPGA then sequences and plays back in real-time. 

<br>

[![Logic Analyzer Project](https://opengraph.githubassets.com/1/wavius/Step-Sequencer)](https://github.com/wavius/Logic-Analyzer)