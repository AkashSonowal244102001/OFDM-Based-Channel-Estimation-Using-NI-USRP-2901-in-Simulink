# Single-Carrier Channel Impulse Response Estimation — NI USRP-2901 
Designed and implemented a real-time wireless channel sounding system using NI USRP-2901. A band-limited impulse signal was transmitted at 915 MHz and the received complex baseband IQ samples were processed to estimate the channel impulse response (CIR). The system models the wireless channel as a linear time-invariant (LTI) system, where the received signal represents the convolution of the transmitted impulse with the channel.

Channel gains, propagation delay, and multipath effects were extracted by analyzing the received waveform and performing cross-correlation in MATLAB. The project demonstrates practical SDR-based channel characterization, including RF front-end effects and bandwidth limitations (~200 kHz effective bandwidth).


This project demonstrates practical wireless channel characterization using an impulse-based single-carrier SDR system. The measured waveform directly represents the effective channel impulse response, enabling extraction of channel gains and delay characteristics in a real hardware environment.
