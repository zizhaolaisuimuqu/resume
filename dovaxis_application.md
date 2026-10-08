# DOVAXIS — Software Engineering Intern, Applied AI & Agentic Development

Project: [Quotaquarium](https://github.com/zizhaolaisuimuqu/Quotaquarium)

## 1. What did you build, and who was it for?

I built Quotaquarium, a standalone ESP32-S3 device that turns Codex usage limits into an animated, touch-controlled aquarium. Remaining quota becomes the water level, while consumption, reset windows, account state, and local weather drive the display. I originally built it for my own desk because checking usage across accounts interrupted my work, then documented and published it so other developers could build and adapt it.

## 2. How did you use a coding agent?

I used Codex throughout the engineering workflow rather than only for code completion. I asked it to explore the existing C++ codebase, trace state across UI and network modules, propose scoped implementation plans, edit and refactor files, run PlatformIO builds, and investigate compiler or runtime symptoms. I reviewed its diffs and assumptions, kept control of architecture and product decisions, and iterated with it until the behavior was understandable and verifiable.

## 3. What did the agent get wrong, and how did you catch or fix it?

During the IMU-based water-leveling work, an agent-generated change treated the landscape coordinate transform as if it used the same sign convention as portrait mode. The firmware compiled, but on the physical device the water tilted in the wrong direction in landscape orientation. I reproduced the issue by rotating and tilting the board through each orientation, traced the transformed acceleration values into the renderer, corrected the landscape mapping, and kept the fix as a focused commit rather than accepting the initially plausible output.

## 4. How did you verify the result worked?

I ran the PlatformIO build, flashed the firmware to the Waveshare ESP32-S3 board, and tested the display in all four orientations while tilting it along both axes. I compared the physical response with the expected gravity direction, monitored runtime diagnostics for state or sensor anomalies, and repeated the test after reviewing the final diff. More broadly, I verify Quotaquarium changes with clean builds, hands-on device testing, bounded logs, and synthetic capture modes that avoid exposing account or credential data.
