# Software Engineering & Testing Laboratory (SE-Lab-1-to-7)

**Institution:** Department of Computer Science & Engineering, PES University  
**Student Name:** PAVAN KISHOR M  
**Course:** Software Engineering (SE) & Requirements Engineering / Software Testing  

---

## 📌 Repository Overview

This repository consolidates the complete coursework, implementation code, automated testing suites, static analysis reports, and formal submission deliverables for **Software Engineering Laboratories 1 through 7**.

Each laboratory is organized into dedicated directories containing production source code, unit/property tests, formal documentation, and analytical verification reports.

---

## 📂 Laboratory Structure & Navigation

| Lab | Module / Directory | Topic & Key Technologies | Deliverables & Artifacts | Status |
|:---:|:-------------------|:-------------------------|:-------------------------|:------:|
| **Lab 1** | [`Multi-Vendor-Artisan-E-Commerce-Marketplace_SE-Lab-1`](./Multi-Vendor-Artisan-E-Commerce-Marketplace_SE-Lab-1) | Requirements Engineering & UML Modeling | • Requirements Table (FR/NFR)<br/>• Use Case Flow Specifications<br/>• UML Use Case Diagrams | **Completed** |
| **Lab 3** | [`L3_31_galaga`](./L3_31_galaga) | Vibe Coding & Game Engine Repair (Pygame) | • Cubic Bézier curve fix<br/>• Dynamic enemy palettes<br/>• Stage banners & wave lifecycle<br/>• Player energy shield mechanics | **Completed** |
| **Lab 4** | [`lab-4`](./lab-4) | Modular Minesweeper Architecture | • Modular terminal game engine<br/>• Recursive cell reveal & flag mechanics<br/>• Forked upstream tracking | **Completed** |
| **Lab 5** | [`L5_31_event_manager`](./L5_31_event_manager) | Static Code Analysis & Security Hardening | • Flake8, Pylint & Bandit audits<br/>• Pre/Post remediation reports<br/>• Vulnerability mitigation & reflection | **Completed** |
| **Lab 6** | [`L6_L7_31_coupon_validator/lab6`](./L6_L7_31_coupon_validator/lab6) | Code & Branch Coverage Testing | • 100% Statement Coverage (`pytest-cov`)<br/>• 100% Branch Coverage (`coverage`)<br/>• Formal Verification Report | **100% (10/10)** |
| **Lab 7** | [`L6_L7_31_coupon_validator/lab7`](./L6_L7_31_coupon_validator/lab7) | Property-Based Fuzz Testing | • Hypothesis fuzz testing suite<br/>• Defensive crash-proofing<br/>• Formal Fuzz Testing Report | **100% (10/10)** |

---

## 🛠️ Laboratory Details

### Lab 1: Requirements Engineering & UML Use-Case Modelling
- **Domain:** Multi-Vendor Artisan E-Commerce Marketplace
- **Scope:** Complete specification of 5 Functional Requirements (FR-001 through FR-005) and 2 Non-Functional Requirements (NFR-001, NFR-002).
- **Deliverables:** Formal requirements matrix, detailed use-case flow specifications with alternate/exception paths, and high-resolution UML diagrams.

### Lab 3: Galaga-Lite Game Repair & Vibe Coding
- **Domain:** Pygame Arcade Game Engine
- **Tasks Completed:**
  1. Fixed entry and dive path cubic Bézier curve calculation for smooth trajectory interpolation.
  2. Implemented wave-based dynamic enemy palette tinting (`enemy_tint`).
  3. Built `on_wave_start` stage banner announcements with smooth fade transitions.
  4. Added player energy shield mechanic with hit charges and visual circular shield aura.
- **Evidence:** Video recordings (`video_before.mp4`, `video_after.mp4`) and AI pair-programming audit logs.

### Lab 4: Minesweeper Architecture
- **Domain:** Terminal Game Mechanics & State Modeling
- **Deliverables:** Architectural reference documentation, modular game state management, and recursive mine reveal algorithms.

### Lab 5: Static Code Analysis — Event Management System
- **Domain:** Code Quality, Style Conformance, and AST Security Auditing
- **Tools:** `pylint`, `flake8`, `bandit`
- **Deliverables:**
  - Initial baseline reports revealing critical security issues (unsafe `pickle` deserialization, mutable default arguments, poor error handling).
  - Remediated `event_manager.py` using secure JSON persistence, validated type annotations, and robust error handlers.
  - Verification reports showing 10/10 Pylint score, 0 Flake8 errors, and 0 Bandit security warnings.

### Lab 6: Code & Branch Coverage Analysis — Coupon Validator
- **Domain:** White-Box Unit Testing & Structural Code Coverage
- **Metrics Achieved:**
  - **Statement Coverage:** 100% (32/32 statements)
  - **Branch Coverage:** 100% (24/24 branches)
- **Artifacts:** Modular test suites (`CodeCoverageTest_coupon_validator.py`, `BranchCoverageTest_coupon_validator.py`, `test_coupon_validator.py`) and formal PDF report.

### Lab 7: Fuzz Testing — Property-Based Input Validation
- **Domain:** Automated Fuzzing & Negative Testing with `Hypothesis`
- **Scope:** Exposing boundary crashes, NaN/Inf floats, type mismatches, unicode anomalies, and negative order values.
- **Resolution:** Production hardening of `coupon_validator.py` with defensive type guards, boundary checks, and graceful validation errors. 100% pass rate under random fuzzing.

---

## 📜 Execution & Testing Guidelines

### Running Tests (Labs 6 & 7)
```bash
# Lab 6 Coverage Suites
cd L6_L7_31_coupon_validator/lab6
pytest --cov=coupon_validator --cov-branch --cov-report=term-missing

# Lab 7 Fuzz Testing Suite
cd ../lab7
pytest test_coupon_validator.py
```

### Running Static Analysis (Lab 5)
```bash
cd L5_31_event_manager
pylint event_manager.py
flake8 event_manager.py
bandit -r event_manager.py
```

### Running Arcade Game (Lab 3)
```bash
cd L3_31_galaga
python3 game.py
```

---

## 📄 License
This repository is released under the MIT License for educational and academic assessment purposes.
