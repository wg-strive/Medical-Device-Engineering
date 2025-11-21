# Software System Test Cases (SSTC)
## Medfusion® 3500 Syringe Infusion Pump
**Document ID:** SSTC-MF3500  
**Version:** 0.2  
**Author:** Wenbo Gong  
**Date:** 2025-11-20  

---

## 1. Purpose

This Software System Test Case (SSTC) document defines verification tests for software and system requirements described in the **SRS_Medfusion3500.md**.  
Each test case links directly to its originating SRS requirement(s) and provides structured inputs and expected results.

Execution procedures (step-by-step actions) will be defined separately in the **SSTP_Medfusion3500.md**.

---

## 2. Scope

This document includes test cases covering:  
- Functional requirements  
- Performance requirements  
- Safety & essential performance  
- Cybersecurity requirements  
- Usability requirements  

Hardware-only tests (mechanical, EMC, environmental) are outside this SSTC’s scope.

---

## 3. References

- SRS_Medfusion3500.md  
- ISO 14971  
- IEC 62304  
- IEC 60601-1  
- FDA Cybersecurity Guidance (2023)  
- SSTP_Medfusion3500.md (procedures)  
- RTM_Medfusion3500.md (traceability matrix)  

---

## 4. Traceability Summary (Mini-RTM)

| Requirement ID | Short Description | Test Case ID |
|----------------|-------------------|--------------|
| FUNC-001 | Syringe size detection | TC-FUNC-001-01 |
| FUNC-002 | Infusion modes available | TC-FUNC-002-01 |
| FUNC-007 | Event logging | TC-FUNC-007-01 |
| PERF-001 | Infusion accuracy ±2% | TC-PERF-001-01 |
| PERF-003 | Occlusion detection time | TC-PERF-003-01 |
| SAFE-001 | Safe state on critical fault | TC-SAFE-001-01 |
| SAFE-003 | Hard limit enforcement | TC-SAFE-003-01 |
| CYBER-001 | Authentication for config changes | TC-CYBER-001-01 |
| CYBER-004 | Firmware integrity verification | TC-CYBER-004-01 |
| USAB-001 | TALLman drug name display | TC-USAB-001-01 |

---

# 5. Test Cases

Each test case includes:

- **Test Case ID**  
- **Related SRS Requirement(s)**  
- **Test Inputs (parameters, triggers, conditions)**  
- **Expected Results**  
- **Test Type**  
- **Reference (for RTM/SSTP linking)**  

---

## 5.1 Functional Test Cases

### **TC-FUNC-001-01 — Syringe Size Detection**
**Related Requirement(s):** FUNC-001  
**Test Inputs:**  
- Insert syringes of sizes 1 mL, 3 mL, 10 mL, 20 mL, 30 mL, 60 mL  
- Include one unsupported syringe model  
**Expected Results:**  
- Device identifies all supported syringe sizes correctly  
- Unsupported syringe triggers warning or rejection  
**Test Type:** Functional  
**Reference:** SRS FUNC-001  

---

### **TC-FUNC-002-01 — Infusion Mode Availability**
**Related Requirement(s):** FUNC-002  
**Test Inputs:**  
- Navigate mode selection menu with a compatible syringe installed  
**Expected Results:**  
- Continuous, VTBI, weight-based, intermittent, and bolus modes are displayed and selectable  
**Test Type:** Functional  
**Reference:** SRS FUNC-002  

---

### **TC-FUNC-007-01 — Event Logging**
**Related Requirement(s):** FUNC-007  
**Test Inputs:**  
- Power on/off sequence  
- Infusion start/stop  
- Rate change  
- Simulated recoverable alarm  
**Expected Results:**  
- All events logged with correct timestamps and in correct order  
**Test Type:** Functional  
**Reference:** SRS FUNC-007  

---

## 5.2 Performance Test Cases

### **TC-PERF-001-01 — Infusion Accuracy ±2%**
**Related Requirement(s):** PERF-001  
**Test Inputs:**  
- 60 mL syringe  
- Infusion rates: low, nominal, and high  
**Expected Results:**  
- Delivered rate within ±2% of programmed value for all tested conditions  
**Test Type:** Performance  
**Reference:** SRS PERF-001  

---

### **TC-PERF-003-01 — Occlusion Detection Time**
**Related Requirement(s):** PERF-003  
**Test Inputs:**  
- Infusion at 1.0 mL/h  
- Apply downstream occlusion  
**Expected Results:**  
- Occlusion alarm occurs within max allowed detection time  
**Test Type:** Performance  
**Reference:** SRS PERF-003  

---

## 5.3 Safety Test Cases

### **TC-SAFE-001-01 — Safe State on Critical Fault**
**Related Requirement(s):** SAFE-001  
**Test Inputs:**  
- Induce simulated system fault (watchdog timeout or memory error)  
**Expected Results:**  
- Infusion stops  
- High-priority alarm activates  
- Fault message displayed  
**Test Type:** Safety  
**Reference:** SRS SAFE-001  

---

### **TC-SAFE-003-01 — Hard Limit Enforcement**
**Related Requirement(s):** SAFE-003  
**Test Inputs:**  
- Attempt to program infusion parameters exceeding configured hard limits  
**Expected Results:**  
- Entry blocked  
- Clear message displayed  
- Infusion cannot start  
**Test Type:** Safety  
**Reference:** SRS SAFE-003  

---

## 5.4 Cybersecurity Test Cases

### **TC-CYBER-001-01 — Authentication Required for Configuration**
**Related Requirement(s):** CYBER-001  
**Test Inputs:**  
- Attempt to modify drug library, network settings, or firmware update without valid login  
**Expected Results:**  
- Authentication is required  
- Unauthorized access is blocked  
**Test Type:** Cybersecurity  
**Reference:** SRS CYBER-001  

---

### **TC-CYBER-004-01 — Firmware Integrity Validation**
**Related Requirement(s):** CYBER-004  
**Test Inputs:**  
- Provide modified or corrupted firmware file  
**Expected Results:**  
- Firmware rejected  
- Integrity failure error displayed  
- Device prevents boot/update  
**Test Type:** Cybersecurity  
**Reference:** SRS CYBER-004  

---

## 5.5 Usability Test Cases

### **TC-USAB-001-01 — TALLman Drug Name Display**
**Related Requirement(s):** USAB-001  
**Test Inputs:**  
- Access drug list containing LASA drugs requiring TALLman formatting  
**Expected Results:**  
- Proper TALLman capitalization displayed  
- No truncation or formatting errors  
**Test Type:** Usability  
**Reference:** SRS USAB-001  

---

## 6. Document Control

| Version | Date | Author | Description |
|--------|------|---------|-------------|
| 0.2 | 2025-11-20 | W. Gong | Updated format — removed test steps, added inputs/expected results |

