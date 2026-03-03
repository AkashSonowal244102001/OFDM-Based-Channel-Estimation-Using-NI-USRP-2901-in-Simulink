# Single-Carrier Channel Impulse Response Estimation — NI USRP-2901 
Designed and implemented a real-time wireless channel sounding system using NI USRP-2901. A band-limited impulse signal was transmitted at 915 MHz and the received complex baseband IQ samples were processed to estimate the channel impulse response (CIR). The system models the wireless channel as a linear time-invariant (LTI) system, where the received signal represents the convolution of the transmitted impulse with the channel.

Channel gains, propagation delay, and multipath effects were extracted by analyzing the received waveform and performing cross-correlation in MATLAB. The project demonstrates practical SDR-based channel characterization, including RF front-end effects and bandwidth limitations (~200 kHz effective bandwidth).

📡 Single-Carrier Channel Impulse Response Estimation using NI USRP-2901
📖 Overview

This project implements a real-time wireless channel sounding system using the NI USRP-2901 software-defined radio platform. A discrete-time band-limited impulse signal is transmitted at 915 MHz, and the received baseband IQ samples are processed to estimate the channel impulse response (CIR).

The experiment validates the linear time-invariant (LTI) channel model:

𝑦
[
𝑛
]
=
𝑥
[
𝑛
]
∗
ℎ
[
𝑛
]
y[n]=x[n]∗h[n]

Since the transmitted signal is an impulse, the received signal directly represents the effective channel impulse response.

🎯 Objectives

Design and transmit a band-limited impulse using NI USRP-2901

Capture complex baseband IQ samples at the receiver

Estimate channel impulse response in time domain

Measure channel gains and propagation delay

Analyze multipath effects and bandwidth characteristics

🛠 System Configuration
Parameter	Value
Carrier Frequency	915 MHz
Sampling Rate	1 MS/s
Buffer Length	1024 samples
Impulse Length	5 samples
Effective Bandwidth	~200 kHz
Platform	NI USRP-2901
Development Tool	LabVIEW + MATLAB
⚙️ Transmitter Design

Generated a discrete-time impulse centered at a specified sample index.

Converted real-valued impulse to complex baseband IQ signal.

Transmitted continuously using NI-USRP Tx blocks in LabVIEW.

The impulse duration:

𝑇
𝑝
𝑢
𝑙
𝑠
𝑒
=
5
1
 
MS/s
=
5
 
𝜇
𝑠
T
pulse
	​

=
1MS/s
5
	​

=5μs

Resulting effective bandwidth:

𝐵
≈
1
𝑇
𝑝
𝑢
𝑙
𝑠
𝑒
=
200
 
𝑘
𝐻
𝑧
B≈
T
pulse
	​

1
	​

=200kHz
📡 Receiver Design

Captured complex IQ samples using NI-USRP Rx blocks.

Extracted real part (or magnitude) of received samples.

Plotted received waveform in time domain.

Stored received data for offline analysis.

The received signal represents:

ℎ
[
𝑛
]
=
Channel Impulse Response
h[n]=Channel Impulse Response
📊 Channel Analysis (MATLAB)

Loaded received samples.

Generated reference impulse.

Performed cross-correlation:

r = xcorr(rx, imp);
[~, idx] = max(abs(r));
delay_samples = idx - length(rx);
delay_time = delay_samples / Fs;
Extracted Metrics:

Channel gain (peak amplitude)

Propagation delay

Multipath components

Delay spread

📈 Expected Results

The received waveform shows:

Time delay (shift in impulse index)

Amplitude attenuation (path loss)

Pulse spreading (band-limiting)

Multipath reflections (multiple peaks)

🔬 Key Concepts Demonstrated

Single-carrier channel sounding

LTI channel modeling

Impulse response estimation

SDR-based wireless experimentation

Time-domain channel characterization

🚀 Applications

Wireless channel modeling

Delay spread estimation

Coherence bandwidth analysis

SDR-based physical layer experimentation

📌 Conclusion

This project demonstrates practical wireless channel characterization using an impulse-based single-carrier SDR system. The measured waveform directly represents the effective channel impulse response, enabling extraction of channel gains and delay characteristics in a real hardware environment.
