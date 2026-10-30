# QPSK-Communication-Simulator
Python-based QPSK digital communication simulator with AWGN channel and BER analysis
# QPSK Communication System Simulator Using Python

**A Python-based simulation of Quadrature Phase Shift Keying (QPSK) modulation and demodulation over an Additive White Gaussian Noise (AWGN) channel, with constellation visualization and Bit Error Rate (BER) performance analysis.**

## 1. Project Overview

Digital modulation is an essential component of modern communication systems, allowing digital information to be transmitted efficiently through physical communication channels.

This project implements a simplified end-to-end QPSK digital communication system using Python. It models the transmission of randomly generated binary data through an AWGN channel and evaluates the ability of the receiver to recover the original information under different noise conditions.

The simulator also compares experimentally obtained BER values with theoretical predictions, providing a practical demonstration of how channel noise influences communication reliability.

The project was developed as an independent learning exercise to strengthen my understanding of digital communications, signal processing, Python programming, and communication system performance evaluation.

## 2. Project Objectives

The main objectives of this project are to:

- Implement QPSK modulation and demodulation using Python.
- Simulate the transmission of binary data through an AWGN channel.
- Visualize transmitted and received symbols using constellation diagrams.
- Investigate the relationship between noise intensity and bit errors.
- Calculate the Bit Error Rate of the simulated communication system.
- Compare simulated BER performance with theoretical QPSK predictions.
- Develop a foundation for more advanced digital communication simulations.

## 3. Communication System Architecture

The simulator follows a simplified digital communication chain:

**Random Bit Generation → QPSK Modulation → AWGN Channel → QPSK Demodulation → BER Calculation**

### Transmitter

The transmitter generates random binary data and groups the bits into pairs. Each pair is mapped to one of four possible QPSK symbols.

### Communication Channel

The channel introduces Additive White Gaussian Noise, representing random disturbances that affect the transmitted symbols.

### Receiver

The receiver estimates the transmitted bits by examining the real and imaginary components of each received symbol.

### Performance Evaluation

The recovered bits are compared with the original transmitted bits to determine the number of errors and calculate BER.

## 4. Technical Background

### 4.1 Quadrature Phase Shift Keying (QPSK)

QPSK is a digital modulation technique that represents information using four distinct carrier phase states.

Because each symbol represents two binary bits, QPSK transmits two bits per symbol.

The implementation uses the following symbol mapping:

| Binary Input | In-Phase (I) | Quadrature (Q) | Phase |
|---|---|---|---|
| 00 | +1 | +1 | 45° |
| 01 | +1 | -1 | 315° |
| 10 | -1 | +1 | 135° |
| 11 | -1 | -1 | 225° |

Each QPSK symbol is represented as a complex number:

\[
s=\frac{I+jQ}{\sqrt{2}}
\]

Where:

- \(I\) is the in-phase component.
- \(Q\) is the quadrature component.
- \(j\) is the imaginary unit.
- \(\sqrt{2}\) is the normalization factor.

This normalization ensures that every transmitted symbol has unit energy.

### 4.2 Additive White Gaussian Noise (AWGN)

AWGN is commonly used to model random noise in communication systems.

The received signal is represented by:

\[
r=s+n
\]

Where:

- \(r\) is the received symbol.
- \(s\) is the transmitted QPSK symbol.
- \(n\) is complex Gaussian noise.

The simulator generates independent Gaussian noise components for the real and imaginary parts of the signal.

By increasing the noise level, the received constellation points become more widely distributed around their ideal positions, increasing the probability of incorrect bit detection.

### 4.3 QPSK Demodulation

The receiver estimates the transmitted bits using the signs of the received symbol's real and imaginary components.

For each component:

- A nonnegative value is decoded as binary 0.
- A negative value is decoded as binary 1.

The two detected bits are combined to reconstruct the original binary sequence.

This method assumes ideal carrier synchronization and knowledge of the QPSK symbol mapping.

### 4.4 Bit Error Rate (BER)

Bit Error Rate measures the proportion of incorrectly detected bits.

\[
BER=\frac{\text{Number of Bit Errors}}{\text{Total Transmitted Bits}}
\]

A lower BER indicates more reliable communication.

For coherent QPSK with Gray mapping over an AWGN channel, the theoretical BER is:

\[
P_b=\frac{1}{2}\operatorname{erfc}\left(\sqrt{\frac{E_b}{N_0}}\right)
\]

Where:

- \(E_b\) represents energy per bit.
- \(N_0\) represents the noise power spectral density.
- \(\operatorname{erfc}\) is the complementary error function.

The theoretical expression provides a reference for validating the simulated results.

## 5. Technologies and Libraries

| Technology | Application |
|---|---|
| Python | Main programming language |
| NumPy | Binary data generation, complex arithmetic, and numerical processing |
| Matplotlib | Constellation diagrams and BER visualization |
| SciPy | Theoretical BER calculations using the complementary error function |
| Google Colab | Development and execution environment |
| GitHub | Source code hosting and project documentation |

## 6. Implementation

The simulation is organized into five main functions.

### `generate_bits(num_bits)`

Generates a random sequence of binary digits representing the information to be transmitted.

### `qpsk_modulate(bits)`

Groups binary data into pairs and maps each pair to a normalized complex QPSK symbol.

### `add_noise(symbols, noise_std)`

Adds complex Gaussian noise to the transmitted symbols to simulate an AWGN channel.

### `qpsk_demodulate(received_symbols)`

Recovers the transmitted binary information using decision boundaries on the in-phase and quadrature components.

### `calculate_ber(original_bits, received_bits)`

Compares the transmitted and recovered bit sequences and calculates the proportion of bit errors.

The simulator also includes a separate BER-versus-\(E_b/N_0\) experiment to compare simulated performance with theoretical predictions.

## 7. Simulation Parameters

The project uses different simulation configurations for visualization and performance evaluation.

| Parameter | Value |
|---|---|
| Modulation scheme | QPSK |
| Bits per symbol | 2 |
| Channel model | AWGN |
| Symbol energy | 1 (normalized) |
| BER comparison bit count | 200,000 |
| \(E_b/N_0\) range | 0–10 dB |
| \(E_b/N_0\) step | 1 dB |
| Constellation experiment | 2,000 bits |
| Functional testing | 20,000 bits |
| Functional test noise levels | 0.0, 0.3, 0.7, 1.0 |

The simulation uses randomly generated data and noise, so the exact numerical results can vary between runs.

## 8. Results and Discussion

### 8.1 Transmitted QPSK Constellation

The transmitted constellation contains four distinct symbol positions corresponding to the four possible binary pairs.

These points are located in the four quadrants of the I-Q plane.

This confirms that the modulation process maps the binary input into the intended QPSK symbol positions.

**Insert transmitted constellation diagram here.**

### 8.2 Received QPSK Constellation

After introducing AWGN, the received symbols become scattered around their original constellation positions.

As noise intensity increases, the spread of the received symbols increases, making symbol detection less reliable.

**Insert received constellation diagram here.**

### 8.3 Bit Error Rate Under Different Noise Conditions

The simulator evaluates BER under different noise levels.

The observed behavior is consistent with the expected operation of a digital communication system:

- Without noise, the receiver recovers the transmitted bits without errors.
- Under low-noise conditions, the receiver generally recovers most bits correctly.
- As noise intensity increases, the number of incorrectly detected bits generally increases.
- Higher noise levels result in reduced communication reliability.

### 8.4 Simulated Versus Theoretical BER

The project compares simulated QPSK BER with the theoretical BER over an AWGN channel.

The results demonstrate that:

- BER decreases as \(E_b/N_0\) increases.
- Simulated BER generally follows the theoretical prediction.
- Higher signal quality improves the reliability of bit detection.

Small differences between simulated and theoretical BER values may occur because the simulation uses a finite number of randomly generated bits.

At sufficiently high \(E_b/N_0\), a finite simulation may observe zero errors even when the theoretical BER remains nonzero.

**Insert simulated versus theoretical BER graph here.**

## 9. How to Run the Project

### Option 1: Google Colab

1. Open the `QPSK_Communication_Simulator.ipynb` notebook from this repository.
2. Select **Open in Colab**, if available, or upload the notebook manually to Google Colab.
3. Run the notebook cells sequentially.
4. Examine the generated constellation diagrams and BER plots.
5. Modify the noise levels or simulation parameters to explore different channel conditions.

### Option 2: Local Python Environment

Install the required libraries:

```bash
pip install numpy matplotlib scipy notebook
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open `QPSK_Communication_Simulator.ipynb` and execute the cells in order.

## 10. Project Limitations

This simulator represents an idealized QPSK communication system and does not model every impairment present in real wireless environments.

Current limitations include:

- The channel model considers AWGN but does not include multipath fading.
- The receiver assumes ideal timing and carrier synchronization.
- Carrier frequency offsets and phase estimation errors are not modeled.
- The simulation uses baseband complex symbols rather than a complete radio-frequency transmission chain.
- The receiver uses simple sign-based hard decisions.

These assumptions make the simulator suitable for studying fundamental digital communication principles.

## 11. Future Improvements

Potential extensions include:

- Implementing Rayleigh and Rician fading channels.
- Comparing QPSK performance with BPSK and 16-QAM.
- Adding carrier phase and frequency offset impairments.
- Implementing channel estimation and equalization.
- Investigating forward error correction techniques.
- Developing interactive controls for noise and SNR parameters.
- Expanding the simulator to include OFDM-based communication systems.

## 12. Key Learning Outcomes

Developing this project provided practical exposure to several concepts in digital communications.

These include:

- Understanding how binary data is mapped to complex modulation symbols.
- Working with in-phase and quadrature signal components.
- Modelling random channel noise using Gaussian distributions.
- Implementing a basic digital receiver.
- Evaluating communication reliability through BER.
- Validating simulation results against theoretical models.
- Using Python to develop and visualize engineering simulations.

The project also reinforced the importance of connecting mathematical concepts with computational experimentation.

## 13. Conclusion

This QPSK Communication System Simulator demonstrates the fundamental operation of a digital modulation system under AWGN channel conditions.

By implementing modulation, channel noise, demodulation, and BER analysis, the project provides a practical introduction to communication system modelling and performance evaluation.

It serves as a foundation for further exploration of wireless communication technologies, digital signal processing, and more advanced communication system simulations.

---

**Author:** Kehinde Ajayi

**Field:** Electrical and Electronics Engineering

**Areas of Interest:** Wireless Communications | Signal Processing | Telecommunications | Communication Systems
