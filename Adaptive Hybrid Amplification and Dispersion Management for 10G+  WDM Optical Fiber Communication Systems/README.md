# Adaptive Hybrid Amplification and Dispersion Management for 10G+ WDM Optical Fiber Communication Systems

Project Report | VIT Vellore, School of Electronics Engineering
Simulated using OptiSystem | Bit Rate: 10 Gbps | Wavelength: 1550 nm (C-band)

---

## Overview

This project investigates the design and performance evaluation of a 4-channel and 8-channel WDM optical fiber communication system operating at 10 Gbps. The study systematically compares the impact of dispersion compensation using Dispersion Compensating Fiber (DCF) and hybrid amplification using EDFA combined with Raman amplifiers across single-span and multi-span configurations.

The channel spacing is 100 GHz (0.8 nm) centered around 1550 nm, and performance is evaluated using Q-factor and Bit Error Rate (BER) metrics.

---

## Project Flow

1. Implement a 4-channel WDM system at 10 Gbps
2. Establish feasible transmission length with dispersion disabled
3. Compare performance with and without Dispersion Compensating Fiber (DCF)
4. Compare EDFA-only vs EDFA + Raman hybrid amplification over multiple spans
5. Extend the system to 8-channel WDM

---

## System Configurations Studied

**Single Span (160 km):**
- 4-channel WDM without DCF
- 4-channel WDM with DCF (EDFA + DCF inline compensation)

**Multiple Span (480 km = 3 x 160 km):**
- EDFA + DCF only
- Raman + EDFA + DCF (hybrid amplification)

---

## Key Results

### Case 1 — Dispersion Disabled (Baseline)

Maximum feasible transmission length at 10 Gbps: **160 km**
Q-factor range: 6–7 | BER range: 10^-9

Establishes the performance upper bound with chromatic dispersion as the dominant impairment in uncompensated systems.

---

### Case 2 — EDFA with and without DCF at 160 km

| Configuration | Q-factor (avg) | BER |
|---|---|---|
| EDFA without DCF | ~0–1.6 | ~1 (unusable) |
| EDFA with DCF | 10.6 – 13.5 | 10^-27 to 10^-42 |

Without DCF, accumulated dispersion at 16.75 ps/nm/km over 160 km amounts to 2680 ps/nm, causing complete eye closure and ISI. DCF inline compensation fully restores performance.

---

### Case 3 — Multi-Span (480 km): EDFA-only vs Hybrid EDFA + Raman

| Channel (nm) | Q-factor (EDFA only) | Q-factor (EDFA + Raman) | BER (EDFA only) | BER (EDFA + Raman) |
|---|---|---|---|---|
| 1550 | 5.49 | 8.42 | 1.60E-08 | 1.51E-17 |
| 1550.8 | 4.81 | 6.46 | 6.14E-07 | 4.37E-11 |
| 1551.6 | 5.98 | 7.28 | 8.77E-10 | 1.42E-13 |
| 1552.4 | 7.29 | 7.69 | 1.15E-13 | 5.38E-15 |

Hybrid amplification improves Q-factor by approximately 2–3 dB and BER by approximately 4 orders of magnitude across all channels. All channels exceed the FEC threshold of Q = 6 with the hybrid scheme, restoring system viability at 480 km.

---

## Key Inferences

**Dispersion compensation** is essential at 10 Gbps beyond short distances. Uncompensated chromatic dispersion renders the system completely unusable at 160 km, while inline DCF restores Q-factors above 10.

**EDFA-only multi-span** amplification is insufficient beyond approximately 400 km due to cumulative ASE noise. Channels closer to the EDFA gain peak at 1550 nm perform better due to gain non-uniformity.

**Hybrid EDFA + Raman** amplification provides distributed gain within the transmission fiber itself, reducing the effective noise figure of each amplification stage and suppressing ASE accumulation. This is the preferred configuration for long-haul DWDM transmission.

---

## Repository Structure

```
├── OptiSystem_Files/       # OptiSystem simulation project files
│   ├── 4ch_without_DCF/
│   ├── 4ch_with_DCF/
│   ├── multispan_EDFA/
│   └── multispan_Raman_EDFA/
├── Results/                # Q-factor and BER tables, eye diagrams, optical spectrum plots
├── Block_Diagrams/         # System block diagram screenshots
└── README.md
```

---

## Tools Used

- OptiSystem — optical communication system simulation
- 4-channel and 8-channel WDM at 10 Gbps
- FR4 standard SMF fiber, DCF, EDFA (Black Box), Raman Amplifier (co-propagating pump at 1450 nm, 30 dBm)
