# Extreme background-rejection techniques for the ELROI optical satellite license plate

[PERSON]

[EMAIL_ADDRESS]; ISR-1, Space Science & Applications

[PERSON]

[EMAIL_ADDRESS]; ISR-2, Space & Remote Sensing Los Alamos National Laboratory, Los Alamos, NM

November 6, 2021

###### Abstract

The Extremely Low-Resource Optical Identifier (ELROI) is a concept for an autonomous, low-power optical \"license plate\" that can be attached to anything that goes into space. ELROI uses short, omnidirectional flashes of laser light to encode a unique ID number which can be read by a small ground telescope using a photon-counting sensor and innovative extreme background-rejection techniques. ELROI is smaller and lighter than a typical radio beacon, low-power enough to run on its own small solar cell, and can safely operate for the entire orbital lifetime of a satellite or debris object. The concept has been validated in ground tests, and orbital prototypes are scheduled for launch in 2018 and beyond. In this paper we focus on the details of the encoding scheme and data analysis that allow a milliwatt optical signal to be read from orbit. We describe the techniques of extreme background-rejection needed to achieve this, including spectral and temporal filtering, and discuss the requirements for an error-correcting code to encode the ID number. Worked examples with both simulated and experimental (ground test) data will illustrate the methods used. We present these techniques to describe a new photon-counting optical communication concept, and to encourage others to consider observing upcoming test flights.

Footnote †: preprint: LA-UR-18-28957
Introduction

The Extremely Low-Resource Optical Identifier (ELROI) is a low-power optical \"license plate\" that can be attached to anything that goes into space[1; 2; 3]. ELROI is designed to help address the problem of space object identification (SOI) in the crowded space around the Earth, where over 19,000 objects--from active satellites to debris fragments--are currently tracked and monitored[4]. Tracking these objects is a multi-billion USD effort, and requires continuous knowledge of each object's position and trajectory. Sudden orbit changes or interruption in tracking can lead to confusion about a tracked object's identity, and multiple costly observations may be needed to re-identify it as a known satellite. SOI is easier if a satellite carries a continuous identifying beacon that can be read by anyone on the ground, but no suitable standard technology is currently used for this purpose[5; 6]. ELROI is a new optical SOI technology which is currently at the prototype stage (Figure 1). The concept has been validated in ground tests[1], and orbital prototypes are scheduled for launch in late 2018 and beyond.

ELROI is an autonomous solar-powered optical beacon that uses short, diffused flashes of laser light at milliwatt average power to encode a unique ID number, which can be read by a small ground telescope during local night using a photon-counting sensor and innovative extreme background-rejection techniques. ELROI is smaller and lighter than a typical radio

Figure 1: a. A current-generation ELROI prototype, showing laser diodes and solar cell. The design shown is approximately 10 cm x 10 cm x 3 cm and 300 g. A mature design, in progress, can be miniaturized to the size of a postage stamp with 0.5 cm thickness. Details may be found in[7]. b. Simplified block diagram of the ELROI beacon electronics.

beacon, suitable for small satellites including CubeSats, and can safely operate for the entire orbital lifetime of a satellite without concern for radio-frequency interference (RFI). Autonomous solar power also allows ELROI to continue emitting after the end of a satellite's operational lifetime, and makes ELROI suitable for non-powered debris objects such as rocket bodies. Space object identification is generally more challenging than tracking with current technology, and ELROI is designed to address the problem of objects that are tracked but not identified; thus, reading the ELROI ID number requires tracking information for the host satellite (such as the publicly available and regularly updated data in the SpaceTrack catalog [4]).

This paper is not a comprehensive overview of the ELROI system, and additional details about the beacon hardware, ground station designs, link budgets, and the concept of operations may be found in [1]. Here, we focus on the details of the encoding scheme and data analysis that allow a milliwatt optical signal to be read from orbit. We will describe the techniques of extreme background-rejection needed to achieve this, including spectral filtering and temporal filtering using a period- and phase-recovery algorithm, and discuss the requirements for an error-correcting code to encode the ID number. Worked examples with both simulated and experimental (long-range ground test) data will illustrate the methods used.

We encourage others to consider observing our test flights. Details about current flight prototypes, as well as practical considerations and necessary equipment for those interested in observing ELROI test flights from their own ground stations, may be found in [7].

### Characteristics of the ELROI signal

ELROI uses short, bright flashes of laser light at a fixed period to encode a unique binary ID number with an on-off keying (OOK) scheme (Figure 2). The approach builds on photon-counting laser optical communications techniques [8; 9; 10; 11], but in a novel operating regime at much lower power, very low bandwidth, and without strict pointing requirements due to the very broad optical beam. The ID number repeats many times per second. The laser light is nearly monochromatic, with a spectral range of about 1 nm. The peak power of the laser is high (\(P_{\text{peak}}\approx\) 1 watt), but it is pulsed at a low duty cycle so that the average power is reduced to a few milliwatts.

This low average power requirement is essential for autonomous solar-powered operation in space, and allows the beacon to be \"low-resource\" in size and mass. Light from the beacon is diffused over a wide angle--approximately 145 degrees for current prototypes--to increase visibility from the ground without active pointing. At orbital distances, this combination of low optical power and large solid angle results in an extremely weak signal at a ground station. Link budget calculations for a typical design indicate that a ground station will detect 3-4 signal photons/s from a 2-mW ELROI beacon in low-Earth orbit (LEO) at 1000 km range [1]. This is far below the 90 photons/s of background light (at the beacon wavelength) expected from a small sunlit CubeSat host. However, the spectral and timing characteristics of the signal enable extreme background-rejection techniques, introduced in Section I.2, which allow the beacon ID to be read reliably after a few minutes of accumulating data--i.e., in a single pass over a ground station for a typical LEO orbit.

Reading an ELROI ID requires a photon-counting sensor, such as a single-photon avalanche diode (SPAD) or photomultiplier. The sensor must, at minimum, register discrete signals for each detected photon with timing resolution better than the pulse width \(\tau\). (Due

Figure 2: An example of the signal produced by an ELROI beacon. The onboard laser diode emits short pulses of light (pulse width = \(\tau\)) separated by a fixed period (clock period = \(T\)). Each clock period encodes one bit of the beacon ID number (shown at top): if the bit is a 1, the beacon emits a pulse, and if the bit is a 0, the beacon does not emit a pulse. The laser power during a pulse is \(P_{\text{peak}}\); otherwise it is zero. The pulse width in this example is exaggerated compared to the clock period. For a real beacon, a typical value of \(\tau/T\) is 1/1000. The ID number repeats many times per second.

to read noise, conventional CCD or CMOS detectors are not suitable.) The sensor must receive light from a telescope, which may be relatively small, but must be able to accurately and precisely track objects across the sky. An imaging or position-sensitive detector is useful to reduce the pointing and tracking tolerance requirements on the ground station telescope, and our current ground station uses a LANL-developed photon-counting camera which combines a photocathode, microchannel plate (MCP), and multi-anode readout [12]. However, an imaging sensor is not required to read the ELROI ID. Further discussion of the design trade-offs between sensor, ground station, and beacon may be found in [1] and [7].

The data recorded from the ground station is a list of photon detection times. Some of these times correspond to signal photons, and many more are background photons, either from the environment or from noise in the sensor. The goal of data analysis is to isolate enough of the signal photons to determine the value of each ID bit with sufficient confidence to recover the ID number. Each step in this analysis can be done efficiently, so that a satellite can be identified in real time as it is tracked over the ground station.

### Background rejection

The critical characteristics of the ELROI signal that enable extreme background rejection are the narrow spectral range of the laser light, the precise timing of the signal clock period, and the high peak power and narrow width of the signal pulses relative to the clock period.

#### ii.2.1 Spectral filtering

The narrow spectral range of the beacon light allows most environmental background photons to be blocked with a narrow-band optical filter. Current prototypes use 638-nm laser diodes with a spectral width of less than 1 nm. (This wavelength was chosen to match the sensitivity of the LANL photon-counting camera; other wavelengths, particularly near-IR, may be more appropriate for future designs.) For an orbital beacon, the majority of background photons are sunlight reflected from the host satellite, with some sky background depending on environmental conditions (particularly moon phase) and tracking accuracy. A 10-nm filter centered at 638 nm blocks about 99% of reflected sunlight. The filter bandwidth is a compromise between background transmission and tolerance for thermal shifts in the central wavelength of the beacon. Spectral filtering is an important part of the ELROI system, but the rest of this paper will focus on background rejection in data analysis after spectrally filtered photons have been detected. All background photon rates will be assumed to be measured after appropriate spectral filtering.

#### ii.1.2 Phase cut

Because the ELROI signal consists of short, bright pulses that are clocked at a fixed period, all the signal photons are detected within short, precisely spaced time windows (recall Figure 2). The phase of signal photons in the range of [0,1) clock cycles is restricted to a narrow peak with width \(\tau/T\) (Figure 3). In contrast, background photons are detected

Figure 3: A simple example of the phase cut used to reject background photons. The top panel shows simulated photon detection times from a sensor observing the beacon that was introduced in Figure 2, with signal photons shown in red (filled) and background photons in gray (unfilled). Time increases from left to right and the observation covers 10 clock periods. The average background detection rate is about 10 times the average signal detection rate. Below, the same 10 clock periods are expanded and stacked to demonstrate that all signal photons arrive within a phase window with width \(\tau/T\). Photons outside this window can be rejected as background. As in Figure 2, the ratio \(\tau/T\) is shown much larger here than for a real signal. The signal photon rate is also exaggerated compared to a real beacon, and in a real application, the beacon must be observed for several minutes spanning many repetitions of the ID number.

at random times. Thus, if the clock period is known, a phase cut can be used to reject any photons outside this narrow phase peak. This is analogous to \"lock-in\" detection methods. The phase cut reduces background counts by a factor of \(\tau/T\), which is between 1/1000 and 2/500 for typical signals. This is the advantage of using short pulses relative to the clock period.

Ignoring out-of-phase data is common in optical communications, but the ELROI data analysis requires much more accurate knowledge of the clock period than typical high-power applications where transitions between 0 and 1 bits can be used to continuously synchronize the receiver clock to the emitter. In the simple example of Section II, we will assume that the clock period is known to arbitrary precision. In practice, even if the nominal clock period is known, temperature variations and the tolerance of the beacon on-board clock will lead to small deviations from the nominal value, and even drift over time. To achieve full sensitivity, the true clock period must be recovered from the data to an accuracy of a few parts per million. This is possible for ELROI because an entire 2-3 minute observation can be used to determine the clock period in post-processing, with latency still short compared to the observation length. Efficient methods for clock detection and recovery are discussed in the more realistic example of Section III.

### Decoding the ID number

A typical ELROI beacon will repeat its ID number 5-10 times per second, so an observation spanning several minutes contains many repetitions of the ID number. The data from each repetition must be combined to get the best estimate of the ID bit values. Thus, after out-of-phase background photons are removed with a phase cut, the remaining photon detection times are \"folded\" by the known ID length: the time data is divided into windows the length of the ID (the number of bits \(m\times T\)), these windows are summed, and the result is binned by the clock period to get the total number of photons corresponding to each expected ID bit.

These photon detection totals must then be used to assign a 1 or 0 value to each bit to recover the ID. The bit value assignment must account for the fact that some background photons will remain even after the phase cut, so 0 bits may contain photons. The number of photons detected for 1 bits will also fluctuate significantly with Poisson statistics (shot noise),due to the very low signal count rate from orbit and the limited time available to accumulate photons during one pass over a ground station. Background is expected to be independent and identically distributed (i.i.d.) over short times. In most cases, the photon numbers of 1 and 0 bits will form clearly separate distributions, and a simple threshold procedure can be used to separate them (hard decision decoding). The hard decision method can also be extended to cases with poorer signal-to-noise ratios. The examples in this paper will use a hard decision method, but other possibilities are briefly discussed in Section V.

#### Error-checking and correction codes

Particularly for observations with very few signal photons, it is expected that some bits will be assigned the wrong value, and the recovered ID number may not exactly match the true ID. To provide tolerance for incorrect bits, an error-correcting code is used to generate the ID numbers. Error-checking and correction (ECC) codes are a proven strategy in modern digital communications, and can provide codeword error rates (the probability of incorrectly identifying an ID) orders of magnitude lower than the bit error rate (the probability of incorrectly identifying a bit). The error-correcting code used for ELROI restricts the ID numbers to a minimum Hamming distance from any other ID, so that up to some threshold number of bit errors, a single true ID will be significantly closer to the recovered ID than any other possible ID[13]. Thus, the final step in reading an ELROI ID is to search the database of all active ID numbers for the ID with the fewest number of errors relative to the recovered ID.

For the examples in this paper, we use constant-weight 64-of-128-bit codes allowing cyclic permutation: the ID numbers are 128 bits long, 64 bits are 1 and 64 bits are 0, and two IDs that differ only by moving some bits from the start of the ID to the end of the ID are considered to be the same ID. The possible IDs are chosen such that any pair of IDs differs by at least 24 bits, which allows for millions of unique IDs while guaranteeing that up to 12 incorrect bits can be corrected. Because the start bit of the recovered ID is not known, it must be compared to each ID in the database with each of \(m\) shifts, where \(m\) is the number of bits in the code; however, the search can still be done quickly compared to the length of the observation. (While this example ECC scheme does not indicate the start bit of the ID number, other schemes can do so.) This scheme is sufficient to demonstrate the value of error-correcting codes for ELROI, and will be used on the current generation of orbital prototypes. There are several options for refining the final ECC code strategy for ELROI, but these are beyond the scope of this paper and are summarized only briefly in Section V.

## II Example: Decoding Simulated Data

This example will analyze a simulated ELROI dataset with signal and background photon rates comparable to a beacon in LEO. The simulation uses typical beacon signal characteristics (Table 1), and models a detector similar to the LANL photon-counting camera.

A three-minute simulated dataset was generated with a Monte Carlo method. The data is a list of simulated photon detection timestamps, and contains \(N_{\mathrm{tot}}=19,038\) timestamps total, corresponding to \(N_{\mathrm{s}}=931\) signal photons from a beacon (spread over 180,000 pulses) and \(N_{\mathrm{bg}}=18,107\) random background photons. The background photon rate is assumed to be detected after spectral filtering. Photon detection timestamps were generated to a resolution of 1 ns.

### Phase cut

To apply the phase cut, we first compute the fractional phase \(\phi_{i}\) of each photon in the dataset, relative to the clock period:

\[\phi_{i}=\mathrm{frac}(t_{i}/T) \tag{1}\]

\begin{table}
\begin{tabular}{l l l} \hline Parameter & & Value \\ \hline ID number (hexadecimal) & & 0x8345f3 ca6 ca6f0e338f5d598e525a912 \\ ID length & \(m\) & 128 bits \\ Pulse width & \(\tau\) & 1 \(\mu\)s \\ Clock period & \(T\) & 1 ms \\ Average signal photon rate & \(R_{s}\) & 5 photons/s (detected) \\ Average background photon rate & \(R_{b}\) & 100 photon/s (detected) \\ Clock phase & \(\phi_{0}\) & 0.50 cycles \\ ID start bit & \(s\) & 10 \\ Dataset length & \(t_{\mathrm{obs}}\) & 180 s \\ \hline \end{tabular}
\end{table}
Table 1: Parameters for the simulated dataset analyzed in Section II. The 128-bit binary ID number is represented in hexadecimal for compactness.

where \(t_{i}\) is the time at which the photon was detected, \(T\) is the clock period, and

\[\text{frac}(x)=x-\lfloor x\rfloor \tag{2}\]

is the fractional part function. \(\phi_{i}\) is in the range [0,1) and has units of cycles. (In this example we have assumed the clock period \(T\) is known exactly. The next example in Section III will demonstrate the more realistic process of determining the clock period from the data.)

A histogram of \(\phi_{i}\) is shown in Figure 4. The peak at \(\phi_{i}=0.5\) cycles is due to the in-phase signal photons, while the background photons have random phases. (Note that in this example, the phase of the signal photons was fixed as a simulation parameter, but in general it could take any value between 0 and 1.) We will apply a phase cut of width 3 \(\tau/T\) centered on this peak, and discard all photons outside the range of 0.499 cycles to 0.502 cycles. It is clear from the histogram that a narrower phase cut would be possible without losing any signal photons, but it is not necessary for this example. For autom

Figure 4: (Simulated data) Histogram of the fractional phase \(\phi_{i}\) of photon detection times in the range [0,1) clock cycles. Because the clock period is known exactly, the histogram shows a clear peak with width \(\tau/T=0.001\). The inset shows a closer view of the peak (each phase bin is 0.25 \(\times\)\(\tau/T\)). The dashed lines in the inset show the phase cut window that will be applied to this data, with a width 3 \(\tau/T\).



corresponding to 0 bits and 1 bits. A threshold of \(N_{\mathrm{thresh}}=5\) appears reasonable based on the histogram of \(N_{j^{\prime}}\), and also produces equal numbers of 0 bits and 1 bits, which matches our expectation for a 64-of-128-bit code (as discussed in the next example of Section III, this property of the ID numbers can be used to choose an appropriate value of \(N_{\mathrm{thresh}}\) when the distinction between 1 and 0 bits is less obvious).

The final step is to compare the recovered ID number to the registry of known IDs (with each shift \(0\leq s<m\)) to find the best match. In this example we will simply find the matching ID with the smallest Hamming distance (number of bit errors) from the recovered ID. Because the ID numbers are generated with an error-correcting code, if all other IDs have a larger Hamming distance than the best match, this indicates with high confidence that our identification is correct. For this example, we will compare the recovered code to a test registry containing 20 ID numbers generated under the restrictions described in Section I.3. (An operational registry would contain at least as many ID numbers as there are satellites with ELROI beacons, and millions of unique IDs are possible.) The result of this comparison is shown in Figure 6. In this simulation, we were able to get a perfect match (zero bit errors) with a registry ID. The recovered ID matches registry ID number 16 with a shift \(s=10\).

Figure 5: (Simulated data) a. Histogram showing the frequency of photon numbers per bit (for 981 photons in 128 bits) after the phase cut. The histogram clearly shows two distributions with different means, corresponding to 0 bits and 1 bits. b. Histogram showing the frequency of photon numbers per bit (for 19,038 photons in 128 bits) before the phase cut is applied to remove background photons. Note that without the phase cut, the distributions of 0 bits and 1 bits are indistinguishable.

## III Example: Decoding Experimental Data

The ELROI concept has been demonstrated in a ground test over approximately 15 km. This test served both to validate link budget calculations, as discussed in more detail in [1], and to verify data analysis techniques for conditions similar to a LEO system. According to our link budget calculations, signal rates of 3 to 20 photons/s will be typical at our ground station for prototype ELROI beacons on LEO satellites, depending on the beacon power and range [1; 7]. To approximate the expected LEO link budgets, the ground test used laser diodes with lower peak power than the orbital beacons, a neutral density filter on one of the beacons to further reduce the outgoing light, and a smaller lens at a variety of apertures to replace the telescope that would be used for an orbital beacon. This allowed us to test reception at signal rates that were both higher and lower than expected for the nominal orbital case.

In this example, which uses a three-minute portion of ground test data with approximately 4.8 photons/second signal rate, we will illustrate more realistic elements of data processing,

Figure 6: (Simulated data) Histogram of the number of bit errors in each of 20 registry IDs with each shift \(0\leq s<m\) (2560 shifted IDs total), compared to the recovered ID. The single ID with zero errors is the correct ID.

including determining the true clock period from the data, and using the known properties of the ID number to choose an appropriate bit value threshold for decoding.

### ELROI ground test conditions

The ground test used a receiver stationed 15 km away from two beacon units. Each beacon consisted of a red laser diode (638 nm), optical diffuser, and driver electronics. The lasers were driven in a 64-of-128 pattern ID with a pulse duration \(\tau=2\,\mathrm{\SIUnitSymbolMicro s}\) and a nominal clock period \(T_{\mathrm{nom}}=500\,\mathrm{\SIUnitSymbolMicro s}\) (signal characteristics are summarized in Table 2). The two beacon units encoded different IDs. The time-averaged effective isotropic radiated power (EIRP) in the direction of the receiver was measured to be 0.3 mW, corresponding to a peak EIRP of 150 mW after adjusting for the 1:500 duty fraction. Unit 2 was attenuated by a 13%-transmission neutral density filter to 0.04 mW EIRP, while Unit 1 was left unfiltered. This example analyzes data from Unit 2.

Figure 7: Single-photon image of an ELROI test beacon at a horizontal range of approximately 15 km. The image represents a 3-minute accumulation with the LANL photon-counting camera, and has been spatially binned, as well as cropped to show only the area of interest. The circular aperture shows the region of the camera data (within a radius of 100 image units around the apparent location of the beacon) that was used in the analysis of Section III.

The receiver consisted of a LANL-developed photon-counting camera [12; 14] with an f = 400 mm lens and adjustable aperture (up to f/2.8 = 143 mm diameter). The camera has a quantum efficiency of about 3.9% at 638 nm, sub-nanosecond timing resolution, a dark count rate of a few thousand counts/second over the entire sensor, and it can detect approximately 500,000 photons/s. The receiver was equipped with a 10-nm bandpass filter centered on the transmitter laser wavelength to reduce background. The observations were made at night. Along with the adjustable sensor aperture, the beacon power and the range to the receiver were chosen to simulate predicted photon rates from typical ELROI beacons with a range of optical powers and orbital distances. Detailed link budget calculations may be found in Ref. [1]. Radius cuts were applied to the camera data to isolate the photon detections from each beacon (Figure 7) and produce a list of photon detection times to analyze. Like the simulated data in Section II, the radius cut also contains background photons, both from the environment and from the dark count rate of the sensor.

### Recovering the true clock period

The nominal clock period of the ground test beacon is known (and programmed into the pulse generator that drives the laser), but in contrast with the the simulated data in Section II, we expect to observe some deviation from the nominal value. The fractional error tolerance \(e_{T}\) of the beacon onboard clock determines the expected uncertainty range of \(T\): \(T_{\mathrm{nom}}(1-e_{T})<T<T_{\mathrm{nom}}(1+e_{T})\). For inexpensive crystal oscillators commonly used in integrated circuits, \(e_{T}\) = 50-100 ppm is a typical value. Temperature changes, electromagnetic fields, radiation damage, and mechanical stress can also cause small deviations from the

\begin{table}
\begin{tabular}{l l l} \hline Parameter & & Value \\ \hline ID number (hexadecimal) & & 0x65b0278a7 cad7b5c766f056a470f01 cc \\ ID length & \(m\) & 128 bits \\ Pulse width & \(\tau\) & 2 \(\mu\)s \\ Nominal clock period & \(T_{\mathrm{nom}}\) & 500 \(\mu\)s \\ Sensor aperture & & f/2.8 = 143 mm \\ Measured signal photon rate & \(R_{s}\) & 4.8 photons/s (detected) \\ Measured background photon rate & \(R_{b}\) & 50.7 photons/s (detected) \\ Dataset length & \(t_{\mathrm{obs}}\) & 180 s \\ \hline \end{tabular}
\end{table}
Table 2: Parameters for the ground test dataset analyzed in Section III. We consider only one of the two test beacons, Unit 2. The 128-bit binary ID number is represented in hexadecimal for compactness.

nominal period. As illustrated in Figure 9, even a small deviation from the nominal period destroys the stable fractional phase relationship between signal photons that is critical for the background-rejection phase cut. Therefore, it is necessary to determine the true clock period from the photon detection data before calculating \(\phi_{i}\).

#### iv.1.1 The Fast Folding Algorithm

Given the nominal clock period and the expected value of \(e_{T}\), the true clock period can be recovered with computationally efficient techniques such as the Fast Folding Algorithm (FFA)[15]. Details on the FFA may be found in 15; what follows is a brief conceptual summary.

If a periodic signal is present in time series data, the fractional phase of the signal relative to the period (Equation 1) has a constant value over time. If the phase is measured relative to a period which is close to but not exactly the true period, the measured phase will change linearly with time (examples are shown in Figures 8a and 9a). The FFA determines the most likely slope of this linear relationship, and therefore the true period, using a sequence of shifting and adding steps on a two-dimensional histogram of the time series data binned by time and phase.

The FFA has advantages over the more familiar Fast Fourier Transform (FFT) for the ELROI clock period recovery task. The FFA concentrates the power of the non-sinusoidal ELROI signal, while the FFT disperses power at higher harmonics into other bins. The FFA can use the known value of \(T_{\mathrm{nom}}\) to search for periodic signals in a specified frequency range with a specified frequency spacing, while the FFT must be calculated over all frequencies from zero to the highest frequency of interest with a fixed frequency spacing. Finally, unlike the FFT, the FFA can also be extended to measure slow changes in frequency over the duration of an observation (e.g., due to temperature drift).

A Python implementation of the FFA was used to find the true clock period in this example[16]. The inputs to the FFA are the photon detection times \(t_{i}\) in bins of width \(b_{t}\), and the photon phases \(\phi_{i}\) relative to the nominal period \(T_{\mathrm{nom}}\) in bins of width \(b_{\phi}\) (Figure 8a). The optimal width of \(b_{\phi}\) is the approximate width of the phase peak \(\tau/T\). The width of \(b_{t}\) is an integer number of nominal periods determined by \(\Delta f\), the maximum frequency deviation to be included in the search (larger \(\Delta f\) requires more timebins). Using \(b_{\phi}=0.004\), \(\Delta f=0.01\) Hz, and \(b_{t}=0.352\) s, the FFA found a peak period of \(T_{\mathrm{true}}=499.9996115\)\(\mu\)s in our three-minute dataset, corresponding to a peak frequency of \(f_{\text{true}}=2000.001554\) Hz (Figure 8b). The deviation from the nominal period (\(T_{\text{nom}}=500\)\(\mu\)s) is less than 0.8 ppm, but the correction is still critical in order to apply an efficient phase cut. The FFA also determines the phase of the periodic signal in the data (relative to the true period), \(\phi_{\text{peak}}=0.16\) cycles.

### Phase cut

The true clock period, recovered using the Fast Folding Algorithm, can then be used to apply a phase cut to the photon time data. Because the FFA also determines the phase \(\phi_{\text{peak}}\) of the clock, the phase cut can now be applied given a desired tolerance around the peak phase. We use the same tolerance as in the example of Section II, and reject all photons outside a \(3\)\(\tau/T\) phase window (Figure 9b).

The phase cut window is not perfectly centered on the phase peak, nor is the peak as narrow and tidy as in the simulated example of Section II. The phase peak is wider than \(\tau/T\), indicating that we still do not have exactly the correct clock period. The true location of the phase peak also appears slightly offset from the phase found by the FFA, which is due to the size of the phase bins \(b_{\phi}\) and the uncertainty in the best period. If necessary, some additional

Figure 8: (Ground test data) a. Two-dimensional histogram input to the Fast Folding Algorithm (FFA). Photon detections are binned by time \(t_{i}\) and fractional phase \(\phi_{i}\) relative to the nominal period. The time bins span the full 180-second dataset, and the phase bins extend from 0 to 1. A faint line is visible, providing a preliminary indication that there is a periodic signal. b. Result of the FFA applied to (a). The point with the highest value corresponds to the peak frequency and phase of the input data.

sensitivity could be recovered by making small adjustments to \(T\) and \(\phi_{\rm peak}\) to maximize the height of the phase peak and allow the narrowest possible phase cut. However, this step is not needed to get good results in the current example.

After the phase cut, we are left with \(N_{\rm kept}\) = 868 photon detections, out of the original \(N_{\rm tot}=9,997\) in this three-minute dataset. Therefore, we can estimate that the background photon count rate in this dataset is

\[R_{b}=\frac{N_{\rm tot}-N_{\rm kept}}{(1-3\tau/T)t_{\rm obs}}=51.3\ \rm{ photons/s} \tag{6}\]

where \(3\tau/T\) is the width of the phase cut window in this example. The estimated signal photon count rate is

\[R_{s}=\frac{N_{\rm kept}}{t_{\rm obs}}-(3\tau/T)R_{b}=4.2\ \rm{photons/s} \tag{7}\]

where \((3\tau/T)R_{b}\) is an estimate of the rate of background photons remaining after the phase cut. We can also calculate the expected values of \(N_{j^{\prime}}\) for 0 bits and 1 bits after the phase cut:

\[\langle N_{0}\rangle=\frac{(3\tau/T)R_{b}\times t_{\rm obs}}{m}=0.87 \tag{8}\]

Figure 9: (Ground test data) a. Fractional phase \(\phi_{i}\) of each photon detection relative to the nominal (top) and recovered (bottom) clock periods. Note that the signal phase drift over time is corrected when \(\phi_{i}\) is measured relative to the true clock period. Photons with random phases are background detections. b. Histogram of \(\phi_{i}\) relative to the true clock period \(T_{\rm true}=499.9996115\ \mu\)s (\(f_{\rm true}=2000.001554\ \rm{Hz}\)). The dashed lines in the inset show the phase cut window we will apply to this data, with a width 3 \(\tau/T\). (As in Figure 4, each phase bin is 0.25 \(\times\)\(\tau/T\).)

\[\langle N_{1}\rangle=\langle N_{0}\rangle+\frac{R_{s}\times t_{\rm obs}}{n}=12.7 \tag{9}\]

The values of \(N_{j^{\prime}}\) for 0 bits and 1 bits are Poisson distributed, neglecting any saturation effects in the sensor. As shown in Figure 10, the measured distribution of \(N_{j^{\prime}}\) is well described by the normalized sum of two Poisson distributions with means \(\langle N_{0}\rangle\) and \(\langle N_{1}\rangle\).

### Decoding the ID number

As in the example of Section II, the remaining photon detection times are folded by the code length \(mT\) and binned by the clock period \(T\) to obtain a histogram of bit photon counts (Figure 9(b)). In this example, there are again two clear bit photon count distributions corresponding to 0 bits and 1 bits. This time we will use a quantitative method to determine the best bit value threshold for hard decision decoding.

If constant-weight ID numbers are used, \(N_{\rm thresh}\) can be chosen to split the \(b_{j^{\prime}}\) values into the expected number of zeros and ones. The ID number for this ground test data (and all others used in this paper) has a fraction of 1 bits \(n/m=0.50\). As discussed further in Section III.4, choosing a threshold that results in \(n/m\) as close as possible to the expected value minimizes the number of incorrect bits. (This method can also be extended to non

Figure 10: (Ground test data) a. Poisson probability mass functions (PMFs) with means equal to the measured expectation values \(\langle N_{0}\rangle\) and \(\langle N_{1}\rangle\). b. The measured distribution of \(N_{j^{\prime}}\) (for 868 detected photons in 128 bits) agrees well with the combined PMFs for 0 bits and 1 bits.

constant-weight codes if the fraction of 1 bits is restricted to some known range.) Figure 11a shows the fraction of 1 bits in the recovered ID as a function of the bit value threshold. Given several thresholds that result in \(n/m\) = 0.5, we arbitrarily choose the lowest one and set \(N_{\text{thresh}}=5\). The value of each bit is then determined using the hard decision method described in Section II.2.

Finally, we compare the recovered ID number to all the IDs in the registry (with each shift \(0\leq s<m\)) to find the matching ID with the smallest Hamming distance. The recovered ID has zero errors compared to ID 3 in the registry (with a shift of 85), and indeed, ID 3 is the ID number used to program beacon Unit 2 in the ground test.

### Data with reduced signal counts

The previous two examples, using simulated and experimental data, both showed a clear separation between the photon number distributions of 0 bits and 1 bits, and both recovered an ID that exactly matched an ID in the registry. The signal and background rates in these

Figure 11: (Ground test data) a. The fraction of 1 bits in the recovered code as a function of the bit value threshold \(N_{\text{thresh}}\). The known fraction of 1 bits is 0.5 for our 64-of-128-bit error-correcting code, and this information can be used to select an appropriate threshold.

two examples were both within the expected range for an ELROI beacon on a small LEO object under good observing conditions, which demonstrates that the data analysis in that case is expected to be very straightforward. But by restricting our analysis to a shorter one-minute portion of the ground test data, we can see what happens when the number of signal photons detected is so low compared to the background that the distributions of 0 bits and 1 bits significantly overlap, and bit errors become inevitable.

The simple techniques of the previous two examples are still useful even with reduced counts. When each step in the data processing is identical to the analysis of the three-minute dataset, including recovering the clock period and phase with the FFA and applying a 3 \(\tau/T\) phase cut, the resulting bit photon count histogram is shown in Figure 11(a). Although there is no longer an obvious distinction between the distributions of 0 bits and 1 bits, the fraction of 1 bits \(n/m\) may still be used to choose the best value of \(N_{\text{thresh}}\). Figure 12 shows that choosing a threshold that results in \(n/m\) as close as possible to the expected value minimizes the number of incorrect bits. \(N_{\text{thresh}}=2\) achieves \(n/m\) = 0.5 for this dataset.

The best recovered ID has five bit errors compared to the true ID. However, all other IDs have significantly more errors (the second-best match has 45 bit errors) so even using

Figure 12: (Ground test data) a. Histogram showing the frequency of photon numbers in time bins corresponding to the bits of the code, for a 1-minute subset of the 3-minute dataset analyzed previously. b. In this example, there is no clear distinction between the distributions of 1 bits and 0 bits, but the known fraction of 1 bits may still be used to determine the most appropriate threshold. The bit error rate (fraction of bits that are incorrect compared to the known ID number) has a minimum at the value of \(N_{\text{thresh}}\) that achieves the known fraction of 1 bits \(n/m\) = 0.5.

this shortened dataset, we can confidently identify the ID number of the beacon. Because of the ECC scheme used to generate the registry IDs (Section I.3), all incorrect IDs are guaranteed to be larger Hamming distance from the recovered ID than the true ID, up to 12 bit errors in the recovered ID. As discussed in Sections IV and V, more sophisticated analysis techniques, improved ECC schemes, and operational context may be able to further improve our confidence that the recovered ID number is correct even for \(>12\) bit errors.

## IV Error Rates

As discussed in Section I.3, all the example ELROI IDs used in this paper are 128-bit binary sequences with a minimum 24-bit distance between a given ID and all other sequences (allowing cyclic permutation). This guarantees that for up to 12 incorrect bits, the true ID will be closer to the recovered ID than any other ID in the ELROI registry. Thus, if the bit error rate (frequency of individual bit errors) in a given recovered ID is 12/128 or lower, the codeword error rate (probability of incorrect beacon identifications) for that ID is zero. For more than 12 bit errors, the codeword error rate increases with

Figure 13: Numerical simulation of bit error rates and codeword error rates in recovered ELROI IDs, for different signal rates (in photons/s). The background rate for all observations (after spectral filtering and phase cut) is assumed to be 0.36 photons/s, an estimated value for a small sunlit LEO satellite. The signal rate of 3.3 photons/s is the value estimated for a typical beacon at 1000 km range in [1]. Each data point represents \(10^{7}\) simulated observations. a. Simulated bit error rates. The dashed horizontal line indicates a bit error rate of 12/128. b. Simulated codeword error rates.

Figure 13 shows the results of a numerical simulation of bit error rates and codeword error rates in recovered IDs. Bit photon counts \(N_{j}\) were randomly generated for 0 bits and 1 bits, and the hard decision decoding method described in Section III.4 was used to determine bit values, with the threshold chosen to achieve the fraction of 1 bits closest to 0.50 for each recovered ID. If the number of bit errors in an ID was 13 or more, it was counted as a codeword error. This is a conservative approach, as a recovered ID with more than 12 bit errors may still be closer to the true ID than any other ID in the registry.

The error rates in Figure 13 may appear high compared to typical optical communications applications, but they are acceptable for the ELROI application. Note that for a signal rate of 3.3 photons/s (comparable to our current LEO prototypes) the code error rate is 1 in 100,000 after only two minutes of observation. This means that the chance of mis-identification is 1 in 100,000 after two minutes if all ID numbers in the ECC scheme are in use. In practice, context will also give additional information, and not all possible IDs in the registry will be equally likely--for example, if 100 CubeSats are launched together into a known orbit, all carrying ELROI beacons, the codeword error rate for identifying one of these CubeSats will be greatly reduced compared to a complete registry of thousands or millions of IDs. Additional observation time also reduces the chance of mis-identification.

According to our link budget calculations, signal rates of 3 to 20 photons/s will be typical at our ground station for prototype ELROI beacons on LEO satellites, depending on the beacon power and range [1; 7]. We expect to be able to identify our current flight prototypes with codeword error rates of \(10^{-5}\) or lower, and under ideal conditions codeword error rates may reach \(10^{-9}\).

Figure 14 shows how codeword error rates vary with the background rate for a fixed signal rate of 3.3 photons/s. If the actual observed background rate is three times higher than expected, less than a minute of additional observation is needed to reach a codeword error rate of \(10^{-5}\). If the observed background rate is ten times higher than expected, approximately three minutes of additional observation are needed to reach the same codeword error rate. In this case, the ID may not be able to be identified with the same level of confidence in a single pass over a ground station, but can still be identified with lower confidence. Higher-power beacons may be used to improve performance for large satellites with high background rates from reflected sunlight (further discussion of these design trade-offs may be found in Reference 1).

## V Conclusions

We have described the basic data analysis techniques needed to recover the unique ELROI ID number for a space object, and we invite readers to consider observing our upcoming test flights. As we have shown with both simulated and ground test data, even the simple methods described here can easily recover the beacon ID for a small LEO satellite.

However, further optimization is possible and should be explored. Improvements to both the encoding and decoding schemes may be considered. The examples shown here have used a hard decision decoding method. Although Figure 12 suggests this method may be close to optimal, a registry search for the best ID after hard decision decoding weights all bit errors between the recovered ID and a registry ID equally, without considering the actual number of photons detected for each bit. A soft decision decoding approach might improve on this by weighting bit errors by the number of photons detected.

Although the simple ECC scheme presented here is sufficient for many practical use cases, there are codes that achieve substantially better Hamming distance (and therefore improved error tolerance) for the same code length and number of codes; for example, BCH

Figure 14: Numerical simulation of codeword error rates with a fixed signal rate of 3.3 photons/s and three different background rates (after spectral filtering and phase cut). 0.36 background photons/s is a reasonable estimate for a LEO CubeSat.

codes [17; 18]. There may also be an advantage to using forward error correction and Bayesan decoding with prior information, as implemented in (for example) turbo codes, LDPC codes, and, recently, polar codes [19; 20; 21]. These types of ECC codes are frequently used in modern digital communications, including space communications, and have known optimal decoding techniques.

## Funding

US Department of Energy through the Los Alamos National Laboratory (LANL) Laboratory Directed Research and Development (LDRD) program

[PERSON] Center for Innovation at Los Alamos National Laboratory

Center for Space and Earth Sciences at Los Alamos National Laboratory

## Acknowledgments

ELROI hardware and software was developed and tested at LANL by [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], and [PERSON]. The ELROI long-range ground test was assisted by [PERSON], [PERSON], [PERSON], and [PERSON].

## References

* (1) [PERSON] and [PERSON], \"Extremely Low Resource Optical Identifier: A License Plate for Your Satellite,\" AIAA Journal of Spacecraft and Rockets **55**, 1014-1023 (2018).
* (2) [PERSON]. [PERSON], \"OPTICAL IDENTIFICATION BEACON, patent application 15/232,857,\" (2016).
* (3) [PERSON], \"OPTICAL IDENTIFICATION BEACON, provisional patent application 62/218,232,\" (2015).
* (4) \"Space-Track.org,\" (2017).

* (5)\"IADC Statement on Large Constellations of Satellites in Low Earth Orbit: 4.3.5 Trackability,\" Tech. Rep. IADC-15-003 (Inter-Agency Space Debris Coordination Committee Steering Group, 2017).
* [PERSON], [PERSON], and [PERSON] (2018)[PERSON], [PERSON], and [PERSON], \"Space Traffic Management in the Age of New Space,\" Tech. Rep. (The Aerospace Corporation, 2018).
* [PERSON] _et al._ (2018)[PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], and [PERSON], \"Progress on ELROI satellite license plate flight prototypes,\" in _Proc. SPIE 10659, Advanced Photon Counting Techniques XII_, May, edited by [PERSON] and [PERSON] (SPIE, 2018) p. 23, arXiv:1804.00649.
* [PERSON] (2018)[PERSON], \"The performance of Geiger mode avalanche photo-diodes in free space laser communication links,\" in _Proc. SPIE 10641, Sensors and Systems for Space Applications XI_, May, edited by [PERSON] and [PERSON] (SPIE, 2018) p. 23.
* [PERSON] (2018)[PERSON], \"Quantum limited performance of optical receivers,\" in _Proc. SPIE 10641, Sensors and Systems for Space Applications XI_, May, edited by [PERSON] and [PERSON] (SPIE, 2018) p. 21.
* [PERSON] _et al._ (2007)[PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], and [PERSON], \"Design of an Optical Photon Counting Array Receiver System for Deep-Space Communications,\" Proceedings of the IEEE **95**, 2059-2069 (2007).
* [PERSON], [PERSON], and [PERSON] (2004)[PERSON], [PERSON], and [PERSON], \"MLCD: overview of NASA's Mars laser communications demonstration system,\" in _Proc. SPIE 5338, Free-Space Laser Communication Technologies XVI_, June 2004, edited by [PERSON], [PERSON], and [PERSON] (2004) p. 16.
* [PERSON] (2013)[PERSON], \"Imaging One Photon at a Time,\" Tech. Rep. LA-UR-13-22617 (Los Alamos National Laboratory, 2013).
* [PERSON] (1950)[PERSON], \"Error Detecting and Error Correcting Codes,\" Bell System Technical Journal **29**, 147-160 (1950).
* [PERSON] and [PERSON] (2005)[PERSON] and [PERSON], \"Optical detection of rapidly moving objects in space,\" Applied Optics **44**, 423 (2005).
* [PERSON] (1969)[PERSON], \"Fast folding algorithm for detection of periodic pulse trains,\" Proceedings of the IEEE **57**, 724-725 (1969).

* (16) [PERSON], \"[[https://github.com/petigura/FFA](https://github.com/petigura/FFA)]([https://github.com/petigura/FFA](https://github.com/petigura/FFA)),\".
* (17) [PERSON], \"Codes correcteurs d'erreurs,\" Chiffres (in French) **2**, 147-156 (1959).
* (18) [PERSON] and [PERSON], \"On A Class of Error Correcting Binary Group Codes,\" Information and Control **2**, 68-79 (1960).
* (19) [PERSON], \"Channel Polarization: A Method for Constructing Capacity-Achieving Codes for Symmetric Binary-Input Memoryless Channels,\" IEEE Transactions on Information Theory **55**, 3051-3073 (2009).
* (20) [PERSON], \"Low-density parity-check codes,\" IEEE Trans. Info. Theory **8**, 21-28 (1962).
* IEEE International Conference on Communications_, Vol. 2 (IEEE, 1993) pp. 1064-1070.