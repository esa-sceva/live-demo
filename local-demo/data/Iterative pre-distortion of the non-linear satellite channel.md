# Iterative pre-distortion of the non-linear satellite channel

[PERSON], [PERSON], [PERSON], and [PERSON]

[PERSON]* and [PERSON] are with the OPERA - Wireless Communications Group, Universite Libre de Bruxelles, Brussels, Belgium.M. Dervin is with Thales Alenia Space, Toulouse, France.K. Kasai is with Tokyo Institute of Technology, Tokyo, Japan.

###### Abstract

Digital Video Broadcasting - Satellite - Second Generation (DVB-S2) is the current European standard for satellite broadcast and broadband communications. It relies on high order modulations up to \(32\)-amplitude/phase-shift-keying (APSK) in order to increase the system spectral efficiency. Unfortunately, as the modulation order increases, the receiver becomes more sensitive to physical layer impairments, and notably to the distortions induced by the power amplifier and the channelizing filters aboard the satellite. Pre-distortion of the non-linear satellite channel has been studied for many years. However, the performance of existing pre-distortion algorithms generally becomes poor when high-order modulations are used on a non-linear channel with a long memory. In this paper, we investigate a new iterative method that pre-distorts blocks of transmitted symbols so as to minimize the Euclidian distance between the transmitted and received symbols. We also propose approximations to relax the pre-distorter complexity while keeping its performance acceptable.

 Pre-distortion, non-linear satellite channel, DVB-S2.

## I Introduction

In broadcast or broadband satellite communication, information is most often exchanged between one hub and many user terminals in a so-called star topology. We focus here on the forward link, defined as the link from the hub towards the user terminals, while the return link (when it exists) refers to the link from a user terminal towards the hub. In such context, the available radio spectrum is generally divided into sub-bands, also referred to as channels, which are separately amplified by different power amplifiers aboard the satellite. In a single carrier per channel scenario, each carrier transmitted on the forward link is separately amplified by a different power amplifier. As a single carrier signal shows limited envelope variations, this conveniently allows each power amplifier to be driven close to its saturation point, so that the power consumption aboard the satellite is minimized. When the link budget is good enough, it is possible to increase the spectral efficiency of the system by using high-order modulations. However, the transmission channel includes non-linear inter-symbol interference (ISI) due to the combination of the non-linear high power amplifier (HPA) aboard the satellite with linear filtering present in the channel. Moreover, the larger the modulated carrier bandwidth, the more interference occurs due to the bandpass nature of the onboard channelizing filters. Higher-order modulations being more sensitive to the non-linear ISI, compensation algorithms are necessary to remove the non-linear interference induced by the satellite channel, and fully benefit from the spectral efficiency improvement.

In the literature, the methods proposed to compensate for the non-linear interference can be divided into two categories: equalization and pre-distortion.

Firstly, the non-linear interference can be mitigated with an equalizer at the receiver side. If the channel is exactly known, the maximum-a-posteriori (MAP) symbol detection algorithm and the alternative maximum-likelihood sequence detection algorithm can be perfectly defined. However, the complexity of these optimum algorithms increases exponentially with the channel length and modulation order, so that several sub-optimum algorithms have been proposed in the literature. For instance, in [1], the detection of the received signal is based on a reduced channel model described in [2] combined with a channel shortening technique described in [3]. Adaptive non-linear equalizers have been proposed in [4, 5], where a-priori channel knowledge is not required. In [6], joint equalization and channel decoding is performed using Gaussian processes. To take advantage of the channel coding gain, iterative turbo-equalization structures have also been considered [7, 8].

Secondly, the channel non-linear interference can be compensated by pre-distortion at the transmitter side. This approach is particularly interesting in the forward link of a broadband satellite system, where it is preferred to concentrate the computational load in the hub and relax as much as possible the complexity of the terminals. One usually uses the term _signal_ (or _waveform_) pre-distortion when it is located _after_ the pulse shaping filter. This kind of pre-distortion can be applied to compensate memoryless channels, as shown in [9, 10] and references therein. The pre-distorter is then an approximation of the inverse characteristic of the power amplifier at the transmitter side. This method can be analog or digitally implemented (see for example the adaptive implementations in [11] and [12]). On the other hand, we refer to _data_ pre-distortion when a pre-distortion of the data symbols is applied _prior_ to the pulse shaping. This allows compensating for ISI and avoids out-of-band emissions. A first approach is to consider a pre-distorter based on the Volterra model, a common tool to describe the input-output relation of a non-linear system with memory, as described in [13]. The coefficients of the pre-distorter are adaptively determined to minimize the mean-square error (MSE), as in [14, 15]. The complexity of such pre-distorters may be high and the convergence of adaptive algorithms maybe slow, so that pre-distortion methods based on reduced Volterra models have been studied in [16] and references therein. The order-\(p\) inverse for non-linear systems has been described in [17] and applied to the satellite channel in [18]. The order-\(p\) pre-distorter removes, up to the order \(p\), all Volterra terms from the channel model relating the received to the transmitted symbols (note that this algorithm can actually be applied to both pre-distortion and equalization). Another structure of interest relies on a look-up table (LUT). In [19], the value of each pre-distorted symbol is a function of the neighboring initial symbols, which can be calculated offline and stored in a LUT. The pre-computation of these values aims at minimizing the MSE between the initial and the received symbols. The performance of this algorithm has been assessed for high-order modulations in [20].

Except for the order-\(p\) inverse, existing pre-distortion methods suffer from a performance loss due to their intrinsic structure: pre-distorters based on a Volterra structure cannot cope with the huge number of coefficients required to theoretically represent the channel inverse and are most of the time limited in order and memory. Pre-distorters based on LUT have a number of entries exponentially growing with the modulation order so that the pre-distorter length must be limited. In case of large channel length and high HPA non-linearity, these pre-distorters are therefore expected to perform poorly. This is also the case for the order-\(p\) pre-distorter since it creates higher order terms, that become more powerful than the cancelled terms. In this paper, we propose an iterative pre-distortion algorithm, which can be seen as a pre-distorter of infinite order and finite length. Very large pre-distorter lengths can be considered because the algorithm complexity computed per symbol is independent of this parameter. Improved performance is therefore expected compared to state-of-the-art pre-distortion methods. The proposed scheme independently pre-distorts successive symbol blocks. To pre-distort each block of symbols, an iterative algorithm is used, aiming at minimizing the Euclidian distance between the initial symbol and the received symbol sequence. Based on the system model defined in Section II, we describe the proposed algorithm in Section III. A main concern of the algorithm design is its complexity, so that variations of the algorithm of much lower complexity are proposed in Section IV. The complexity and the performance of the different algorithms are compared in Sections V and VI respectively.

## II System model

### _Satellite Channel_

A block diagram of the satellite channel is depicted in Fig. 1. At the transmitter, data bits are first encoded, interleaved and linearly modulated. In this work, we will only consider the highest modulation order defined in the DVB-S2 standard ([21]): the 32-amplitude/phase-shift-keying (APSK) modulation. Based on the data symbols, denoted as \(s(n)\), the pre-distorter produces the pre-distorted symbols, denoted as \(x(n)\). The pre-distorted symbols are shaped with a square-root raised cosine (SRRC) filter and the resulting signal is transmitted to the satellite. At the satellite, the input multiplexer (IMUX) filter is a bandpass filter that selects the sub-band to be amplified. The satellite HPA can be seen as a non-linear memoryless device. The output multiplexer (OMUX) filter is also a bandpass filter, necessary to remove the out-of-band components produced by the power amplifier. At the receiver, the signal is filtered with a SRRC filter and sampled to produce the received samples \(y(n)\). The demodulator performs a memoryless detection, assuming that residual interference after pre-distortion behaves like additive white Gaussian noise (AWGN). The demodulator produces a-posteriori statistics of the encoded bits, which are transmitted to the decoder after desinterleaving. The pre-distortion block is assumed to have a perfect knowledge of the channel, and is dedicated to the mitigation of the non-linear ISI induced by the combination of the linear filters and the HPA. The pre-distortion block is further detailed in the next section.

### _Volterra Model_

The Volterra model is an analytical model that describes the relation between the input and the output of a non-linear system with memory. The case of the baseband non-linear satellite channel has been described in [18]. The relation between the pre-distorted symbols \(x(n)\) at the channel input and the received symbols \(y(n)\) is given by:

\[\begin{split} y(n)=&\sum_{m=0}^{\infty}\sum_{n_{1} \ldots n_{2m+1}}H_{2m+1}(n_{1}...n_{2m+1})x(n-n_{1})...\\ & x(n-n_{m+1})x^{*}(n-n_{m+2})...x^{*}(n-n_{2m+1})+w(n).\end{split} \tag{1}\]

The coefficients \(H_{2m+1}(n_{1}...n_{2m+1})\) are called the Volterra kernels of the system. The first sum in (1) represents the different orders of the non-linearity induced by the power amplifier. The second set of sums represents the memory of the system, which is theoretically infinite. In practice however, the length of the channel can be reasonably assumed of finite length. We denote the anti-causal memory of the channel as \(L_{1}\) and the causal memory of the channel as \(L_{2}\). The total channel length is then denoted as \(L_{\text{c}}=L_{1}+L_{2}+1\). In (1), each index \(n_{i}\) varies thus from \(-L_{1}\) to \(L_{2}\). The received symbols are also corrupted by thermal noise \(w(n)\), which is supposed to behave like AWGN.

### _Total degradation_

The performance of pre-distortion or equalization algorithms in a non-linear satellite channel is usually quantified in terms of the total degradation [19, 20, 22]. The total degradation, denoted as TD, is defined as follows:

\[\text{TD}[dB]= \text{OBO}[\text{dB}]+L^{\text{omax}}[\text{dB}]\] \[+\left[\frac{Eb}{N_{0}}\right]^{\text{NL}}_{\text{req}}[\text{ dB}]-\left[\frac{Eb}{N_{0}}\right]^{\text{AWGN}}_{\text{req}}[\text{dB}], \tag{2}\]

where OBO is the HPA power backoff. \(L^{\text{omax}}\) is the mean power loss in the OMUX filter, \(\left[\frac{Eb}{N_{0}}\right]^{\text{NL}}_{\text{req}}\) and \(\left[\frac{Eb}{N_{0}}\right]^{\text{AWGN}}_{\text{req}}\) are the average symbol energy over noise ratio required to achieve a given bit error rate (BER) or frame error rate (FER), in the non-linear and AWGN channels. As shown by (2), the total degradation depends on the OBO, and the optimum OBO which minimizes the total degradation can significantly be different depending on the considered pre-distortion technique, as shown in [19, 20, 22]. Pre-distortion techniques must therefore be compared based on the minimum total degradation they can reach.

## III Per-block iterative pre-distortion

### _Minimization of Euclidian Distance_

We consider the pre-distortion of length-\(N\) symbol blocks, assuming that the transmitter has perfect knowledge of the channel. For a given block, we denote by \(\mathbf{s}\) the vector with elements comprising a symbol block: \(\mathbf{s}=[s(1)...s(N)]\). For each symbol block, the pre-distorter produces a modified symbol block of length \(N\), denoted by the vector \(\mathbf{x}=[x(1)...x(N)]\). At the receiver, \(N\) samples are also gathered in a vector of size \(N\), denoted by \(\mathbf{y}=[y(1)...y(N)]\). In addition, we denote by \(\mathbf{y}(\mathbf{x})\) the vector \(\mathbf{y}\) of the received symbols when the block \(\mathbf{x}\) is sent at the channel input. In this section, we propose an algorithm that precodes the block \(\mathbf{x}\) so that \(||\mathbf{y}-\mathbf{s}||_{2}\) is minimized.

Since the optimal compensation of a finite length channel is of infinite length, it is important to take \(N\) as large as possible. However, \(N\) cannot be too large to prevent too high latency. In this work, we take \(N\) equal to the number of symbols in the physical layer frame as defined in the DVB-S2 standard (a few thousand symbols). Note that the length of the block \(\mathbf{y}\) should be equal to \(N+L_{\text{c}}-1\). However, memoryless detection is applied on consecutive received symbols, so that the symbols \(y(-L_{1})\),..., \(y(-1)\) and \(y(N+1)\),..., \(y(N+L_{2})\) can be neglected. The pre-distorter minimizes the Euclidian distance assuming a noiseless channel. Since the AWGN is independent of the transmitted sequence, this also minimizes the MSE at the receiver in presence of AWGN. The vector \(\mathbf{y}\) can be developed using (1). However, there is no straightforward derivation of the block \(\mathbf{x}\) that minimizes \(||\mathbf{y}-\mathbf{s}||_{2}\). We therefore propose an iterative algorithm to determine the pre-distorted block \(\mathbf{x}\). Each iteration of the algorithm is divided into \(N\) steps, respectively focused on consecutive symbols of the block of interest. The pre-distorted block after Step \(j\) of Iteration \(k\) is denoted as \(\mathbf{x}_{k,j}=[x_{k,j}(1)...x_{k,j}(N)]\), where only the \(j\)th pre-distorted value is modified and is chosen to minimize \(||\mathbf{y}-\mathbf{s}||_{2}\) when \(\mathbf{x}_{kj}\) is transmitted. All other pre-distorted values are thus kept equal to their values from the previous step. For each iteration, \(x_{k,j}(n)\) is mathematically expressed as follows. For the first step (\(j=1\)),

\[x_{k,1}(n)=\begin{cases}&x_{k-1,N}(n),\quad\;n\
eq 1,\\ &\underset{x_{k,1}(1)}{\operatorname{argmin}}[||\mathbf{y}-\mathbf{s}||_{2} |\forall i\
eq 1:x(i)=x_{k-1,N}(i)],\\ &n=1,\end{cases} \tag{3}\]

and thereafter (\(j>1\)),

\[x_{k,j}(n)=\begin{cases}&x_{k,j-1}(n),\quad\;n\
eq j,\\ &\underset{x_{k,j}(j)}{\operatorname{argmin}}[||\mathbf{y}-\mathbf{s}||_{2} |\forall i\
eq 1:x(i)=x_{k,j-1}(i)],\\ &n=j.\end{cases} \tag{4}\]

Note that \(x_{k,1}(n)\) is calculated using the end values of the previous iteration, except for the first iteration where \(x_{k,1}(n)\) is calculated using the un-pre-distorted values. The vector \(\epsilon_{\mathbf{k}j}\) is defined as the difference between \(\mathbf{y}\) and \(\mathbf{s}\) when the sequence obtained after Step \(j\) of Iteration \(k\) is transmitted:

\[\epsilon_{\mathbf{k}j}\triangleq\mathbf{y}-\mathbf{s}|\forall i:x(i)=x_{k,j} (i). \tag{5}\]

By definition of the algorithm, we have:

\[||\epsilon_{\mathbf{k}j}||_{2}\leq||\epsilon_{\mathbf{k}j,1}||_{2}, \tag{6}\]

Fig. 1: Block diagram of the satellite channel so that the convergence of proposed algorithm is ensured. The term \(||\mathbf{y}-\mathbf{s}||_{2}\) minimized in (3) can be seen as a non-linear function of the complex variable \(x_{k,j}(n)\). The coefficients of this function can be found using the Volterra model and depend on the fixed pre-distorted values in (3). Since the channel has finite length, (3) can be simplified as:

\[x_{k,j}(j)= \underset{x_{k,j}(j)}{\mathrm{argmin}}[||\mathbf{y}-\mathbf{s}|| _{2}]\forall i\
eq j:x(i)=x_{k,j-1}(i)]\] \[= \underset{x_{k,j}(j)}{\mathrm{argmin}}[\sum_{m=max(1,\ j-L1)}^{ min(N,\ j+L2)}|y(m)-s(m)|^{2}|\forall i\
eq j:\] \[x(i)=x_{k,j-1}(i)]. \tag{7}\]

The complexity of the algorithm is very high since it is necessary to successively find the minimum of \(N\) complex non-linear functions for each iteration. Moreover, the number of Volterra coefficients in each equation can be very high in the case of high-order non-linearities. Therefore, the pre-distorted symbols defined in (3) are difficult to compute in practice. In the next subsection, we propose an algorithm of much lower complexity to compute the pre-distorted symbols. We refer to this algorithm as the _small-variation_ algorithm.

### _Small-Variation Algorithm_

The small-variation algorithm has the same iterative structure as the algorithm presented in the previous subsection. However, at Step \(j\) of Iteration \(k\), it calculates a suboptimal value for \(x_{k,j}(j)\) in a much less complex way. We first define \(\Delta_{k,j}\) as:

\[x_{k,j}(j)=x_{k,j-1}(j)+\Delta_{k,j} \tag{8}\]

Thus, the variation from \(x_{k,j-1}(j)\) to \(x_{k,j}(j)\) is considered as the unknown variable instead of \(x_{k,j}(j)\) itself. The case \(j=1\) is not explicitly given anymore in the following derivations, as it is always similar to (3). The vector \(\mathbf{\Delta}_{k,j}\) is defined as a zero vector of length \(N\), except for the element \(j\) which is equal to \(\Delta_{k,j}\), so that:

\[\mathbf{x}_{kj}=\mathbf{x}_{kj,l}+\mathbf{\Delta}_{k,j}. \tag{9}\]

We define the value \(\Delta_{k,j}^{\text{opt}}\) as the optimum value that minimizes (4):

\[\Delta_{k,j}^{\text{opt}}=\underset{\Delta_{k,j}}{\mathrm{argmin}}[ ||\mathbf{y}-\mathbf{s}||_{2}]\forall i\
eq j:x(i)=x_{k,j-1}(i),\] \[x_{k,j}(j)=x_{k,j-1}(j)+\Delta_{k,j}] \tag{10}\]

It is possible to simplify (10) as in (7), but we prefer to adopt the following more compact notation:

\[\Delta_{k,j}^{\text{opt}}=\underset{\Delta_{k,j}}{\mathrm{argmin}}[||\mathbf{y }(\mathbf{x}_{kj,l}+\mathbf{\Delta}_{k,j})-\mathbf{s}||_{2}]. \tag{11}\]

We define:

\[\mathbf{F}_{kj}^{\text{NL}}\triangleq\mathbf{y}(\mathbf{x}_{kj,l}+\mathbf{ \Delta}_{kj})-\mathbf{y}(\mathbf{x}_{kj,l}) \tag{12}\]

so that:

\[\Delta_{k,j}^{\text{opt}} =\underset{\Delta_{k,j}}{\mathrm{argmin}}[||\mathbf{y}(\mathbf{ x}_{kj,l})-\mathbf{s}+\mathbf{F}_{kj}^{\text{NL}}||_{2}]\] \[=\underset{\Delta_{kj}}{\mathrm{argmin}}[||\epsilon_{k,j,l}+ \mathbf{F}_{kj}^{\text{NL}}||_{2}]. \tag{13}\]

Each element \(F_{k,j}^{\text{NL}}(n)\) represents the output \(n\) variation resulting from a variation of the input symbol j at Step \(j\) during Iteration \(k\). The vector \(\mathbf{F}_{k,j}^{\text{NL}}\) can be seen as a vector of functions depending on the scalar variable \(\Delta_{k,j}\). Inspecting (1) and (12), it can be mathematically computed that each element \(F_{k,j}^{\text{NL}}(n)\) takes the form:

\[F_{k,j}^{\text{NL}}(n)=\begin{cases}&0,\quad n<j-L_{2},n>j+L_{1},\\ &\sum_{m_{1}=0}^{\infty}\sum_{m_{2}=0}^{\infty}A_{k,j}^{n}(m_{1},m_{2})\Delta_ {k,j}^{m_{1}}(\Delta_{k,j}^{*})^{m_{2}},\\ &n\geq j-L_{2},n\leq j+L_{1},\end{cases} \tag{14}\]

where the coefficients \(A_{k,j}^{n}(m_{1},m_{2})\) depend on the Volterra coefficients and the sequence of pre-distorted symbols. For the sake of clarity, Appendix A gives some examples for the coefficients \(A_{k,j}^{n}(m_{1},m_{2})\) in the case of simple Volterra models consisting of only a single Volterra coefficient. In the general case of a channel depending on several Volterra coefficients, the value of \(A_{k,j}^{n}(m_{1},m_{2})\) can be obtained by first computing the value of \(A_{k,j}^{n}(m_{1},m_{2})\) corresponding to each Volterra coefficient taken independently and then summing all the obtained values.

The small-variation algorithm is based on the assumption that each function \(F_{k,j}^{NL}(n)\) can be approximated by keeping only its linear dependency on \(\Delta_{k,j}\):

\[F_{k,j}^{\text{NL}}(n)\approx F_{k,j}^{\text{Lin}}(n)\triangleq A_{k,j}^{n}(1, 0)\Delta_{k,j}+A_{k,j}^{n}(0,1)\Delta_{k,j}^{*}. \tag{15}\]

This will be more likely the case for small values of \(\Delta_{k,j}\). Denoting \(\mathbf{F}_{k,j}^{\text{Lin}}(\Delta_{k,j})\), \(\mathbf{A}_{k,j}(1,0)\), and \(\mathbf{A}_{k,j}(0,1)\) the vectors obtained with elements \(F_{kj}^{\text{Lin}}(n)\), \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\), with \(n\) varying from \(1\) to \(N\), we have:

\[\mathbf{F}_{k,j}^{\text{NL}}\approx\mathbf{F}_{k,j}^{\text{Lin}}\triangleq \mathbf{A}_{k,j}(1,0)\Delta_{k,j}+\mathbf{A}_{k,j}(0,1)\Delta_{k,j}^{*} \tag{16}\]

Instead of calculating the value \(\Delta_{k,j}^{\text{opt}}\) from (11), the small-variation algorithm calculates \(\Delta_{k,j}^{Lin}\) defined as:

\[\Delta_{k,j}^{\text{Lin}}=\underset{\Delta_{k,j}}{\mathrm{argmin}}[||\epsilon_{k,j-1}+\mathbf{F}_{k,j}^{Lin}||_{2}] \tag{17}\]

The objective function \(||\mathbf{y}(\mathbf{x}_{kj,l})-\mathbf{s}+\mathbf{F}_{kj}^{\text{NL}}||_{2}\) in (13) is approximated by a second order equation, given by \(||\epsilon_{k,j-1}+\mathbf{F}_{k,j}^{Lin}||_{2}\). Using partial derivatives, the optimum value of \(\Delta_{k,j}\) that minimizes (17), can be found by solving a system of two linear equations with two unknowns (the real and imaginary parts of \(\Delta_{k,j}\)), which makes the calculation much easier than minimizing the exact non-linear equation. The main difficulty raised by the proposed algorithm is the complexity to assess the parameters \(\mathbf{A}_{k,j}(m_{1},m_{2})\) as they depend on all Volterra coefficients. Section IV will be devoted to this question.

### _Linearity Assumption_

The variation \(\Delta_{k,j}^{\text{Lin}}\) is computed based on the approximation (15), which is only valid for small values of \(\Delta_{k,j}^{\text{Lin}}\). In practice, we consider that the applied variation \(\Delta_{k,j}^{\text{applied}}\) has at least to decrease the Euclidian distance between the initial and the received symbols. Mathematically, this is expressed as:

\[(||\epsilon_{k,j-1}+\mathbf{F}_{k,j}^{\text{NL}}||_{2}|\Delta_{k,j}=\Delta_{k,j }^{\text{applied}})\leq||\epsilon_{k,j-1}||_{2}. \tag{18}\]Taking \(\Delta_{k,j}^{\text{applied}}=\Delta_{k,j}^{\text{Lin}}\) does not ensure that (18) is verified at each step since the linear assumption may not be met. Therefore, we consider instead that the applied variation is given by:

\[\Delta_{k,j}^{\text{applied}}=\gamma\Delta_{k,j}^{\text{lin}}, \tag{19}\]

where \(\gamma\) is a real number in the interval \([0,1]\). It is proven in Appendix B that \(\gamma\Delta_{k,j}^{\text{lin}}\) is a sub-optimum solution of the second order approximation of the objective function:

\[(||\epsilon_{k,j-1}+\mathbf{F}_{k,j}^{\text{lin}}||_{2}|\Delta_{k,j}=\gamma \Delta_{k,j}^{\text{Lin}})\leq||\epsilon_{k,j-1}||_{2}. \tag{20}\]

It is always possible to define \(\gamma\) small enough to meet the linear approximation (15), so that the sub-optimum solution of (17) becomes also a sub-optimum solution of (13), which means that \(\Delta_{k,j}^{\text{applied}}\) satisfies (18). The value of \(\gamma\) could be optimized at each step of the algorithm. For instance, decreasing values of \(\gamma\) can be applied until (18) is true. However, the complexity of such approach is difficult to predict. In this work, we follow an approach similar to the trust-region method described in [23], where the norm of the applied variation \(|\Delta_{k,j}^{\text{applied}}|\) is limited to a pre-defined value \(\Delta_{max}\). The value of \(\gamma\) is chosen so as to make this statement true. Mathematically, \(\gamma\) is defined as follows:

\[\gamma=\begin{cases}&1,\quad|\Delta_{k,j}^{\text{lin}}|\leq\Delta_{max},\\ &\Delta_{max}|\Delta_{k,j}^{\text{lin}}|^{-1},\quad|\Delta_{k,j}^{\text{lin}}|> \Delta_{max}.\end{cases} \tag{21}\]

If the so obtained \(\gamma\) and the resulting \(\Delta_{k,j}^{\text{applied}}\) does not meet (18), no variation is applied at the given step. The value of \(\Delta_{max}\) is a trade-off between convergence speed and maximum achievable performance, as shown in Section V.

### _Linear filtering_

Besides the iterative pre-distortion algorithm, a linear filter is applied to the transmitted signal to remove the linear interference caused by the channel. The iterative pre-distortion algorithm includes this linear filter as part of the channel. Intuitively this improves the convergence of the pre-distortion algorithm because the optimum values of the pre-distorted symbols are closer to the values of the un-pre-distorted symbols. Note that this filter could alternatively be applied at the receiver. This would keep the peak-to-average power ratio (PAPR) lower at the transmitter and limit the induced higher-order terms (see [18]). However, this would also amplify the noise on the channel deeps. In this work, we stick to the transmitter alternative.

## IV Complexity Reduction of the Small-Variation Algorithm

The algorithm presented in the previous section is rather theoretical, as the number of Volterra coefficients can be very large. We now present more practical methods to calculate the coefficients \(A_{k,j}^{n}(m_{1},m_{2})\). The coefficients \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\) are necessary to calculate \(\Delta_{k,j}^{\text{lin}}\). We propose three methods to compute these coefficients. The first has arbitrarily high precision, so that it can be considered as an exact and practical method to calculate \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\). The two other methods calculate only approximations of these coefficients, but are less complex than the first method. The other coefficients \(A_{k,j}^{n}(m_{1},m_{2})\), with \(m_{1}>1\) or \(m_{2}>1\), have also to be computed in order to verify the linearity assumption, so that the complexity still remains very high. The final part of this section shows how the calculations of these coefficients can be avoided.

_Calculations of the Coefficients \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\) Based on Channel Simulations_

The coefficients \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\) can be estimated by the following procedure. At Step \(j\) of Iteration \(k\), the channel outputs are calculated that result from three different channel input variations:

\[1)\Delta_{k,j}=0\hskip 56.905512 pt2)\Delta_{k,j}=\epsilon_{\text{r}} \hskip 56.905512 pt3)\Delta_{k,j}=\epsilon_{\text{i}} \tag{22}\]

where \(\epsilon_{\text{r}}\) and \(\epsilon_{\text{i}}\) are respectively small real and pure imaginary numbers. The respective channel outputs are denoted as \(y(n)\), \(y_{t}(n)\) and \(y_{t}(n)\). If \(\epsilon_{\text{r}}\) and \(\epsilon_{\text{i}}\) are chosen sufficiently small, there is a linear relation between the input and output variations:

\[y_{t}(n) =y(n)+A_{k,j}^{n}(1,0)\epsilon_{\text{r}}+A_{k,j}^{n}(0,1)\epsilon _{\text{r}}\] \[y_{i}(n) =y(n)+A_{k,j}^{n}(1,0)\epsilon_{\text{i}}-A_{k,j}^{n}(0,1)\epsilon _{\text{i}}. \tag{23}\]

For each \(n\), (23) form a set of two equations with two unknowns, \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\), so that they can easily be estimated. Only \(L_{c}\) sets of equations need to be solved due to the finite channel length assumption. The smaller \(\epsilon_{\text{r}}\) and \(\epsilon_{\text{i}}\), the more accurate the calculation. This method still has a high complexity since three simulations of the channel at each step of each iteration.

To simulate the channel, the pre-distortion block needs to oversample the signal by several times the symbol rate in order to avoid spectral aliasing from the non-linear interference. For channels with large memory, the channel simulations can require a high complexity. In the following sections, we describe methods to obtain approximations of the coefficients \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\) with a lower complexity.

_Calculations of the Coefficients \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\) Based on a Reduced Volterra Model_

The coefficients \(A_{k,j}^{n}(1,0)\) and \(A_{k,j}^{n}(0,1)\) can be computed by summing the contribution of each Volterra coefficient. To decrease the algorithm complexity, they can instead be approximated by summing the contributions of only the most significant Volterra coefficients. Let us consider the generic Volterra coefficient \(H_{2m+1}(n_{1}...n_{2m+1})\). Volterra coefficients that do not have at least one index equal to \(n-j\) can be neglected, since only the symbol \(j\) is modified. To further decrease the number of Volterra coefficients, an approximated value of \(A_{k,j}^{n}(m_{1},m_{2})\) can be calculated by truncating the non-linearity order and by limiting the channel length. Truncating the channel length to a given value \(L_{c}^{{}^{\prime}}\) implies that only the Volterra coefficients \(H_{2m+1}(n_{1}...n_{2m+1})\) for which each index \(n_{i}\) satisfies \(|n_{i}|\leq L_{c}\) are considered. Moreover, \(A_{k,j}^{n}(m_{1},m_{2})=0\) for \(|n-j|>L_{c}^{n}\). Differentapproximations are proposed in [16] to further decrease the number of coefficients. In this paper, we further reduce the number of Volterra coefficients by only considering the ones depending on maximum \(2\) different indexes.

_Calculations of the Coefficients \(A^{n}_{k,j}(1,0)\) and \(A^{n}_{k,j}(0,1)\) Using a Look-Up Table_

The idea of this approximation is to pre-compute the values of \(A^{n}_{k,j}(1,0)\) and \(A^{n}_{k,j}(0,1)\) and to store them in a look-up table. Since \(A^{n}_{k,j}(1,0)\) depends on the symbols \([x_{k,j-1}(n-L_{2})\)... \(x_{k,j-1}(n+L_{1})]\), which take on continuous values, an infinite number of pre-computed table entries would need to be stored. Therefore, an approximation of \(A^{n}_{k,j}(1,0)\) is calculated by rounding each value in \([x_{k,j-1}(n-L_{2})\...\ x_{k,j-1}(n+L_{1})]\) to the closest value in \(C\), where \(C=\{c_{1},c_{2}...c_{P}\}\) is a set of \(P\) complex numbers. Considering the channel length \(L_{\text{c}}\), approximately \(P^{L_{\text{c}}}\) values need to be stored. To avoid the complexity of rounding each pre-distorted symbol to the closest value in \(C\), a further approximation can be introduced, considering that the coefficients \(A^{n}_{k,j}(1,0)\) and \(A^{n}_{k,j}(0,1)\) are independent of \(k\). This means that these coefficients are calculated at Iteration \(k\) using the symbols \([s(n-L_{2})\...\ s(n+L_{1})]\) instead of the symbols \([x_{k,j-1}(n-L_{2})\...\ x_{k,j-1}(n+L_{1})]\).

### _Alternative to the Calculation of the Remaining Coefficients \(A^{n}_{k,j}(m_{1},m_{2})\)_

Once the precoded symbols are updated using the lower complexity algorithms proposed in Sections IV-B and IV-C, it is important to check the linearity assumption based on which the algorithms rely. This can be simply done by simulating the actual channel, but we wanted to avoid that in Sections IV-B and IV-C for complexity reasons. A pragmatic approach to keeping the low-complexity advantage is to check the linearity assumption only at the end of each iteration by a single channel simulation. We consider that the linearity assumption is met if the MSE decreases after each iteration of the algorithm. When the Euclidian distance stops decreasing, the algorithm is stopped and the pre-distorted values of the previous iteration are kept as the final values.

### _Complexity Comparison_

In this subsection, the complexity of the small-variation algorithm is compared to that of its reduced-complexity alternatives. In the following, \(\Delta_{k,j}\) and \(\Delta^{*}_{k,j}\) are replaced by \(\Re(\Delta_{k,j})\) and \(\Im(\Delta_{k,j})\) in (15), and the coefficients \(A^{n}_{k,j}(1,0)\) and \(A^{n}_{k,j}(0,1)\) are accordingly modified. This simple notational change allows a (small) complexity decrease. The algorithm consists in \(K\) iterations of \(N\) steps. At each step, the initial algorithm and the reduced-complexity algorithms all require the following operations:

* Calculate the coefficients \(A^{n}_{k,j}(1,0)\) and \(A^{n}_{k,j}(0,1)\) from (15). These coefficients are calculated differently for each method.
* Evaluate \(||\epsilon_{k,j-1}+\mathbf{F}^{Lin}_{k,j}||_{2}\) in (17), with \(\mathbf{F}^{\text{NL}}_{k,j}=\mathbf{F}^{\text{Lin}}_{k,j}\) as defined in (16). The computation of the norm of this vector is obtained by summing the norm of each element of the vector \(\epsilon_{k,j-1}+\mathbf{F}^{Lin}_{k,j}\). It can be shown that this necessitates \(10L_{\text{c}}\) multiplications and \(5(L_{\text{c}}-1)\) additions.
* Find the minimum of (17). Using partial derivatives, this requires the inversion of a \(2\times 2\) (real) matrix, \(4\) multiplications, and \(2\) additions.
* Update the channel outputs for the next step (in fact calculate \(\epsilon_{\mathbf{k},j}\) from \(\epsilon_{\mathbf{k},j-1}\) using \(A^{n}_{k,j}(1,0)\), \(A^{n}_{k,j}(0,1)\) and the applied variation). This requires \(4L_{c}\) multiplications and \(4L_{c}\) additions.

The complexity to determine the linear coefficients depends on the chosen algorithm:

* The complexity of the algorithm using the Volterra model depends on the number of considered Volterra coefficients and on the order of the Volterra coefficient. A Volterra coefficient of order \(p\) requires \(4p\) multiplications and 2 additions. By truncating the channel length to \(L^{{}^{\prime}}_{\text{c}}\), each of the \(L^{{}^{\prime}}_{\text{c}}\) outputs depends on approximately \((L_{\text{c}})^{(p-1)}\) coefficients of order \(p\).
* The method based on channel simulations necessitates three channel simulations. At each channel simulation, \(L_{\text{c}}\) outputs need to be calculated. This requires simulating the power amplifier output for more than \(L_{\text{c}}k_{\text{OSF}}\) input values, where \(k_{\text{OSF}}\) is the oversampling factor. The output of the power amplifier can be obtained by interpolating the AM-AM and AM-PM characteristics or assessed using a polynomial approximation. The number of operations to calculate the power amplifier output is then approximatively proportional to the chosen non-linearity order. The complexity of the convolution with the linear filters also needs to be taken into account, which is proportional to \(L_{\text{c}}^{2}k_{\text{OSF}}\). To calculate the coefficients \(A^{n}_{k,j}(1,0)\) and \(A^{n}_{k,j}(0,1)\) from the channel simulations, \(4\) additions and \(4\) divisions need to be done.
* The method based on look-up tables needs to round \(4L^{{}^{\prime}}_{\text{c}}\) values to the closest value in the look-up table since the \(L^{{}^{\prime}}_{\text{c}}\) complex outputs depend on \(2L^{{}^{\prime}}_{\text{c}}\) inputs.

The method based on the look-up tables is the least complex. The method based on the approximated Volterra model is less complex than the method based on channel simulations only if the number of Volterra coefficients is very small, so that very short channel lengths must be considered. This will be further discussed in the next section.

## V Numerical results

We consider \(32\)-APSK symbols and SRRC shaping and receiver filters. If not specified differently, the roll-off factor is assumed to be equal to \(0.1\). A traveling-wave tube (TWT) amplifier is considered with AM-AM and AM-PM characteristics given in Fig. 2. The IMUX and OMUX characteristics are given in Fig. 3 and Fig. 4 respectively. Their \(3\)-dB cut-off frequency is equal to \(36\) MHz. The low density parity-check (LDPC) encoder and the interleaver are the ones defined in the DVB-S2 standard for the 32-APSK modulation and the code rate equal to 3/4. As discussed in Section III-A, \(N\) is equal to the number of symbols in a PLFRAME of the DVB-S2 standard, which is equal to \(12960\) for the case of 32-APSK modulation. The symbol rate is equal to \(36\)MBauds, so that the channel occupation is equal to \(110\%\) of the theoretical channel bandwidth. This allows increasing the spectral efficiency at the cost of more non-linear interference. Fig. 5 illustrates the MSE between the initial and the received symbols after each iteration of the small-variation algorithm described in Section III for different values of \(\Delta_{max}\), with or without a linear zero-forcing filter. Fig. 5 shows that a better optimum is reached when a linear zero-forcing filter is used so that it will always be considered in the following results. The linear zero-forcing filter is placed at the transmitter. At each step of the algorithm, it is checked that the variation \(\Delta_{k,j}^{\text{applied}}\) decreases the square error so that the algorithm always converges to a local optimum. The value \(\Delta_{max}\) has no impact on the value of the local optimum but controls the convergence speed of the algorithm. Too small values of \(\Delta_{max}\) obviously decrease the speed of convergence of the algorithm. This is also the case for too large values of \(\Delta_{max}\) since it increases the number of steps where no variation is applied. Fig. 6 illustrates the performance reached when the square error decrease is only checked at the end of each iteration (instead of the end of each step) as described in Section IV-D. It can be observed that the asymptotic performance now depends on the considered \(\Delta_{max}\). Sufficiently small values of \(\Delta_{max}\) (\(0.05\) and \(0.1\)) however allow to reach similar performance as in previous figure.

Table I shows the performance loss associated to the reduced-complexity alternatives of the small-variation algo

Fig. 4: OMUX characteristics.

Fig. 5: Mean-square error (MSE) after each iteration of the small-variation algorithm, symbol rate\(=36\) MSymb/s.

Fig. 3: IMUX characteristics.

Fig. 2: AM-AM and AM-PM characteristics of the HPA.

rithm, proposed in Section IV-B and IV-C. For both approximations, the performance loss decreases with the IBO. Considering \(L_{c}^{{}^{\prime}}=5\) allows a small performance increase compared to \(L_{c}^{{}^{\prime}}=3\). Slightly better performance is achieved with the method based on look-up tables, which necessitates a look-up table of \(L_{c}^{{}^{\prime}}\times 32^{L_{c}^{{}^{\prime}}}\) entries. The method based on a reduced Volterra model however does not require any pre-computation and still allows a decrease in complexity compared to the method based on channel simulations. Considering \(L_{c}^{{}^{\prime}}=3\), each step of each iteration requires about \(60\) multiplications and \(30\) additions, relying on the fact that some products of the pre-distorted symbols can be reused to calculate different channel outputs. Using channel simulations with \(L_{c}^{{}^{\prime}}=3\) and an oversampling factor equal to 8, \(40\) samples need to be filtered by the shaping and IMUX filters, interpolated, and re-filtered by the OMUX filter and the receiver filter. Considering that the shaping and IMUX filters (and OMUX and receiver filters) have an impulse response longer than \(40\) samples, this means that already \(40^{2}\) multiplications are involved for each convolution. Clearly, the complexity is lower using the Volterra model instead of channel simulations.

Fig. 7 compares the small-variation algorithm and its reduced-complexity alternatives to state-of-the-art algorithms. The comparison is performed based on the total degradation, described in Section II-C, as a function of the OBO. The target BER is equal to \(10^{-5}\). Two state-of-the-art methods are considered for the comparison. The first method is based on memory polynomials, where the pre-distorter is a reduced Volterra system presented in [16]. Third order Volterra coefficients and a pre-distorter length \(L_{c}^{{}^{\prime}}=9\) have been considered. The second method is the one proposed in [20], where the value of each pre-distorted symbol is a function of the neighboring un-pre-distorted symbols. All possible combinations are pre-computed offline and stored in a look-up table. A pre-distorter length \(L_{c}^{{}^{\prime}}=3\) is considered so that \(32^{3}\) entries are stored in the look-up table. Among all pre-distortion methods, this approach has the lowest real-time complexity, since only one memory access per symbol needs to be performed. Moreover, Fig. 7 shows that it outperforms the first state-of-the art method in the considered scenario. Fig. 7 also shows that the small-variation algorithm and the reduced-complexity alternatives outperform the state-of-the-art algorithms. About \(1.2\)dB is gained on the optimum total degradation point. The performance of the reduced-complexity alternatives of the small-variation algorithm is assessed assuming also a pre-distorter length equal to \(L_{c}^{{}^{\prime}}=3\). The loss of the reduced-complexity alternatives on the optimum total degradation point is on the other hand smaller than \(0.2\)dB.

Fig. 8 considers an increased symbol rate equal to \(38\)MHz

Fig. 6: Mean-square error (MSE) after each iteration of the small-variation algorithm, using the convergence method described in Section IV-D, symbol rate\(=36\) MSymb/s.

Fig. 7: Total degradation for small-variation algorithm (SVA) and state-of-the-art pre-distortion methods, symbol rate\(=36\) MSymb/s, roll-off\(=0.1\).

and a reduced roll-off factor equal to \(0.05\), simulating therefore a higher interference scenario. As a result, the total degradation using the small-variation algorithm is higher for every OBO when compared to the previous case. The 2 state-of-the-art methods give similar performance. The gain compared to these state-of-the-art algorithms is higher than in previous case and is about \(2\)dB. The reduced-complexity alternatives reach again almost the same optimum total degradation.

## VI Conclusion and future work

This paper proposes a new iterative pre-distortion algorithm suited to the use of high-order modulations on a highly non-linear satellite communication channel. The algorithms aims at minimizing the Euclidian distance between the transmitted and received symbols. The pre-distorted symbols are updated at each iteration based on a linear approximation of the channel output variation, which is only valid if the symbol update is kept sufficiently local. However, a major issue of the algorithm is the complexity involved in the estimation of the linear relation between the channel input and output variations. Two approximations have been proposed to strongly decrease the algorithm complexity. The first one relies on a reduced Volterra model and the second one is based on the use of look-up tables.

The performance improvement brought by the algorithm, compared to state-of-the-art algorithms, represents several dBs on the MSE and \(1\) to \(2\)dBs on the link budget with \(32\)-APSK modulation. The channel occupancy bandwidth is equal to \(110\%\) of the theoretical channel bandwidth to improve the spectral efficiency. Roll-off factors as low as \(0.05\) have been considered. The performance improvement is obtained at the cost of a complexity increase. The choice of the pre-distortion algorithm is therefore a performance/complexity trade-off. Future work will include the algorithm extension to the case where more than one carrier is amplified by the same power amplifier. If the channel is known and if all signals are transmitted from the same hub, a pre-distortion algorithm similar to the one proposed here for a single carrier per channel can be applied.

Appendix A Calculation of the coefficients \(A_{k,j}^{n}(m_{1},m_{2})\) for some simple Volterra models

Let us first consider a channel consisting only of the third-order Volterra coefficient \(H_{3}(0,0,0)\). Each element of the difference between the output \(\mathbf{y}(\mathbf{x}_{\mathbf{k},\mathbf{j}-1}+\mathbf{\Delta_{k},\mathbf{j}})\) and the output \(\mathbf{y}(\mathbf{x}_{\mathbf{k},\mathbf{j}-1})\) is given by:

\[F_{k,j}^{\text{NL}}(j) =H_{3}(0,0,0)\{|x_{k,j-1}(j)+\Delta_{k,j}|^{2}[x_{k,j-1}(j)+ \Delta_{k,j}]\] \[\qquad\qquad\qquad-|x_{k,j-1}(j)|^{2}x_{k,j-1}(j)\}\] \[=H_{3}(0,0,0)[x_{k,j-1}(j)^{2}\Delta_{k,j}^{2}+2|x_{k,j-1}(j)|^{ 2}\Delta_{k,j}\] \[+2x_{k,j-1}(j)|\Delta_{k,j}|^{2}+x_{k,j-1}(j)^{*}\Delta_{k,j}^{2 }+|\Delta_{k,j}|^{2}\Delta_{k,j}]. \tag{24}\]

The other outputs are not modified since the channel is memoryless. The different coefficients \(A_{k,j}^{n}(m_{1},m_{2})\) can be directly estimated from (24), and are given in the second column of Table II. The third and fourth columns of Table II give the non-zero values for \(A_{k,j}^{n}(m_{1},m_{2})\), considering a channel with a single Volterra coefficient respectively equal to \(H_{3}(1,0,0)\) and \(H_{3}(0,1,2)\). It should be noticed that more than one input is now modified, due to the memory of the system. Moreover, the output variation for \(H_{3}(0,1,2)\) is linear in \(\Delta_{k,j}\) because all indexes of this Volterra coefficient are different.

## Appendix B Proof of (20)

By definition of \(\Delta_{k,j}^{\text{Lin}}\), we have that:

\[[||\epsilon_{k,j-1}+\mathbf{F}_{k,j}^{\text{Lin}}|_{2}|\Delta_{k, j}=\Delta_{k,j}^{\text{Lin}}]=\] \[||\epsilon_{k,j-1}||_{2}+\sum_{n}|A_{k,j}^{n}(1,0)\Delta_{k,j}^{ \text{Lin}}+A_{k,j}^{n}(0,1)(\Delta_{k,j}^{\text{Lin}})^{*}|^{2}\] \[\qquad+2\Re\{\epsilon_{k,j-1}(n)^{*}[A_{k,j}^{n}(1,0)\Delta_{k,j}^ {Lin}+A_{k,j}^{n}(0,1)(\Delta_{k,j}^{Lin})^{*}]\}\] \[\leq||\epsilon_{k,j-1}||_{2}. \tag{25}\]

Therefore, we have that the second line of (25) is negative and that:

\[\sum_{n}|A_{k,j}^{n}(1,0)\Delta_{k,j}^{Lin}+A_{k,j}^{n}(0,1)(\Delta _{k,j}^{Lin})^{*}|^{2}\] \[\leq-2\Re[\epsilon_{k,j-1}^{Lin}(n))^{*}(A_{k,j}^{n}(1,0)\Delta_{ k,j}+A_{k,j}^{n}(0,1)(\Delta_{k,j}^{Lin})^{*}]. \tag{26}\]

Since \(\gamma^{2}<\gamma\), it is easy to see that:

\[[||\epsilon_{k,j-1}+\mathbf{F}_{k,j}^{\text{Lin}}||_{2}|\Delta_{k, j}=\Delta_{k,j}^{\gamma}]=||\epsilon_{k,j-1}||_{2}\] \[\qquad+\gamma^{2}\sum_{n}|A_{k,j}^{\text{Lin}}(1,0)\Delta_{k,j}^ {\text{Lin}}+A_{k,j}^{n}(0,1)(\Delta_{k,j}^{\text{Lin}})^{*}|^{2}\] \[\qquad+2\gamma\Re\{\epsilon_{k,j-1}(n)^{*}[A_{k,j}^{n}(1,0)\Delta _{k,j}^{Lin}+A_{k,j}^{n}(0,1)(\Delta_{k,j}^{Lin})^{*}]\}\] \[\leq||\epsilon_{k,\mathbf{j}-1}||_{2}. \tag{27}\]

## References

* [1] [PERSON], [PERSON], and [PERSON], \"Channel shortening for nonlinear satellite channels,\" _IEEE Commun. Lett._, vol. 16, no. 12, pp. 1929-1932, Dec. 2012.
* [2] [PERSON] and [PERSON], \"Novel siso detection algorithms for nonlinear satellite channels,\" _IEEE Commun. Lett._, vol. 1, no. 1, pp. 22-25, Feb. 2012.
* [3] [PERSON] and [PERSON], \"Optimal channel shortening for mimo and isi channels,\" _IEEE Trans. Commun._, vol. 11, no. 2, pp. 810-818, Feb. 2012.
* [4] [PERSON] and [PERSON], \"Performance of Volterra and MLSD receivers for nonlinear band-limited satellite systems,\" _IEEE Trans. Commun._, vol. 48, no. 7, pp. 1171-1177, Jul. 2000.
* [5] [PERSON], [PERSON], and [PERSON], \"Nonlinear channel equalization with Gaussian processes for regression,\" _IEEE Trans. Signal Process._, vol. 56, no. 10, pp. 5283-5286, Oct. 2008.
* [6] [PERSON], [PERSON], and [PERSON], \"Joint nonlinear channel equalization and soft LDPC decoding with Gaussian processes,\" _IEEE Trans. Signal Process._, vol. 58, no. 3, pp. 1183-1192, Mar. 2010.
* [7] [PERSON] and [PERSON], \"Intersymbol interference cancellation for 16 QAM transmission through nonlinear channels,\" in _Proc. 10 th IEEE Digital Signal Processing Workshop and 2 nd Signal Processing Education Workshop_, Oct 2002, pp. 322-326.

* [8] [PERSON], [PERSON], and [PERSON], \"Reduced-complexity BCJR algorithm for turbo equalization,\" _IEEE Trans. Commun._, vol. 55, no. 12, pp. 2279-2287, Dec. 2007.
* [9] [PERSON], [PERSON], and [PERSON], \"RF power amplifier linearization through amplitude and phase predistortion,\" _IEEE Trans. Commun._, vol. 44, no. 11, pp. 1477-1484, Dec. 1996.
* [10] [PERSON] and [PERSON], \"Digital predistortion for power amplifiers using separable functions,\" _IEEE Trans. Signal Process._, vol. 58, no. 8, pp. 4121-4130, Aug. 2010.
* [11] [PERSON], [PERSON], [PERSON], and [PERSON], \"Adaptive fractional predistortion techniques for satellite systems based on neural networks and tables,\" in _Proc. 65 th IEEE Vehicular Technology Conference (VTC 2007-Spring)_, Apr. 2007, pp. 1400-1404.
* [12] [PERSON] and [PERSON], \"A neural network pre-distorter for the compensation of HPA nonlinearity: application to satellite communications,\" in _4 th IEEE Consumer Communications and Networking Conference (CCNC 2007)_, Jan. 2007, pp. 465-469.
* [13] [PERSON], _The Volterra and Wiener Theories of Nonlinear Systems_. New York: Wiley, 1980.
* [14] [PERSON] and [PERSON], \"An adaptive Volterra predistorter for the linearization of RF high power amplifiers,\" in _IEEE MTT-S International Microwave Symposium Digest_, vol. 1, 2002, pp. 461-464.
* [15] [PERSON], [PERSON], and [PERSON], \"Adaptive predistortion of nonlinear Volterra systems using spectral magnitude matching,\" in _Proc. IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP 2009)_, Apr. 2009, pp. 2985-2988.
* [16] [PERSON], [PERSON], [PERSON], [PERSON], and [PERSON], \"A generalized memory polynomial model for digital predistortion of RF power amplifiers,\" _IEEE Trans. Signal Process._, vol. 54, no. 10, pp. 3852-3860, Oct. 2006.
* [17] [PERSON] and [PERSON], \"A reconsideration of the pth-order inverse predistorter,\" in _Proc. 49 th IEEE Vehicular Technology Conference_, vol. 2, 1999, pp. 1501-1504.
* [18] [PERSON] and [PERSON], \"Digital transmission over nonlinear channels,\" in _Principles of Digital Transmission: With Wireless Applications_, ser. Information Technology: Transmission, Processing, and Storage. Springer US, 2002, pp. 725-772.
* [19] [PERSON] and [PERSON], \"A data predistortion technique with memory for QAM radio systems,\" _IEEE Trans. Commun._, vol. 39, no. 2, pp. 336-344, 1991.
* [20] [PERSON], [PERSON], and [PERSON], \"DVB-S2 modem algorithms design and performance over typical satellite channels,\" _International Satellite Commun. and Netw._, vol. 22, no. 3, pp. 281-318, May 2004.
* [21] \"Digital Video Broadcasting (DVB): Second Generation Framing Structure, Channel Coding and Modulation Systems for Broadcasting, Interactive Services, News Gathering and Other Broadband Satellite Applications (DVB-S2),\" _ETSI EN 302 307, VI.2.1_, Apr. 2009.
* [22] [PERSON] and [PERSON], \"Analysis and compensation for nonlinear interference of two high-order modulation carriers over satellite link,\" _IEEE Trans. Commun._, vol. 58, no. 6, pp. 1824-1833, Jun. 2010.
* [23] [PERSON] and [PERSON], \"Trust-Regions Methods,\" in _Numerical Optimization_, ser. Operations Research and Financial Engineering. Springer, 2006, pp. 64-99.