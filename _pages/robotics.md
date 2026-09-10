---
layout: archive
title: "Robotics & Automation"
permalink: /robotics/
author_profile: true
---

{% include base_path %}

Hands-on work in embedded systems, motion control, and digital fabrication. This section collects robotics and automation projects built around microcontrollers, motor drivers, and G-code based tooling.

## 2.5D Mini CNC Plotter

**Course:** Microprocessor and Embedded Systems (MAES)  
**Role:** Core Contributor, First author 
**Team:** Sk. Md. Asif Newaz, Tanvir Shaad, Safin Khan, MD. Shohanul Haque, and Sharon Bhoumick  

This project is a compact, low-cost **2.5D CNC plotter** that draws 2D figures on a plane with a pen. It is built around an Arduino Uno R3 and an L293D motor-controller shield, with two salvaged DVD-drive stepper motors for the X/Y axes and a servo for pen lift (Z). A Java control program on a host computer sends motion commands over the Arduino serial port, either axis-by-axis or by tracing a G-code file of the target drawing.

The machine was demonstrated by plotting a portrait of a faculty member from a G-code file generated from a photograph, then comparing the plot with the original image.

<div class="robotics-video">
  <iframe src="https://www.youtube-nocookie.com/embed/aujCV6kbtAY" title="2.5D Mini CNC Plotter — Microprocessor and Embedded Systems project" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>

<p><a href="https://youtu.be/aujCV6kbtAY">Watch on YouTube</a> &nbsp;|&nbsp; <a href="{{ base_path }}/files/2.5d-mini-cnc-plotter-report.pdf">Download the project report (PDF)</a></p>

### How it works

The plotter positions a pen in the XY plane and lifts or lowers it with a servo. Each stepper motor is driven in 48 steps per revolution, with 100 steps corresponding to 1 mm of travel on each axis. Reversing the Y motor moves the platform forward or backward; reversing the X motor moves the pointing arm left or right.

A host-side Java program communicates with the Arduino Uno over a selected COM port. The operator can jog all three axes independently, or open a `.gcode` file. The script interprets the file and streams coordinated movement commands to the microcontroller so the pen traces the drawing.

Typical demo workflow:

1. Power the plotter and connect the Arduino over USB.
2. Launch the Processing / Java control program and select the device port.
3. Load the G-code file that contains the coordinates of the picture.
4. The machine starts drawing; when it finishes, the plot can be compared with the source image.

### Hardware

* Arduino Uno R3 (ATmega328P) — control and G-code execution
* L293D H-bridge motor-controller shield — stepper power and direction
* Two 2-phase (4-wire) DC stepper motors — X and Y motion (from DVD drives)
* Servo motor — Z-axis pen up / pen down
* 12 V DC supply for the motors, plus mechanical frame, rails, wiring, and pen

The working envelope is about **40 × 40 mm**. Total parts cost was about **2,390 BDT**.

### Results and limits

The plotter produced recognizable drawings, including the AIUB logo and a faculty portrait. The small workspace means artwork must be scaled down, which can introduce imperfections. DVD-drive mechanics are increasingly hard to source, and the current software stack (G-code generation plus a lightweight Java controller) is more involved than a single turnkey app.

Possible next steps from the report include a larger workspace, finer calibration, converting the 2.5D plotter into a mini 3D printer with an additional Z drive, replacing the pen with a laser for engraving, or attaching a drill head for light CNC drilling.
