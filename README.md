# AutoRoller

**Demand-triggered, waterless cleaning for rooftop solar panels.**
An SS TechHub project · Smart India Hackathon 2026 (Student Innovation)

AutoRoller is a clip-on unit that keeps a solar panel clean without water, labour, or grid power. A dust sensor watches how much dust has built up on the glass. When the dust starts costing real energy, the unit runs a dry microfiber cleaning cycle, then parks itself fully off the glass so it never shades the cells. It runs from its own battery, charged by the panel it cleans.

> **Status:** concept and prototype stage. No production hardware yet.

---

## Why it matters

- **Dust quietly steals output.** Uncleaned panels in India can lose around 0.3–0.5% of their output every day.
- **Manual cleaning costs money and water.** Crews, rooftop risk, and 3–8 litres of water per panel per wash.
- **Fixed schedules miss the point.** Cleaning on a timer either wastes effort or lets dust build up between visits.

AutoRoller cleans **only when it's needed**, **dry**, and **automatically**.

## How it works

1. **Sense:** a dust sensor and the panel's own output show how much dust has built up.
2. **Decide:** an ESP32 controller cleans only when dust loss passes a set limit, and holds off during quiet hours (such as early-morning dew) or when the battery is low.
3. **Clean:** a stepper motor runs the dry microfiber cleaning cycle, powered by the buffer battery rather than the panel's live output.
4. **Park and report:** the unit parks off the glass, logs the clean, and updates the mobile app.

A manual button and the app can also start a clean on demand.

### Main components

| Part | Role |
|---|---|
| ESP32 controller | Runs the control logic, reads sensors, drives the motor, links to the app over Wi-Fi / Bluetooth |
| Dust sensor (optical or capacitive, under evaluation) | Measures dust build-up on the glass |
| Stepper motor + driver | Runs the cleaning cycle with precise step counts |
| CC/CV charge controller + LiFePO4 battery with BMS | Stores energy from the panel for cleaning |
| Clamp-on housing | Fits the existing panel frame with no drilling or modification |
| Button + status LED, mobile app | Manual cleaning, status, quiet hours, history |

---

## What's in this repository

```
AutoRoller/
├── README.md                          this file
├── LICENSE                            proprietary licence (all rights reserved)
├── viewer/                            autoroller-viewer: interactive 3D model, pip-installable
│   ├── pyproject.toml
│   ├── README.md
│   └── src/autoroller_viewer/
│       ├── cli.py                     local server + browser launcher
│       └── static/                    viewer page and bundled three.js
└── blender/
    └── autoroller_exterior_blender.py builds the 3D exterior model in Blender
```

Both models show the **exterior only**: the panel, the clamped housing, the sensor, and the power module.

---

## Getting started

### 3D viewer (Python 3.8+)

No other dependencies are needed, and it works offline because three.js is bundled.

```bash
cd viewer
python -m pip install .
python -m autoroller_viewer
```

The model opens in your browser. Press **Ctrl+C** in the terminal to stop.

| Option | What it does |
|---|---|
| `--port 9000` | Serve on a different port (default 8765) |
| `--no-browser` | Start the server without opening a browser |

On Windows, if `pip` is not recognised, always use `python -m pip`, as shown above.

**In the viewer:** drag to rotate, scroll to zoom, right-drag to pan, and click a part to highlight it. For slide screenshots, tick *Plain white background* and press **H** to hide the controls.

### Blender model (Blender 3.6 or 4.x)

1. Open Blender and go to the **Scripting** tab.
2. Open `blender/autoroller_exterior_blender.py` and click **Run Script**.
3. The model appears in a collection called `AutoRoller_Exterior`, with a camera and light ready to render.

The panel size and tilt are set at the top of the script. Running it again replaces the model cleanly.

---

## Roadmap

- [x] Concept, control logic, and system architecture
- [x] 3D exterior model and interactive viewer
- [ ] Bench prototype: sensor selection, power system, cleaning cycle
- [ ] Rooftop field trial to measure real dust loss and savings
- [ ] Mobile app
- [ ] Future optical add-on through a modular port

## Intellectual property

A related Indian patent application has been filed and published: **No. 202641087562 A** (Patent Office Journal No. 33/2026). The applicant is Meenakshi Sundararajan Engineering College.

Nothing in this repository grants any licence under any patent or patent application.

## Licence

**Proprietary. All rights reserved.** See [LICENSE](LICENSE). You may not copy, modify, distribute, or use this code or these designs without written permission.

Third-party software keeps its own licence. [three.js](https://threejs.org) is bundled under the MIT licence; see `viewer/src/autoroller_viewer/static/vendor/THREEJS_LICENSE.txt`.

## Team and contact

**Siddharth S S**, SS TechHub
Meenakshi Sundararajan Engineering College, Chennai

For permissions, collaboration, or pilot installations, contact: `[your email]`
