# 6G ISAC New Paradigm: Design and Real-Test of Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas[with MATLAB+python codes]

6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated Sensing and Communications System Based on Intelligent Waveguide Antennas
Abstract: Facing the ubiquitous Internet of Things (IoT) in 6G and high-density indoor IoT scenarios, integrated sensing and communication (ISAC) has become a native key technology. Existing solutions often design perception and communication independently, resulting in low integration of hardware prototypes. This paper is the first to deeply integrate bidirectional feeding intelligent half-width microstrip waveguide leaky antennas (HWM-LWA) with the 5 GHz Wi-Fi protocol. By utilizing the inherent frequency dispersion scanning characteristics of the leaky antennas, it achieves enhanced perception-aided communication in complex multipath indoor environments. The developed prototype does not require active phased array but can precisely predict the beamforming through passive frequency sweeping beams, effectively suppressing interference from cluttered echoes. Measurements show that compared to commercial directional monopole antennas and switchable beam antennas, the system's effective data rate significantly improves, with about 30% improvement in communication quality at distances greater than 5 meters. It also supports high-precision indoor positioning, providing a practical engineering solution for cost-effective, lightweight, and protocol-compatible 6G indoor ISAC.
Introduction: The sixth generation mobile communication (6G) is driving the convergence of cellular, Wi-Fi, and IoT. Indoor IoT, as a core carrier for Industry 4.0, smart factories, and smart logistics, demands strict requirements for wireless link reliability, speed, and positioning accuracy. The indoor environment is filled with metal equipment and structural obstructions, leading to severe multipath effects. Traditional directional antennas have broad coverage but low gain and poor angle resolution; switchable beam antennas and electro-controlled reconfigurable antennas require multi-ports, multi-elements, and phasers, which are costly and bulky; reconfigurable intelligent metasurfaces (RIS) and fluid antennas (FA) are still primarily theoretical, making practical deployment difficult.
Integrated Sensing and Communications (ISAC) attempts to achieve communication and sensing simultaneously using the same hardware, spectrum, and signals. It is one of the optimal approaches to break through indoor coverage, positioning, and multipath challenges. The leaky wave antenna (LWA) has natural frequency scanning beamforming, low cost, passive nature, compact structure, etc., and has demonstrated its potential in RFID, BLE, Wi-Fi positioning. However, an ISAC closed-loop system based on 5 GHz Wi-Fi that simultaneously enhances positioning and communication and addresses real indoor multipath remains unexplored.
This paper first realizes a fully integrated prototype of frequency-scanning LWA + commercial Wi-Fi NIC, achieving continuous 120° field of view beam scanning in the 5 GHz ISM band. The positioning results are dynamically guided to select the optimal channel and port, forming a complete closed loop from "perception→positioning→adaptive beam→communication enhancement". This completes the full process validation in real indoor IoT scenarios.
I. Core principle of the system: Frequency scanning mechanism of the leaky wave antenna This paper adopts a bidirectional feeding half-width microstrip leaky wave antenna (HWM-LWA), based on FR4 dielectric board (εr=4.7, H=0.762 mm), with radiation arm length L=35 cm, achieving high gain narrow beam and frequency scanning coverage in the 5.2–5.8 GHz Wi-Fi channel.
1. Frequency scanning angle formula (Core principle 1) The radiation angle of the leaky wave antenna is determined by the longitudinal phase constant βy(f) of the transmission line and the free space wave number k0:  
θR(f): Main beam radiation angle corresponding to the frequency f  
k0=2πf/c: Free space wave number  
βy(f): Transmission line leaky mode phase constant, determined by the antenna width W and dielectric εr  
Physical meaning: By changing the frequency f, the beam direction can be passively changed without the need for phase shifters or switch matrix.  
2. Half power beam width formula (Core principle 2) The directionality and angular resolution of the antenna are determined by the aperture length L and scanning angle θR:  
Δθ(f): Half power beam width (HPBW)
L: The length of the antenna radiation aperture
λ0: Free space wavelength corresponding to the working frequency
Physical meaning: The longer the antenna, the narrower the beam and the higher the gain; when the scanning angle deviates from end-fire, the beam will widen.
3. Frequency sweeping characteristic design: By selecting an FR4 substrate with εr = 4.7, a suitable dispersion slope is obtained to cover the 5 GHz Wi-Fi channel (#44–#161) with a ±60° (120°) field of view. The P1/P2 dual-feedback configuration forms symmetrical beams, further expanding coverage and enhancing angle estimation robustness.
II. ISAC System Architecture and Implementation
Antenna: Bidirectional feeding HWM-LWA, P1/P2 correspond to the beams of positive and negative angle areas respectively.
Comparative benchmark: omnidirectional monopole antenna, mechanically tilted double-layer panel antenna (switched beam SBA)
Calibration: Darkroom simulated radiation directional pattern + Digital RSSI directional pattern dual calibration
2. Workflow 1
Channel hopping: AP switches between #44 (5.22 GHz) and #161 (5.805 GHz), triggering frequency sweep beam
2  
RSSI acquisition: Collect RSSI for each channel through dual ports, forming a 12-dimensional feature vector (6 channels × 2 ports).
3  
MUSIC DoA estimating: Angle of Arrival Estimation with Calibrated Directional Vectors
4  
Adaptive Channel Selection: Selecting the optimal beam channel based on target angle
5  
Communication Enhancement: Establish a stable link with the highest MCS and peak throughput
6  
Closed-loop monitoring: Real-time monitoring of throughput, trigger re-sensing process if it falls below 250 Mbps.
III. Positioning Algorithm: Improved MUSIC Based on RSSI
1. Vector Direction Construction
SV(φ): Calibrated vector direction corresponding to angle φ
Wn: Amplitude weighted coefficient for darkroom calibration (compensating for peak gain differences across different channels)
RSSIn(φ): Received signal strength at the nth channel / port under angle φ
2. MUSIC Spatial Spectrum Formula (Core Principle 3)
APS(φ): Pseudo spectrum of angle, with peaks corresponding to true arrival directions
H: Conjugate transpose
EN: Noise subspace characteristic vector matrix
Principle: By leveraging the orthogonality between the signal subspace and noise subspace, it is possible to extract the dominant line-of-sight (LoS) paths in multipath environments, achieving **angle error < 5°** high precision positioning.
IV. Real Test Performance: Communications Enhancement and Positioning Accuracy
1. Communications Performance (Key Findings)
MCS: LWA maintains MCS=9 (256-QAM, 80 MHz) at all test points
Throughput: Stabilized at all angles > 300 Mbps, 90th percentile reaches 335 Mbps
Comparison with a single dipole: Throughput increases by approximately **30%** at long distances / large angles
Comparison with an inclined panel: The performance near ±20° is close, but quickly drops off beyond this range, while LWA maintains high performance throughout the full 120° range
2. Power Doppler Spectrum (PDP) Verification: Significant enhancement of spatial filtering by the leaky wave antenna, suppressing multipath:
Point B (+20°): LoS component of LWA is 8.3 dB higher than that of a single dipole
Point G (−50°): LoS component of LWA is 12.95 dB higher than that of a single dipole, resulting in cleaner channels and smaller time delay spread, leading to more stable communications.
3. Energy Efficiency Improvement LWA Power Consumption (1187 mWh) is almost consistent with that of a single-pole (1184 mWh), but the system's energy efficiency has improved by 10.5%. The time required to transmit 1 Gbit of data has been reduced by approximately **20%**, making it more suitable for battery-powered IoT nodes.
4. The dynamic moving test terminal moves from point F (-40°) to point D (+50°), and the system automatically detects a decrease in throughput → reassesses DoA → switches to the optimal channel, allowing for rapid link recovery, verifying the effectiveness of ISAC closed-loop.
V. Conclusion This paper firstly realizes the integrated system of ISAC (Integrated Sensing and Awareness Control) for 5 GHz Wi-Fi + intelligent frequency sweeping leakage antenna, breaking through the bottleneck of traditional antennas "omnidirectional without gain, directional flexibility is not flexible, complex cost is high".
1  
Passive Frequency Swept Beam: 120° Continuous Beam Direction with Switching Wi-Fi Channels, No Need for Phased Array
2  
Positioning auxiliary communication: MUSIC DoA error &lt; 5°, dynamically optimize communication link based on perception results.
3  
Real indoor verification: Compared with single-pole and switch beam antennas, the effective throughput is increased by about 30%, and the energy efficiency is improved by 10.5%.
4  
Protocol Compatibility: Fully based on the standard IEEE 802.11ac, no need to modify the protocol, can be directly commercial deployment.
This solution offers a scalable ISAC implementation for 6G indoor IoT, smart factories, and high-density access scenarios with extremely low hardware costs, lightweight structures, and commercial Wi-Fi compatibility. It represents an important technological pathway for the next generation of integrated sensory communication terminals and APs.

## Images

![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](01.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](02.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](03.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](04.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](05.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](06.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](07.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](08.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](09.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](10.jpg)
![6G ISAC New Paradigm: Design and Measurement of a Wi-Fi Integrated System Based on Intelligent Leakage Wave Radar Antennas [with MATLAB+Python Code]](11.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
