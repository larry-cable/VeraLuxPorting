# VeraLux Suite for PixInsight

![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)
![Platform](https://img.shields.io/badge/Platform-PixInsight-orange)
![Version](https://img.shields.io/badge/Version-2.0.7-green)

**The Unified Photometric Engine: HyperMetric Stretch & StarComposer.**

> [!IMPORTANT]
> **Original Authorship & Credits**
>
> This script is a port of the original **VeraLux** tools developed for Siril/Python by **Riccardo Paterniti**.
> All credit for the underlying mathematics, the "True Color" methodology, and the sensor weighting logic belongs to him.
>
> *   **Original Project:** [VeraLux.space](https://veralux.space)
> *   **Original Author:** [Riccardo Paterniti](https://github.com/RikyPate)
> *   **License:** GPL-3.0-or-later

---

## 📖 About This Port

This repository houses a **PixInsight JavaScript Runtime (PJSR)** implementation of the VeraLux ecosystem. It unifies two powerful engines into a single interface:

1.  **HyperMetric Stretch (HMS):** A physics-based linear-to-nonlinear stretcher (Ported from Python v1.3.1).
2.  **StarComposer:** A high-fidelity star reconstruction and composition engine (Ported from Python v1.0.2).

### 🤖 Origin Story
This project began as a personal experiment to test the capabilities of modern AI coding assistants in translating complex Python/NumPy logic into PixInsight's specific JavaScript implementation. It has since evolved into a fully maintained suite, ensuring PixInsight users have access to Riccardo's latest photometric methodologies.

---

## ✨ Key Features

### Module 1: HyperMetric Stretch
Operates on the axiom that standard histogram transformations destroy photometric color ratios (hue shifts).

*   **Smart Iterative Solver (New in v2.0):** The "Auto-Calc" now simulates the entire post-stretch scaling pipeline. It detects black clipping ("Floating Sky Check") and iteratively adjusts the target to find the safest maximum contrast.
*   **Unified Color Strategy (New in v2.0):** A single, intuitive slider to balance the equation.
    *   **Left (<0):** Cleans noise by increasing Shadow Convergence.
    *   **Right (>0):** Softens highlights by relaxing Color Grip.
*   **Sensor-Aware:** Expanded database (v2.1) including **Seestar S50/S30**, **IMX585**, and **Narrowband (HOO/SHO)** profiles.

### Module 2: StarComposer
Decouples the star field from the main object to prevent bloating and bleaching.

*   **Star Surgery:** Includes native tools for **Large Structure Rejection (LSR)** (removing galaxy cores from star masks) and **Optical Healing** (fixing chromatic aberration/halos).
*   **Vector Preservation:** Stretches stars without losing their core color temperature.
*   **Auto-Stretch Stars:** A specialized solver that ignores black backgrounds to find the optimal visibility for linear star masks.
*   **Composition Modes:** Choose between **Linear Add** (Physical accuracy) or **Screen** (Safe blending to prevent core saturation).

---

## ⏩ Automatic Installation (Recommended)

1.  Open **PixInsight**.
2.  Go to **Resources > Updates > Manage Repositories**.
3.  Click **Add** and paste the URL: `https://raw.githubusercontent.com/killerciao/VeraLuxPorting/main/`
4.  Click **OK**.
5.  Go to **Resources > Updates > Check for Updates**.
6.  Install the package and **Restart PixInsight**.

---

## 🛠️ Manual Installation

1.  Download the `.zip` file from the latest Release.
2.  Extract `VeraLuxSuite.js`.
3.  Open **PixInsight**.
4.  Go to **Script > Execute Script File...**
5.  Select `VeraLuxSuite.js`.

---

## 🚀 Usage Guide

### [Tab 1] HyperMetric Stretch
*Use this for your main image (Linear).*

1.  **Prerequisites:** Image must be **Linear**, **Background Extracted**, and **Color Calibrated (SPCC)**.
2.  **Mode:** Select **Ready-to-Use** for the new Unified Strategy workflow.
3.  **Sensor:** Select your camera profile (or Rec.709).
4.  **Solve:** Click **⚡ Auto-Calc Log D**. The solver will find the perfect stretch intensity.
5.  **Refine:** Use the **Color Strategy** slider.
    *   Background too noisy? Slide **Left**.
    *   Stars too hard/white? Slide **Right**.
6.  **Process:** Click **PROCESS STRETCH**.

### [Tab 2] StarComposer
*Use this to recombine a Linear Starmask with a Stretched Starless image.*

1.  **Input:** Select your **Starmask (Linear)** and **Starless Base (Stretched)** from the dropdowns.
2.  **Calibrate:** Click **⚡ Auto-Stretch Stars**. This calculates the intensity needed to make linear stars visible.
3.  **Surgery (Optional):**
    *   **LSR:** Increase if your star mask contains pieces of nebulosity or galaxy cores.
    *   **Healing:** Increase if your stars have purple/green halos.
4.  **Process:** Click **PROCESS STAR COMPOSITION**.

---

## 📄 License

This project is licensed under the **GNU General Public License v3.0**.

You are free to use, modify, and distribute this software under the terms of the GPLv3. Any derivative works must also be open-source and preserve the original copyright notices and attribution to Riccardo Paterniti.