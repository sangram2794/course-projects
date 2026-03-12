# Wideband Circularly Polarised Microstrip Antenna with Defected Ground Structure

> **Research Paper | VIT Vellore | School of Electronics Engineering**  
> Simulated using **CST Microwave Studio** | Target frequency: **3.5 GHz (5G Mid-Band)**

---

## 📡 Overview

This project presents the design and simulation of a **wideband circularly polarised (CP) microstrip patch antenna** integrated with a **dumbbell-shaped Defected Ground Structure (DGS)** for 5G mid-band applications at 3.5 GHz.

Circular polarisation is achieved using the **truncated corner method**, which excites two orthogonal modes with a 90° phase difference. The DGS is etched into the ground plane to improve the **Axial Ratio Bandwidth (ARBW)** and overall impedance matching.

The antenna is designed on an **FR4 substrate** (εr = 4.3, loss tangent ≈ 0.025).

---

## 🎯 Key Results

| Parameter | Without DGS | With DGS |
|---|---|---|
| Return Loss (S11) at 3.5 GHz | -17.25 dB | -14.78 dB |
| Impedance Bandwidth (IBW) | 304 MHz | 278 MHz |
| Axial Ratio at 3.5 GHz | 1.90 dB | 1.59 dB |
| **Axial Ratio Bandwidth (ARBW)** | **74 MHz** | **101 MHz (+36.5%)** |
| Directivity | 5.51 dB | 5.62 dB |
| Gain | 1.87 dB | 1.69 dB |

**Key takeaway:** DGS improved ARBW by **36.5%** at the cost of a slight reduction in impedance bandwidth and gain — a well-understood and acceptable tradeoff for CP antenna design.

---

## 🔧 Design Methodology

The project was developed in **three progressive stages**:

### Stage 1 — Basic Microstrip Patch Antenna
A simple rectangular microstrip patch designed for 3.5 GHz resonance using standard design equations (patch width, effective dielectric constant, length extension).

**Dimensions:**
- Substrate: 35.9 mm × 29 mm
- Patch: 26.3 mm × 19.4 mm
- Feed Width: 3.08 mm
- Substrate Height: 1.6 mm

---

### Stage 2 — Truncated Corner CP Antenna
Corner truncation applied to excite two orthogonal modes with 90° phase difference, generating **Right Hand Circular Polarisation (RHCP)**.

Truncation length: `t ≈ 0.17 × Lp = 3.55 mm`

**Dimensions:**
- Substrate: 29.6 mm × 30.5 mm
- Patch: 20 mm × 20.9 mm
- Feed Width: 1.6 mm
- Substrate Height: 3.6 mm

**Results:** IBW = 304 MHz, ARBW = 74 MHz, AR at 3.5 GHz = 1.90 dB

---

### Stage 3 — DGS Integration (Final Design)
A **dumbbell-shaped DGS** etched into the ground plane to modify surface current distribution and improve ARBW.

**DGS Dimensions:**
- Dumbbell Length: 7.5 mm
- Dumbbell Width: 1.3 mm
- Disc Radius: 1.2 mm

**Results:** IBW = 278 MHz, ARBW = 101 MHz, AR at 3.5 GHz = 1.59 dB

---

## 📁 Repository Structure

```
├── CST_Files/          # CST Microwave Studio project files
├── Results/            # S11, VSWR, Axial Ratio, Gain plots
│   ├── Stage1_BasicPatch/
│   ├── Stage2_CP_Antenna/
│   └── Stage3_DGS/
├── Images/             # RTL views, surface current distributions, 3D gain plots
├── Paper/              # Research paper (PDF)
└── README.md
```

---

## 🛠️ Tools Used

- **CST Microwave Studio** — EM simulation
- **FR4 Substrate** — εr = 4.3, h = 1.6 mm (Stage 1, 3), h = 3.6 mm (Stage 2)

---

## 👥 Authors

| Name | Roll No. | Institute |
|---|---|---|
| Sangram Phadtare | 23BEC0170 | VIT Vellore |
| Abhishek Sharma | 23BEC0272 | VIT Vellore |
| Anurag Ranjan | 23BML0057 | VIT Vellore |

**Guide:** Prof. Poonkuzhali R, School of Electronics Engineering, VIT Vellore

---

## 📚 References

1. A. Lahmissi and M. L. Tounsi, "A new design of a circularly polarized microstrip patch antenna array for 5G communication systems," IC2EM, 2025.
2. S. Saha et al., "Circular polarized MIMO antenna with plus shaped DGS for ISM range spectrum application," ICCIT, 2024.
3. Sridhar P. and Poonkuzhali R., "A dual-band circular polarized CPW-fed low-profile antenna for WLAN and X-band applications," Results in Engineering, vol. 27, 2025.
4. A. Almeida et al., "Design of circularly polarized antenna for UWB applications," ARPN J. Eng. Appl. Sci., 2016.

---

## 🏷️ Topics

`microstrip-antenna` `circular-polarisation` `defected-ground-structure` `5g` `cst-microwave-studio` `antenna-design` `rf-engineering` `electromagnetics` `vit-vellore`
