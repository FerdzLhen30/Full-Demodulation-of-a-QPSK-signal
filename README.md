# Full-Demodulation-of-a-QPSK-signal
This repository presents an experimental analysis of Quadrature Phase Shift Keying (QPSK), covering serial-to-parallel conversion, signal modulation, channel impairments, coherent demodulation, and noise effects. The project demonstrates how In-phase (I) and Quadrature (Q) components are used to reconstruct the original digital data stream.

# QPSK Demodulation and Signal Reconstruction Study

This repository documents a complete laboratory investigation of **Quadrature Phase Shift Keying (QPSK)**, covering signal generation, channel effects, coherent demodulation, and digital data recovery. The objective is to demonstrate how a complex QPSK waveform can be separated into its **In‑phase (I)** and **Quadrature (Q)** components to reconstruct the original serial bitstream.

---

## Table of Contents
- [Part A: Validation of Serial-to-Parallel Conversion](#part-a-validation-of-serial-to-parallel-conversion)
- [Part B: QPSK Signal Formation](#part-b-qpsk-signal-formation)
- [Part C: Channel Impairment Simulation](#part-c-channel-impairment-simulation)
- [Part D: Coherent Demodulation and Data Recovery](#part-d-coherent-demodulation-and-data-recovery)
- [Part E: Noise Effects on Demodulated Data](#part-e-noise-effects-on-demodulated-data)
- [Results and Analysis](#results-and-analysis)
- [Project Assets](#project-assets)

---

## Background and Objective

Quadrature Phase Shift Keying (QPSK) is a digital modulation technique that maps **two bits per symbol** by selecting one of four discrete carrier phase states. This experiment focuses on **coherent QPSK demodulation**, where accurate carrier phase reference is used to separate the received signal and recover the original digital data.

QPSK is conceptually derived from Binary Phase Shift Keying (BPSK). While BPSK transmits one bit per symbol, QPSK transmits two bits simultaneously by using orthogonal carrier components. This does not inherently increase raw bit speed; instead, it reduces the symbol rate and improves **spectral efficiency**, allowing better bandwidth utilization in communication systems.

<img width="963" height="762" alt="image" src="https://github.com/user-attachments/assets/693d42ea-eab1-48c6-9243-efc6a151d0c9" />

*Figure A: Mathematical block representation of QPSK modulation.*

At the transmitter, the serial data stream is divided into alternating bits. One stream modulates the cosine carrier (In‑phase), while the other modulates a sine carrier shifted by 90° (Quadrature). These orthogonal components share the same frequency band but remain separable due to phase orthogonality.

<img width="950" height="390" alt="image" src="https://github.com/user-attachments/assets/57e5c50f-0976-4c40-a312-d312e65f969b" />


*Figure B: Mathematical block representation of QPSK demodulation.*

At the receiver, synchronized reference carriers are used to extract the I and Q components. These are then converted back into digital form and recombined to reconstruct the original data sequence.

---

## Part A: Validation of Serial-to-Parallel Conversion

QPSK transmission requires converting a high‑speed serial bitstream into two lower‑rate parallel streams.

### Procedure
- A **2 kHz pseudo‑random binary sequence (PRBS)** was applied to a Serial‑to‑Parallel (S/P) converter.

### Observations
- Each output channel (I and Q) operated at **1 kbps**, confirming correct bit separation.

### Technical Insight
- Alternate bits are distributed to the I and Q channels using a common clock, effectively doubling the symbol duration and enabling quadrature modulation.

### A.1 Experimental Setup
<details>
<summary>View Diagrams</summary>

![S/P Setup](Diagrams/fig3.jpeg)
![S/P Diagram](Diagrams/fig4.jpeg)

</details>

### A.2 Measured Results
<details>
<summary>View Waveforms</summary>

![S/P Output](Waveform_Captures/1.jpeg)
![I Channel](Waveform_Captures/2rier.
- The Q data stream modulated the sine carrier.

### Output
- Both modulated signals were summed to produce a constant‑amplitude carrier with four phase states corresponding to bit pairs.

### B.1 Modulator Diagrams
<details>
<summary>View Diagrams</summary>

![QPSK Modulator](Diagrams/fig11.jpeg)
![Signal Combiner](Diagrams/fig12.jpeg)

</details>

### B.2 Modulated Signal Results
<details>
<summary>View Waveforms</summary>

![QPSK Output](Waveform_Captures/9.jpg)
![Phase States](Waveform_Captures/13.jpg)

</details>

---

## Part C: Channel Impairment Simulation

To model real transmission conditions, the QPSK signal was passed through a configurable channel.

### Implementation
- Channel gain and phase delay were adjusted to simulate propagation effects.

### Observations
- Phase rotation displaced the constellation points, demonstrating sensitivity to carrier synchronization errors.

### Significance
- Accurate phase tracking at the receiver is critical to avoid symbol decision errors.

### C.1 Channel Setup
<details>
<summary>View Diagram</summary>

![Channel Model](Diagrams/fig15.jpeg)

</details>

### C.2 Output Signal
<details>
<summary>View Results</summary>

![Channel Output](Waveform_Captures/27.jpg)

</details>

---

## Part D: Coherent Demodulation and Data Recovery

The receiver extracts the transmitted data using coherent detection.

### Demodulation Steps
- The received signal was split into I and Q paths.
- Each path was multiplied with a synchronized **100 kHz local oscillator**.
- Low‑pass filters removed unwanted high‑frequency components.

### Data Reconstruction
- The recovered I and Q streams were recombined using a Parallel‑to‑Serial (P/S) converter to restore the original **2 kHz serial data**.

### D.1 Demodulator Architecture
<details>
<summary>View Diagrams</summary>

![Demodulator](Diagrams/fig17.jpeg)

</details>

### D.2 Recovered Data
