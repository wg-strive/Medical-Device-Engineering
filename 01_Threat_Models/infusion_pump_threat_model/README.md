# Infusion Pump Threat Model

This folder contains a complete threat model for a network-connected infusion pump.  
The objective is to demonstrate practical application of **FDA Cybersecurity Guidance (2023)**, **AAMI TIR57**, **IEC 81001-5-1**, and **secure-by-design principles** in a regulated medical device context.

The threat model includes:
- System architecture diagram  
- Data Flow Diagram (DFD)  
- Trust boundary definition  
- STRIDE analysis  
- CVSS scoring for prioritized threats  
- Recommended mitigations and controls  

All content is original and not derived from proprietary systems.

---

## Device Overview

A modern infusion pump typically includes:
- Pump head + motor control  
- Local UI (touchscreen or membrane keypad)  
- Drug library / dose safety limits  
- Wi-Fi or Ethernet connectivity  
- Integration with EMR / HIS systems  
- Centralized drug library updates  
- Event logs transmitted to hospital servers  

This model evaluates cybersecurity risks associated with both **local** and **networked** functions.

---

## Included Artifacts

### ** 1. System Architecture Diagram**
Illustrates major hardware, firmware, and software components:
- MCU / pump controller  
- Wireless module  
- UI processor  
- Drug library storage  
- Logging subsystem  
- Backend integrations  

(See: `system_architecture.png`)

---

### ** 2. Data Flow Diagram (DFD)**
Defines:
- External entities (nurse, EHR server, update server)  
- Processes (dose calculation, infusion control, drug library sync)  
- Data stores (drug library, logs)  
- Flows with trust boundaries  

(See: `dfd.png`)

---

### ** 3. Trust Boundaries**
Key trust boundaries analyzed:
- Clinical network vs. pump internal network  
- UI interaction boundary  
- Firmware update boundary  
- Drug library update boundary  
- Log transmission boundary  

---

### ** 4. STRIDE Analysis**
A structured analysis using STRIDE:
- **S**poofing  
- **T**ampering  
- **R**epudiation  
- **I**nformation Disclosure  
- **D**enial of Service  
- **E**levation of Privilege  

The table includes:
- Threat source  
- Impacted assets  
- Pre-mitigation risk  
- Recommended controls  

(See: `stride_table.xlsx` or PDF)

---

### ** 5. CVSS Scoring**
Top threats are scored using **CVSS v3.1** to prioritize:
- Network-based attacks  
- Firmware manipulation  
- Authentication bypass  
- Drug library tampering  
- DoS via malformed messages  

(See: `CVSS_calculations.xlsx`)

---

### ** 6. Mitigations & Controls**
Recommended mitigations follow:
- **Secure boot & signed firmware**  
- **Encrypted drug library updates**  
- **Role-based access control (RBAC)**  
- **TLS-secured network communication**  
- **Logging and tamper-evident event records**  
- **Input validation for all control messages**  
- **Hardening of wireless stack**  
- **Separation of clinical vs. management interfaces**  

Mapped to:
- FDA Cybersecurity Controls  
- AAMI TIR57  
- IEC 81001-5-1 foundational practices  

---

## Purpose

This threat model demonstrates competency in:
- Medical device cybersecurity risk analysis  
- Secure system design  
- Threat classification (STRIDE)  
- Risk scoring (CVSS)  
- Regulatory-aligned documentation  
- Clear and defensible engineering reasoning  

It is part of expanding my expertise in **systems engineering**, **V&V**, and **cybersecurity** within the medical device industry.

---
