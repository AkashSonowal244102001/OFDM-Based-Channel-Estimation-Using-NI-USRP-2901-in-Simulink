# Single-Carrier Channel Impulse Response Estimation — NI USRP-2901 
Designed and implemented a real-time wireless channel sounding system using NI USRP-2901. A band-limited impulse signal was transmitted at 915 MHz and the received complex baseband IQ samples were processed to estimate the channel impulse response (CIR). The system models the wireless channel as a linear time-invariant (LTI) system, where the received signal represents the convolution of the transmitted impulse with the channel.

Channel gains, propagation delay, and multipath effects were extracted by analyzing the received waveform and performing cross-correlation in MATLAB. The project demonstrates practical SDR-based channel characterization, including RF front-end effects and bandwidth limitations (~200 kHz effective bandwidth).


This project demonstrates practical wireless channel characterization using an impulse-based single-carrier SDR system. The measured waveform directly represents the effective channel impulse response, enabling extraction of channel gains and delay characteristics in a real hardware environment.

# 📡 Single-Carrier Channel Impulse Response Estimation using NI USRP-2901

## 📖 Overview

This project implements real-time wireless channel sounding using the **NI USRP-2901** Software Defined Radio (SDR).  
A band-limited impulse signal is transmitted at 915 MHz, and the received complex baseband IQ samples are processed to estimate the **Channel Impulse Response (CIR)**.

The wireless channel is modeled as a Linear Time-Invariant (LTI) system:

y[n] = x[n] * h[n]

Since the transmitted signal is an impulse, the received signal directly represents the effective channel impulse response.

---

## 🎯 Objectives

- Transmit a discrete-time band-limited impulse using NI USRP-2901  
- Capture complex baseband IQ samples at the receiver  
- Estimate channel impulse response in time domain  
- Measure channel gains and propagation delay  
- Analyze multipath effects  

---

## 🛠 System Configuration

| Parameter | Value |
|------------|--------|
| Carrier Frequency | 915 MHz |
| Sampling Rate | 1 MS/s |
| Buffer Length | 1024 samples |
| Impulse Length | 5 samples |
| Effective Bandwidth | ~200 kHz |
| SDR Platform | NI USRP-2901 |
| Tools Used | LabVIEW + MATLAB |

---

## ⚙️ Transmitter Design

- Generated a discrete-time impulse centered at a specified index.
- Converted real-valued impulse to complex baseband IQ signal.
- Transmitted continuously using NI-USRP Tx blocks in LabVIEW.

Impulse duration:

T_pulse = 5 / 1e6 = 5 microseconds

Effective bandwidth:

B ≈ 1 / T_pulse ≈ 200 kHz

---

## 📡 Receiver Design

- Captured complex IQ samples using NI-USRP Rx blocks.
- Extracted real part (or magnitude) of received samples.
- Plotted received waveform in time domain.
- Stored received data for offline processing.

The received waveform represents:

h[n] = Channel Impulse Response

---

## 📊 MATLAB Post-Processing

After storing received samples from LabVIEW, cross-correlation is performed in MATLAB to estimate delay and channel gain.

```matlab
% Load received data
rx = load("received_signal.txt");

% Generate transmitted impulse
N = 1024;
imp = zeros(N,1);
imp(513) = 1;   % impulse index

% Cross-correlation
r = xcorr(rx, imp);

% Find delay
[~, idx] = max(abs(r));
delay_samples = idx - length(rx);

Fs = 1e6;
delay_time = delay_samples / Fs;

fprintf("Estimated Delay (samples): %d\n", delay_samples);
fprintf("Estimated Delay (seconds): %e\n", delay_time);

% Plot results
figure;
subplot(3,1,1); stem(imp); title("Transmitted Impulse");
subplot(3,1,2); plot(rx); title("Received Signal");
subplot(3,1,3); plot(abs(r)); title("Cross-correlation");
## 📊 Experimental Outputs

The following figures show the real-time over-the-air channel estimation using NI USRP-2901.

### 📌 Channel Impulse Response (CIR)
![CIR](Outputs/screenshot_630.png)

### 📌 Frequency Response
![Frequency Response](Outputs/screenshot_631.png)

### 📌 Received Signal Analysis
![Signal](Outputs/screenshot_632.png)
