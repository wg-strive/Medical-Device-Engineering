# Software / System Requirements Specification (SRS)
## Medfusion® 3500 Syringe Infusion Pump
**Version:** 0.1  
**Author:** Wenbo Gong  
**Date:** 2025-11-20  

---

## 1. Purpose

The purpose of this Software / System Requirements Specification (SRS) is to define the functional, performance, safety, cybersecurity, and regulatory requirements for the Medfusion® 3500 syringe infusion pump portfolio project.  

This SRS is intended to:
- Provide input to the **Risk Management File (RMF)** per ISO 14971.
- Establish a basis for **V&V planning** (test protocols, traceability matrix).
- Serve as a reference for future **threat modeling** and **cybersecurity analysis**.

---

## 2. Scope

This SRS covers the **system and embedded software** of a smart syringe infusion pump that:

- Delivers fluids/medications from **1 mL to 60 mL** syringes. :contentReference[oaicite:1]{index=1}  
- Operates in acute care settings (ICU, OR, neonatal, pediatric, general infusion). :contentReference[oaicite:2]{index=2}  
- Provides programmable infusion modes (continuous, volume-over-time, body-weight, intermittent, bolus). :contentReference[oaicite:3]{index=3}  
- Uses a drug library with hard/soft limits to support dose-error-reduction. :contentReference[oaicite:4]{index=4}  

Out of scope:
- External hospital IT systems beyond defined interfaces.
- Manufacturing and servicing processes.
- Non-software risk controls (e.g., labeling, packaging) except where referenced.

---

## 3. References

- ISO 13485 – Medical devices – Quality management systems – Requirements for regulatory purposes.
- ISO 14971 – Application of risk management to medical devices. :contentReference[oaicite:5]{index=5}  
- IEC 62304 – Medical device software – Software life cycle processes.
- IEC 60601-1 – Medical electrical equipment – General requirements for basic safety and essential performance.
- FDA Guidance – Cybersecurity in Medical Devices: Quality System Considerations and Content of Premarket Submissions (2023).
- Medfusion® 3500 Syringe Pump manuals and public specifications. :contentReference[oaicite:6]{index=6}  

---

## 3A. Definitions and Acronyms

### 3A.1 Definitions

- **Infusion Mode**  
  A method of delivering medication, such as continuous rate, volume-over-time, weight-based dosing, intermittent, or bolus.

- **Drug Library**  
  A configurable database of medications, dosing parameters, limits, and care-area profiles that supports dose-error-reduction.

- **Care Area Profile**  
  A predefined set of drug configurations tailored to a specific clinical environment (e.g., NICU, ICU, OR).

- **Hard Limit**  
  A non-overridable infusion parameter limit. The system shall not allow infusion parameters outside this range.

- **Soft Limit**  
  An overridable infusion parameter with a warning. The user must acknowledge the warning to proceed.

- **Essential Performance**  
  Performance necessary to maintain basic safety, as defined in IEC 60601-1.

- **Hazardous Situation**  
  Circumstances in which people, property, or the environment are exposed to one or more hazards.

- **Risk Control**  
  A measure implemented to reduce risk to an acceptable level, as defined by ISO 14971.

- **Syringe Detection**  
  The system’s method of identifying syringe size and type through mechanical, optical, or software algorithms.

- **VTBI (Volume To Be Infused)**  
  The total volume of fluid the user programs the device to deliver for an infusion.

---

### 3A.2 Acronyms

- **AC** – Alternating Current  
- **DERS** – Dose Error Reduction System  
- **EMC** – Electromagnetic Compatibility  
- **EMR** – Electronic Medical Record  
- **FDA** – U.S. Food and Drug Administration  
- **IFU** – Instructions for Use  
- **NICU/PICU** – Neonatal/Pediatric Intensive Care Unit  
- **PDMS** – Patient Data Management System  
- **QMS** – Quality Management System  
- **RMF** – Risk Management File  
- **RMP** – Risk Management Plan  
- **RTM** – Requirements Traceability Matrix  
- **SRS** – Software/System Requirements Specification  
- **VTBI** – Volume To Be Infused

---

## 4. System Overview

The Medfusion® 3500 syringe infusion pump is a microprocessor-controlled device that:
- Accepts compatible syringes (1–60 mL).
- Mechanically drives the syringe plunger to deliver fluid at controlled rates.
- Provides a user interface consisting of:
  - Front panel keys and/or soft keys
  - A graphical display
  - Audible/visual alarms
- Stores **drug libraries**, care-area profiles, and logs of infusion events.
- Communicates with external systems (e.g., patient data management systems) via wired or wireless interfaces. :contentReference[oaicite:7]{index=7}  

---

## 5. Intended Use and Use Environment

### 5.1 Intended Use

The syringe pump is intended to **deliver fluids and medications** (e.g., blood products, lipids, antibiotics, enteral solutions, and other therapeutic fluids) via routes including IV, intra-arterial, epidural, intrathecal, subcutaneous, and enteral, with precise control of infusion rate and volume in hospital and clinical environments. :contentReference[oaicite:8]{index=8}  

### 5.2 Intended Users

- Trained healthcare professionals (e.g., anesthesiologists, intensivists, nurses, pharmacists).
- Biomedical engineering staff (device configuration, maintenance).

### 5.3 Use Environment

- Hospital intensive care units, operating rooms, NICU/PICU, and general wards.
- Electromagnetically controlled environment per IEC 60601-1-2 (EMC). :contentReference[oaicite:9]{index=9}  

---

## 6. System Context and Interfaces

### 6.1 System Context

The pump interacts with:
- Patient (receiving infused medication).
- Clinician (programming pump, responding to alarms).
- Hospital IT systems (e.g., EMR, PDMS) via communication interfaces.
- Power sources:
  - AC mains
  - Internal rechargeable battery (approx. 10 h capacity). :contentReference[oaicite:10]{index=10}  

### 6.2 External Interfaces

- **Electrical power input:** 100–240 VAC, 50/60 Hz. :contentReference[oaicite:11]{index=11}  
- **Network/Comms:** IR, serial (e.g., RS-232), optionally Ethernet/Wi-Fi via accessory modules. :contentReference[oaicite:12]{index=12}  
- **Mechanical:** Mounting to IV pole, transport clamps. :contentReference[oaicite:13]{index=13}  

---

## 7. System Constraints and Assumptions

- The device shall comply with applicable standards listed in Section 3.
- Operation is limited to environmental conditions specified in the IFU (temperature, humidity, EMC).
- Only compatible and validated syringes and disposables may be used.
- Users are trained on device operation before use on patients.

---

## 8. Requirements

> **Note:** IDs are structured so you can later map them to risk controls and test cases in your RTM:
> - **FUNC-###** = core functional  
> - **PERF-###** = performance  
> - **SAFE-###** = safety / essential performance  
> - **CYBER-###** = cybersecurity  
> - **USAB-###** = usability / human factors  
> - **REG-###** = regulatory / standards

### 8.1 Functional Requirements (Core Infusion Behavior)

**FUNC-001 – Syringe Size Support**  
The system shall detect and support syringe sizes from **1 mL to 60 mL** from specified manufacturers. :contentReference[oaicite:14]{index=14}  

**FUNC-002 – Infusion Modes**  
The system shall support at least the following infusion modes:
- Continuous rate
- Volume over time
- Body weight / mass-based dosing
- Intermittent
- Bolus

**FUNC-003 – Start/Stop Control**  
The system shall provide dedicated controls to start, pause, and stop an infusion and shall clearly indicate the current infusion state on the display.

**FUNC-004 – Dose Calculation**  
For weight-based infusions, the system shall calculate infusion rate from entered patient weight, concentration, and dose (e.g., µg/kg/min) and display the calculated rate before infusion start.

**FUNC-005 – Drug Library Selection**  
The system shall allow the user to select a **care area profile** and **drug protocol** from a configurable drug library before programming the infusion. :contentReference[oaicite:15]{index=15}  

**FUNC-006 – Alarm Handling**  
The system shall generate and display alarms for, at minimum:
- Occlusion / high pressure
- End of infusion / near end
- Syringe dislodgement / empty syringe
- Door open
- System fault / self-test failure
- Low battery / no AC power

**FUNC-007 – Event Logging**  
The system shall store a log of key events (power on/off, program changes, alarm occurrences, infusion start/stop, user login/logout) with timestamps for at least 1,000 events.

---

### 8.2 Performance Requirements

**PERF-001 – Infusion Accuracy**  
The system shall deliver the programmed infusion rate with an accuracy of **±2%** over the specified operating range, under rated conditions. :contentReference[oaicite:16]{index=16}  

**PERF-002 – Flow Rate Range**  
The system shall support infusion flow rates from **0.01 mL/h to at least 130 mL/h**, depending on syringe size. :contentReference[oaicite:17]{index=17}  

**PERF-003 – Occlusion Detection Time**  
At a flow rate of 1.0 mL/h using a 60 mL syringe, the system shall detect an occlusion and generate an alarm in less than 5 minutes. :contentReference[oaicite:18]{index=18}  

**PERF-004 – Battery Operation**  
On a fully charged internal battery, the system shall support at least **10 hours** of continuous infusion at a nominal rate with a 60 mL syringe. :contentReference[oaicite:19]{index=19}  

---

### 8.3 Safety and Essential Performance Requirements

**SAFE-001 – Default Safe State on Fault**  
On detection of a critical system fault (e.g., watchdog timeout, self-test failure, program memory corruption), the system shall:
- Stop infusion
- Generate a high-priority audible and visual alarm
- Display a clear error message instructing the user to remove the pump from service

**SAFE-002 – Verification of Programmed Parameters**  
Before infusion start or resumption after pause, the system shall display key programmed parameters (drug name, concentration, rate/dose, volume to be infused) for user verification.

**SAFE-003 – Limits Enforcement (Hard Limits)**  
The system shall **prevent** programming of infusion parameters outside configured hard limits for the selected drug and care area profile.

**SAFE-004 – Limits Warning (Soft Limits)**  
When the user attempts to exceed configured soft limits, the system shall present a warning and require explicit confirmation (e.g., extra key press or password) to proceed.

**SAFE-005 – Post-Occlusion Bolus Reduction**  
Upon removal of an occlusion condition, the system shall limit the post-occlusion bolus to < 0.3 mL for a 60 mL syringe at nominal rates. :contentReference[oaicite:20]{index=20}  

**SAFE-006 – Alarm Priority and Differentiation**  
The system shall provide differentiated audible tones and visual indicators for high, medium, and low priority alarms (e.g., occlusion vs. near end vs. advisory).

**SAFE-007 – EMC Immunity / Emissions**  
The system shall meet EMC requirements specified in IEC 60601-1-2 for emissions and immunity for hospital environments, as reflected in the operator’s manual. :contentReference[oaicite:21]{index=21}  

---

### 8.4 Cybersecurity Requirements

(These will tie directly into your threat model + RMS later.)

**CYBER-001 – Authentication for Configuration Changes**  
The system shall require authenticated access (e.g., password or role-based login) for:
- Drug library configuration
- Care area profile changes
- Network communication settings
- Firmware updates

**CYBER-002 – Audit Logging**  
The system shall maintain an audit log recording:
- User ID
- Action performed (e.g., change to limits, new profile)
- Date/time stamp
- Success/failure status  

The audit log shall be protected from tampering and accessible for export.

**CYBER-003 – Secure Communication**  
If the pump communicates over network protocols (e.g., TCP/IP), it shall support:
- Mutual authentication with the peer system
- Encrypted channels (e.g., TLS) to protect PHI and configuration data in transit.

**CYBER-004 – Integrity of Software/Firmware**  
The system shall verify the integrity and authenticity of firmware/software before execution (e.g., digital signatures, secure boot). If verification fails, the system shall not start normal operation and shall indicate an error.

**CYBER-005 – Physical Security**  
Critical ports (service/debug, firmware update, configuration) shall be:
- Physically protected (e.g., behind a locked panel), or
- Logically disabled or access-controlled in clinical use mode.

**CYBER-006 – Security Logging of Cyber Events**  
The system shall log cyber-relevant events (failed logins, configuration changes, firmware update attempts, unexpected reboots) for later forensic analysis.

---

### 8.5 Usability / Human Factors Requirements

**USAB-001 – Display of Drug Name**  
The system shall display the full drug name using strategies such as **TALLman lettering** to distinguish look-alike/sound-alike drug names. :contentReference[oaicite:22]{index=22}  

**USAB-002 – Alarm Visibility**  
When an alarm is active, the alarm status shall be clearly visible at a distance of at least 3 m under typical ward lighting conditions.

**USAB-003 – Confirmation for High-Risk Actions**  
The system shall require explicit confirmation (e.g., additional key press) for high-risk actions such as:
- Stopping an infusion
- Clearing an alarm without resolving the underlying condition
- Overriding soft limits

**USAB-004 – Guided Programming Workflow**  
The system shall guide the user through a stepwise programming workflow, preventing skipping of critical steps (e.g., syringe type selection, care area, drug, units, rate/VTBI).

---

### 8.6 Regulatory / Standards-Driven Requirements

**REG-001 – RMF Integration**  
Each safety-related requirement (SAFE-###, CYBER-###, some FUNC-### and PERF-###) shall be traceable to at least one hazard or hazardous situation and corresponding risk control in the Risk Management File (RMF) per ISO 14971.

**REG-002 – Traceability**  
All requirements in this SRS shall be traceable to upstream inputs (intended use, regulatory requirements, risk analysis) and downstream artifacts (software design specifications, test protocols, and reports).

**REG-003 – Post-Market Feedback**  
The system shall support retrieval of event logs (including alarms, parameter changes, failures) to support post-market surveillance and trending of safety issues.

---

## 9. Open Points / TBDs

- TBD-001: Final list of supported syringe manufacturers and models.  
- TBD-002: Final list of communication protocols and security controls per IT integration strategy.  
- TBD-003: Detailed alarm sound patterns and priorities.  
- TBD-004: Local language support and localization strategy.
