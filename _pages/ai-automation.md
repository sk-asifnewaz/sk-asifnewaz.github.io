---
layout: archive
title: "AI Automation and Robotics"
permalink: /ai-automation/
author_profile: true
redirect_from:
  - /robotics/
---

{% include base_path %}

Work in conversational AI for commerce, workflow automation, embedded systems, and digital fabrication.

## Pears Bargain Bot

**Client:** [Pears International](https://pearsintl.com/) ([Facebook](https://www.facebook.com/pearsintl))

**Role:** Designer and implementer

**Period:** June 2026

Pears International is a Bangladeshi Facebook-commerce retailer selling hair-care products (including Dexe Black/Brown Hair Shampoo) through Messenger. Lead conversion used to depend on manual chatting: inquiries arrive at odd hours, each thread needs product knowledge plus price negotiation in Bangla, and that does not scale when ads spike.

I built an autonomous Messenger sales agent on self-hosted **n8n**, with LLMs via **OpenRouter**. The bot greets customers, answers product FAQs, bargains within encoded price rules, and confirms orders — in natural Bangla, including **voice notes** transcribed with Groq Whisper (`whisper-large-v3-turbo`). Confirmed orders are forwarded to an admin **Telegram** bot for fulfillment.

<p><a href="https://pearsintl.com/">pearsintl.com</a> &nbsp;|&nbsp; <a href="https://www.facebook.com/pearsintl">Facebook page</a> &nbsp;|&nbsp; <a href="{{ base_path }}/files/pears-international-ai-automation-documentation.docx">Download the technical documentation</a></p>

### How it works

Each incoming Messenger event is acknowledged immediately (HTTP 200) so Facebook does not retry aggressively. A short-lived message-ID gate then drops duplicate deliveries. Echo events from manual admin replies are filtered out so the bot does not talk over a human.

Text goes straight into the AI pipeline. Voice attachments are downloaded, transcribed in Bengali, and merged onto the same `messageText` field so the rest of the flow is voice-agnostic. The customer is looked up via the Graph API and PostgreSQL chat memory (keyed by Messenger PSID). An intent classifier sends the turn to one of two LangChain agents that share that memory:

* **FAQ agent** — ingredients, usage, suitability, color variants, and service questions
* **Bargaining agent** — list price, discounts, delivery, and order confirmation

Replies go out through the Messenger Send API. When the customer agrees and gives name, address, and phone, Telegram notifies the shop for packing and delivery.

The bargaining agent is constrained by business rules in the system prompt: a hard price floor, a small discount ladder over at most two rounds, free delivery as a last concession (60 BDT inside Dhaka, 120 BDT outside), a defined close after further haggling, and no invented answers for unknown products. Bulk orders (3+ units) are escalated for a human callback.

### Stack

* n8n (self-hosted, v2.23.2) — workflow orchestration
* OpenRouter — multi-model LLM routing
* Groq Whisper large-v3-turbo — Bangla voice transcription
* PostgreSQL (`n8n_chat_histories`) — per-customer memory
* Facebook Messenger Platform — inbound webhook and outbound replies
* Telegram Bot API — order notifications

### Outcomes (June 2026)

During the live month the system handled **339** Messenger conversations, **2,470** API requests, and **9.88 million** LLM tokens. **26** conversations became confirmed orders — a **7.67%** conversation-to-order rate with little human intervention except edge cases.

Operational issues that were fixed in production included Facebook webhook retries (duplicate replies), OpenRouter response caching that reused stale completions across customers, n8n Code-node binary handling for Groq audio, and pausing the bot when an admin replied manually.

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
