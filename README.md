# FloodGuard: IoT-Based Flood Early Warning System for Riverside Villages

**Course:** Software Engineering and Project Management
**Student:** Jubayer Ahmed (IT24027), Dept. of ICT, MBSTU
**Supervisor:** Professor Dr. Md. Ziaur Rahman
**Level:** 3rd Year, 1st Semester
**Document type:** Project Proposal (initial version)

> Full proposal (LaTeX template): [`report/main.pdf`](report/main.pdf) | Source: [`report/main.tex`](report/main.tex)
> This README summarises the whole proposal, so the main points can be read here without opening other files.

---

## 1. Project in one paragraph

Riverside communities along the Jamuna (including parts of Tangail) often receive flood warnings late, or in a form that does not reach households. **FloodGuard** is a low-cost IoT prototype: an **ESP32** with an **ultrasonic sensor** measures river water level and sends it over WiFi (HTTP POST) to a **Java Servlet** server. The server compares the level with the river's danger level, classifies it as **Safe / Warning / Danger**, stores history, and notifies people through a **web dashboard**, **LED/buzzer** at the device, and **Telegram / simulated SMS**.

## 2. Problem statement

- Village-level water monitoring is mostly manual and irregular.
- Official bulletins (FFWC/BWDB) are periodic and station-level; they do not directly reach every household.
- Residents and volunteers have no automatic, threshold-based alert for their nearest river point.
- Existing solutions are costly or need specialised infrastructure.

## 3. Objectives

1. Measure water level using ESP32 + ultrasonic sensor (HC-SR04 / JSN-SR04T).
2. Send readings to a Java Servlet server over WiFi (HTTP).
3. Classify status: **Safe** (< 80% of danger level), **Warning** (80% to < 100%), **Danger** (>= 100%).
4. Show live status, graph and alert history on a web dashboard.
5. Give local alarms (LED, buzzer) and notifications (console SMS simulation, Telegram).
6. Apply software engineering practice: Incremental model, UML, testing, documentation.

## 4. Scope and limitations

- **In scope:** single river-point node, server-side processing, web dashboard, alert history, roles (Admin, Volunteer, Resident), simulated and real sensor input, UML design, LaTeX documentation.
- **Out of scope:** forecasting / machine learning, nationwide deployment, paid SMS gateway, mobile app, weatherproof enclosure and solar power design.
- **Limitation:** water level is **emulated** (Wokwi or bench test); no live river measurement is claimed. FloodGuard is a decision-support aid and does **not** replace official FFWC forecasts.

## 5. Status logic (core rule)

```
level = H - d          (H = sensor height above river bed, d = measured distance)
p     = level / DangerLevel * 100
Safe    if p < 80
Warning if 80 <= p < 100
Danger  if p >= 100
```

## 6. Software process model: Incremental

Chosen because the system has separable parts (data pipeline, dashboard, alerting) and a single developer works in a fixed time box; a working product is delivered early and extended in each increment.

| Increment | Content | Output |
|---|---|---|
| Planning & Design | Problem analysis, requirements, schedule, UML | Proposal, diagrams |
| Increment 1 | Servlet `/data`, River/Sensor/Reading/Alert classes, status logic, storage | Working data pipeline |
| Increment 2 | Dashboard (colours, progress bar, Chart.js graph), alert list, simulation button | Live dashboard |
| Increment 3 | Role-based login, notifications (console/Telegram), ESP32 + LEDs/buzzer, Wokwi | Complete prototype |
| Testing & Closure | JUnit and system tests, report, GitHub release | Final submission |

## 7. Schedule (12 weeks) and milestones

| Week | Activity | Milestone |
|---|---|---|
| 1-2 | Idea finalisation, problem analysis, requirements, SWOT | M1 |
| 2-3 | Process model, schedule, Gantt chart | M2 |
| 3-5 | UML diagrams (DFD, Use case, Activity, ER, Class, Object) | M3 |
| 5-7 | Increment 1: Servlet, model classes, storage | M4 |
| 7-9 | Increment 2: dashboard, chart, alert list | M5 |
| 9-10 | Increment 3: login, Telegram, ESP32/Wokwi | M6 |
| 10-11 | Testing and bug fixing | M7 |
| 11-12 | Final report (LaTeX), GitHub, submission | M8 |

**Deliverables:** requirements + SWOT (M1), schedule + Gantt + risk register (M2), six UML diagrams (M3), data pipeline source code (M4), dashboard with graph and alerts (M5), integrated system + ESP32 code + Wokwi project (M6), test cases and report (M7), final report PDF + GitHub repository (M8).
The **Gantt chart** is Figure 1 in the proposal PDF.

## 8. UML diagrams (all in the proposal PDF, Section 13)

| Diagram | Where |
|---|---|
| Data Flow Diagram (Level 0 and Level 1) | Figures 3 and 4 |
| Use Case Diagram | Figure 5 |
| Activity Diagram (processing a reading) | Figure 6 |
| Entity Relationship Diagram | Figure 7 |
| Class Diagram | Figure 8 |
| Object Diagram | Figure 9 |

## 9. Classes planned for the simple interface

The proposal plans a browser dashboard served by a Java Servlet using **at least 5 classes from the class diagram**:
`River`, `WaterSensor`, `SensorReading`, `Alert`, `AlertService` (plus `NotificationService` implementations such as `TelegramService` and `ConsoleSmsService`).
The status logic of `River.checkStatus()` is shown as a code listing in the proposal (Section 14).

## 10. Other proposal contents

SWOT analysis, functional requirements (FR1-FR11), non-functional requirements (NFR1-NFR7), feasibility study (technical, economic, operational, schedule, legal), risk register (9 risks with mitigation), cost estimate (hardware about BDT 750-1,100, or BDT 0 with Wokwi simulation), testing plan (T1-T6), conclusion and future work.

## 11. Technology stack

| Layer | Technology |
|---|---|
| Device | ESP32, HC-SR04 / JSN-SR04T, LEDs, buzzer (Arduino C++), Wokwi simulator |
| Backend | Java 17, Jakarta Servlet, DAO pattern, Maven, Jetty |
| Database | ArrayList (initial), MySQL / SQLite |
| Frontend | HTML, CSS, JavaScript, Chart.js |
| Notification | Console SMS simulation, Telegram Bot API |
| Tools | IntelliJ IDEA, Git/GitHub, Overleaf, PlantUML/TikZ, JUnit |

## 12. Repository structure

```
FloodGuard/
├── README.md        <- this file
├── .gitignore
├── report/
│   ├── main.tex     <- LaTeX proposal source
│   └── main.pdf     <- compiled proposal
├── src/             <- Java code (added after proposal approval)
└── wokwi/           <- ESP32 circuit and code (added later)
```

## 13. Current status

| Part | Status |
|---|---|
| Proposal, requirements, risk, cost, schedule, Gantt | Done |
| Six UML diagrams | Done |
| Java Servlet dashboard (5+ classes) | Planned (Increments 1-3) |
| ESP32 / Wokwi circuit | Planned (Increment 3) |

## 14. How to build the proposal

The proposal uses a LaTeX template. Open `report/main.tex` in Overleaf, or run:

```
cd report
pdflatex main.tex
pdflatex main.tex     # run twice for table of contents and numbering
```

## Notes

- Do not commit Telegram tokens or passwords. Use environment variables.
- Water level is emulated in the prototype demo.
