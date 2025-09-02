
# QPSK Coarse Frequency Compensation in MATLAB

This repository demonstrates how to **analyze, apply, and verify coarse frequency compensation** on QPSK-modulated signals. The workflow extracts **I and Q samples** from Verilog simulations (after SRRC filtering), adds a known **Carrier Frequency Offset (CFO)** in MATLAB, and then applies MATLAB’s built-in [`comm.CoarseFrequencyCompensator`](https://www.mathworks.com/help/comm/ref/comm.coarsefrequencycompensator-system-object.html) using both **FFT-based** and **Correlation-based** algorithms.

The project bridges **theoretical derivation** with **practical MATLAB implementation**, making it easier for readers to connect concepts to working code.

---

## Project Title

**QPSK Coarse Frequency Compensation: Correlation-Based and FFT-Based Estimation in MATLAB**

---

## Motivation

When transmitting digitally modulated signals (like QPSK), hardware imperfections cause a **Carrier Frequency Offset (CFO)** between transmitter and receiver oscillators. This offset leads to constellation rotation, degraded demodulation, and higher error rates. To counter this, **coarse frequency compensation** is applied before fine synchronization stages.

In this project:

1. **I/Q data** was extracted from Verilog simulations (post-SRRC filtering).
2. A known CFO (e.g., **1 kHz**) was artificially added in MATLAB.
3. CFO estimation and correction were performed using MATLAB’s **Coarse Frequency Compensator**.
4. Both **FFT-based** and **Correlation-based** algorithms were demonstrated and compared.

---

## Theoretical Background

### Mathematical Derivation of Correlation-Based CFO Estimation

Reference [1] describes the **correlation-based maximum likelihood (ML)** estimator for PSK and PAM signals.

The received signal is:

```math
r_k = e^{j(2 \pi \Delta f k T_s + \theta)}, \quad 1 \leq k \leq N
