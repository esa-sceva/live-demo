Communication Constellation Design of Minimum Number of Satellites With Continuous Coverage and Inter-Satellite Link

[PERSON]

 [PERSON]

Footnote 1: PhD Candidate, Department of Astronomy, Yonsei University, 50 Yonsei-ro, Seodaemun-gu, 614A Science building, Seoul, Korea.

Footnote 2: Professor, Department of Astronomy, Yonsei University, 50 Yonsei-ro, Seodaemun-gu, 624 Science building, Seoul, Korea.

###### Abstract

The recent advancement in research on distributed space systems that operate a large number of satellites as a single system urges the need for the investigation of satellite constellations. Communication constellations can be used to construct global or regional communication networks using inter-satellite and ground-to-satellite links. This study examines two challenges of communication constellations: continuous coverage and inter-satellite link connectivity. The bounded Voronoi diagram and APC decomposition are presented as continuous coverage analysis methods. For continuity analysis of the inter-satellite link, the relative motion between adjacent orbital planes is used to derive analytic solutions. The Walker-Delta constellation and common ground-track constellation design methods are introduced as examples to verify the analysis methods. The common ground-track constellations are classified into quasi-symmetric and optimal constellations. The optimal common ground-track constellation is optimized using the BILP algorithm. The simulation results compare the performance of the communication constellations according to various design methods.

**AAS 25-254**

## Introduction

In recent years, the feasibility of low Earth orbit communication satellites has attracted attention owing to the trend of small satellites. Examples include Space-X's Starlink, Eutelsat's OneWeb, and Amazon's Kuiper projects.[1] Their orbits are designed to provide communication links across the Earth. A satellite constellation operates several satellites with distinct orbits in a single system. Compared with conventional geostationary satellites, low Earth orbit satellites have a smaller coverage size and shorter orbital periods, resulting in degraded spatial and temporal coverage performance. Therefore, low Earth orbit constellations operate several satellites to overcome this limitation while minimizing the number of satellites. If the coverage is continuous in the area of interest, the communication constellation can continuously provide communication links. In addition, when the inter-satellite links are connected, the link is not disconnected even by the orbital motion of the satellite and the Earth's rotation effect. In this study, the low Earth orbit communication constellation design problem was interpreted as the problem of achieving continuous coverage and inter-satellite links.

The sections are presented in the following order: constellation design methods, coverage analysis methods, relative motion in adjacent orbital planes, simulation results, and conclusions. Constellation design methods describe the basis of Walker and common ground-track constellations.

The Walker constellation first introduces the concept of a seed satellite and its design parameters, and defines the orbital elements. The pattern repetition period and duplicate allocation of orbital elements are explained as two important characteristics of the Walker-Delta constellation, and are expressed by the design parameters. The repeat ground-track orbit is the seed satellite orbit for a common ground-track constellation. The quasi-symmetric method configures satellites such that the spacing between adjacent satellites is almost equal. The BILP method optimizes the satellite configuration to satisfy the coverage requirements while minimizing the total number of satellites. The coverage analysis methods section first explains a useful concept: the geometry of the Earth's coverage. Then, Voronoi tessellation and APC decomposition are described with the references. The relative motion in adjacent orbital planes derives the key formulae to analyze the bounds of the relative distance. The simulation results present the continuous coverage analyses for the Walker-Delta, quasi-symmetric, and BILP constellations, and the inter-satellite link continuity analyses for the three constellations. The last section summarizes and concludes the contents of this paper.

## 2 Constellation Design Methods

### Walker Constellation

The Walker constellation is a geometric design method that symmetrically configures the orbits [2, 3]. The seed satellite determines the common orbital elements of the constellation. For the Walker constellation, the satellites are configured in circular orbits with the same semi-major axis (\(a\)), inclination (\(i\)), and argument of perigee (\(\omega\)) of the seed satellites. The two types of Walker constellations are classified according to their inclinations. The Walker-Star constellation is designed based on a polar orbit and achieves global coverage. On the other hand, the Walker-Delta constellation has an inclination under 90 degrees and covers the mid-latitude and equator regions. Therefore, this classification is relevant only to the latitude of the area of interest (AoI).

The three design parameters are the total number of satellites (\(T\)), number of orbital planes (\(P\)), and phasing parameter (\(F\in\{0,1,...,P-1\}\)). The number of satellites per orbital plane (\(S=T/P\)) is an auxiliary parameter used to prevent confusion. The right ascension of ascending node (RAAN, \(\Omega_{m}\)) and mean anomaly (\(M_{m,n}\)) of the \(n\)th satellite in the \(m\)th orbital plane (\(SAT_{m,n}\)) are defined by

Figure 1: **Geometric description of the orbital elements of the Walker-Delta constellation**

Eqs. (1) and (2), as shown in Figure 1.

\[\Omega_{m}=\frac{360}{P}\cdot\left(m-1\right)\mathrm{deg} \tag{1}\]

\[M_{m,n}=\frac{360}{T}\cdot F\cdot\left(m-1\right)+\frac{360}{S}\cdot\left(n-1 \right)\mathrm{deg} \tag{2}\]

where \(m=1,2,...,P\) and \(n=1,2,...,S\).

From the Eq. (1), the RAAN is equally spaced by \(\Delta\Omega=360/P\) deg in the range \(\Omega_{m}\in\left[0,360\right]\) deg. The intraplane spacing \(\Delta M=360/S\) deg generates a symmetric location in the orbital plane in the range \(M\in\left[0,360\right]\) deg and is equivalent to the relative angular distance between the satellites in the orbital plane. The relative argument of the latitude (\(\Delta u\)) in the adjacent orbital planes is derived as \(\Delta u=360/T\cdot F\) deg from Eq. (2).

Pattern Repetition PeriodThe Walker-Delta pattern has geometric characteristics such that the intra- and inter-plane angular spacings are homogeneous. This geometric symmetry determines the pattern repetition period. The investigation of patterns in a geographical coordinate system enhances the understanding of the pattern repetition period. Reference 4 derived the formulas for the pattern repetition period. The pattern unit (PU), which is introduced to understand the orbital configuration of the Walker-Delta constellation, is defined as follows:[2, 3]

\[1\mathrm{PU}=\frac{360}{T}\,\mathrm{deg} \tag{3}\]

The RAAN and mean anomaly in Eqs. (1) and (2) are reorganized in PU as

\[\Omega_{m}=S\,\cdot\left(m-1\right)\mathrm{PU} \tag{4}\]

\[M_{m,n}=F\cdot\left(m-1\right)+P\cdot\left(n-1\right)\mathrm{PU} \tag{5}\]

The time interval in which the mean anomaly increases for \(F\) PU is the first pattern repetition period \(t_{F}\) and defined as

\[t_{F}=F\cdot\frac{360}{T}\cdot\frac{1}{\omega_{orb}}\mathrm{sec} \tag{6}\]

where \(\omega_{orb}\) denotes the orbital angular speed. Assuming the twobody motion, the RAAN and mean anomaly at \(t_{F}\) are derived as

\[\Omega_{m}\left(t_{F}\right)=\Omega_{m}\left(t_{0}\right)=S\,\cdot\left(m-1 \right)\mathrm{PU} \tag{7}\]

\[M_{m,n}\left(t_{F}\right)=M_{m,n}\left(t_{0}\right)+F=F\cdot m+P\cdot\left(n- 1\right)\mathrm{PU} \tag{8}\]

where \(t_{0}\) denotes the epoch time.

From Eqs. (7) and (8), the mean anomaly of the \(n\)th satellite in \(m\)th orbital plane at \(t_{F}\), \(M_{m,n}\left(t_{F}\right)\), is the same as the one of the \(n\)th satellite in \(\left(m+1\right)\)th orbital plane at \(t_{0}\), \(M_{m+1,n}\left(t_{0}\right)\). Thus, the constellation pattern observed at \(t_{F}\) appears as a pattern at \(t_{0}\) that is shifted westward as \(\Delta\Omega\) deg.

On the other hand, the mean anomaly propagates \(P\) PU during \(t_{P}\) and defines the second pattern repetition period as

\[t_{P}=P\cdot\frac{360}{T}\cdot\frac{1}{\omega_{orb}}\mathrm{sec} \tag{9}\]The RAAN and the mean anomaly at \(t_{P}\) are derived as

\[\Omega_{m}\left(t_{P}\right)=\Omega_{m}\left(t_{0}\right)=S\cdot\left(m-1\right) \mathrm{PU} \tag{10}\]

\[M_{m,n}\left(t_{P}\right) =F\cdot\left(m-1\right)+P\cdot n\mathrm{PU} \tag{11}\] \[=M_{m,n+1}\left(t_{0}\right)\]

Let us define the set of satellites in the \(m\)th orbital plane as \(\mathbf{N}=\left\{n\mid n=1,2,...,S\right\}\). Then, Eqs. (10) and (11) derive

\[M_{m,\mathbf{N}}\left(t_{P}\right)=M_{m,\mathbf{N}}\left(t_{0}\right). \tag{12}\]Therefore, the constellation pattern at \(t_{P}\) appears identical to the one at \(t_{0}\).

Figure 2 shows the Walker-Delta constellation pattern for \(i\): \(T/P(S)/F=42\): \(120/20(6)/1\) in the geographic coordinate frame. The marks are subsatellite points; \(+\), \(\bullet\), and \(\circ\) represent \(SAT_{1,1}\), \(SAT_{\text{M},1}\), and the remaining satellites, respectively, where \(\mathbf{M}=\{m|m=1,2,...,P\}\) is the set of orbital plane numbers. The blue line represents the bounded Voronoi diagram for the mid-latitude and equatorial regions, which will be described in the next section. \(SAT_{1,1}\) is barely moved in the middle panel compared to the one in the top panel because \(t_{F}\) is only 54 seconds. However, the blue diagrams show that the entire constellation moves westward for \(\Delta\Omega=18.00\) deg. The bottom panel shows the pattern at \(t_{P}\), which is 18 min and 14 s. The position of each satellite in the bottom panel is propagated for \(t_{P}\) from the top panel; however, the patterns of the top and bottom panels are the same.

_Duplicate Allocation of Orbital Elements_ The Walker-Delta design method allocates the six unique orbital elements to each satellite, and the six orbital elements correspond to the unique orbital state of the six positions and velocity elements. This suggests the possibility of duplicate satellite positions and implies the collision between satellites. The conditions of the duplicate orbital elements of the Walker-Delta constellation are investigated in reference 4 as

\[\begin{cases}\Omega_{m^{\prime},n^{\prime}}-\Omega_{m,n}=180\deg\\ M_{m^{\prime},n^{\prime}}-M_{m,n}=180\deg.\end{cases} \tag{13}\]

Equation (13) can be expressed by the Walker-Delta design parameters as follows:

\[\begin{cases}m^{\prime}=1+\frac{P}{2}\\ n^{\prime}=mod\left(1+\frac{S-F}{2},S\right)+S\cdot\delta\left(mod\left(1+ \frac{S-F}{2},S\right),0\right).\end{cases} \tag{14}\]

where \(mod\left(x,y\right)\) denotes the modulo operation, which returns the remainder when \(x\) is divided by \(y\), and \(\delta\left(x,y\right)\) represents the Kronecker delta function, which equals 1 if \(x=y\) and 0 otherwise. Therefore, the Walker-Delta design parameters that accommodate Eq. (14) must be avoided in the design procedure.

#### Common Ground-track Constellation

Repeat Ground-track OrbitThe repeat ground-track (RGT) orbit is an orbit that traces the same ground-track within a specific time interval. The two main parameters that determine the RGT orbit are the number of revolutions to repeat (\(N_{P}\)) and the number of days to repeat (\(N_{D}\)).[5] For example, if the number of revolutions to repeat is 14 and the number of days to repeat is 1, the ground-track crosses (ascends or descends) the equator 14 times in one day. Thus, the period ratio (\(\
u\)), which is the RGT design parameter, is formulated as

\[\
u=N_{P}/N_{D} \tag{15}\]

The period ratio can also be described by the satellite nodal period (\(T_{S}\)) and the nodal period of Greenwich (\(T_{G}\)). The change in the orbital elements due to \(J_{2}\) effect induces changes in \(T_{S}\) and \(T_{G}\) as

\[T_{S} =\frac{2\pi}{\dot{\omega}+\dot{M}} \tag{16}\] \[T_{G} =\frac{2\pi}{\omega_{E}-\dot{\Omega}} \tag{17}\]where \(\omega_{E}\) is Earth's rotation speed.

The orbital elements are formulated using Eqs. (18), (19), and (20):

\[\dot{\omega}=\frac{3}{2}J_{2}\frac{{R_{E}}^{2}}{p}\sqrt{\frac{{\mu_{E}}}{a^{3}}} \left(2-\frac{5}{2}\sin i^{2}\right) \tag{18}\]

\[\dot{M}=\sqrt{\frac{{\mu_{E}}}{a^{3}}}\left(1-\frac{3}{2}J_{2}\left(\frac{R_{E} }{p}\right)^{2}\sqrt{1-e^{2}}\left(\frac{3}{2}\sin i^{2}-1\right)\right) \tag{19}\]

\[\dot{\Omega}=-\frac{3}{2}J_{2}\left(\frac{R_{E}}{p}\right)^{2}\sqrt{\frac{{ \mu_{E}}^{2}}{p}^{2}}\cos i \tag{20}\]

Based on the definition of period ratio, Eqs. (16) and (17) derive Eq. (15) with respect to the orbital elements as:

\[\
u=\frac{{N_{P}}}{{N_{D}}}=\frac{{T_{G}}}{{T_{S}}}=\frac{{\dot{\omega}+\dot{ M}}}{{\omega_{E}-\dot{\Omega}}} \tag{21}\]

From Eqs. (18), (19), and (20), the orbital elements have arguments as \(\dot{\omega}=\dot{\omega}\left(a,i,e\right)\), \(\dot{M}=\dot{M}\left(a,i,e\right)\), and \(\dot{\Omega}=\dot{\Omega}\left(a,i,e\right)\). It organizes the arguments of \(T_{S}\), \(T_{G}\), and \(\
u\) as:

\[T_{S}=T_{S}\left(a,e,i\right) \tag{22}\]

\[T_{G}=T_{G}\left(a,e,i\right) \tag{23}\]

\[\
u=\
u\left(a,e,i\right) \tag{24}\]

From this, the RGT orbital design algorithm can be derived. Given the specific \(\
u\), inclination (\(i\)), and eccentricity (\(e\)), the algorithm calculates the corresponding semi-major axis (a). Equation (15) implies that \(\
u\) determines the number of revolutions per period and suggests that \(\
u\) is related to the orbital period and semi-major axis. Consequently, when \(e\) and \(i\) are specified, one unique semi-major axis is derived from \(\
u\) and vice versa. For example, if the set of RGT orbital elements is given as \((\
u,i,e)=(14,42\deg,0)\), then \(a\) is \(7201.90 km\). As a result, the RGT orbital elements can be described in two different ways, such as \((a,i,e)=(7201.90 km,42\deg,0)\), and then \(\
u\) is uniquely determined as 14.

_Common Ground-track Constellation_ The RGT orbit that is designed according to Eqs. (21) contains a set of \((\
u,i,e)\) or \((a,i,e)\) with an arbitrary set of \((\omega,\Omega,M)\). From here on, the orbital elements of the RGT orbit are denoted as \((\
u,i,e)\) except for specific purposes. This implies that a numerous number of satellites can trace the same ground-track and introduces the concept of a common ground-track (CGT) constellation. The CGT constellation is designed following the three procedures below: [6, 7]

(1) Calculate the semi-major axis (\(a\)) of the seed satellite from \((\
u,i,e)\) in Eq. (21).

(2) Choose an arbitrary \(\omega\) so that all satellites have the same \((\
u,i,e,\omega)\).

(3) Given the CGT constellation's total number of satellites (\(T\)), the \(k\)th satellite's RAAN and mean anomaly (\(\Omega_{k}\), \(M_{k}\)) satisfy Eq. (25)

\[N_{P}\Omega_{k}+N_{D}M_{k}=constant\mod 2\pi \tag{25}\]

where \(k=1,...,T\).

The CGT constellation design problem is concluded as the configuration method of \((\Omega_{k},M_{k})\) following procedure (3). The reference 7 introduces two methods, quasi-symmetric and binary integer programming (BILP).

_Quasi-symmetric Method_ The simulation time (\(T_{sim}\)) is discretized by the step size \(t_{step}\) and is assumed to be an integer multiple of the repetition period. Thus, this can be formulated as \(T_{sim}=L\cdot t_{step}\). The continuous time variable \(t\in[0,T_{sim}]\) is converted into the discretized time variable \(\tau\in\{0,1,...,L-1\}\). The configuration of the satellites in the CGT constellation can be expressed as time-shifted seed satellites because all satellites have the same ground-track traces. Therefore, the constellation pattern vector \(x\left[\tau\right]\) can be defined as follows:

\[x\left[\tau\right]\triangleq\begin{cases}1&\text{if }\tau=\tau_{k},\\ 0&\text{otherwise}.\end{cases} \tag{26}\]

where \(\tau_{k}\) is the temporal location of the \(k\)th satellite.

In the discretized time domain, the constellation pattern vector has length \(L\). If the total number of constellations is \(T\), then the spacing constant \(\xi\) is defined as follows:

\[\xi\triangleq\frac{L}{T}. \tag{27}\]

If \(\xi\) is an integer, \(\tau_{k}\) is equally spaced and the satellites are configured symmetrically. In contrast, if \(T\) is not a divisor of \(L\), then \(\xi\) is not an integer that makes the index \(\tau_{k}\) a rational number. In this case, only a quasi-symmetric configuration is possible. The formulation for both symmetric and quasi-symmetric constellation pattern vectors \(\overline{x}\left[\tau\right]\) is defined as

\[\overline{x}\left[\tau\right]\triangleq\sum_{k=1}^{T}\delta\left[nint\left( \tau-\xi\left(k-1\right)\right)\right] \tag{28}\]

where \(nint\) denotes the nearest integer function.

_Binary Integer Linear Programming Method_ Because the domain of the constellation pattern vector is defined as binary, the BILP method is introduced as an optimization algorithm. The BILP algorithm is a variant of the linear programming method that optimizes a linearized objective function with constraints and boundaries. The problem statement of the linear programming can be generalized as[8]

\[\min_{x}\boldsymbol{c}^{T}\boldsymbol{x}\text{ subject to }\begin{cases} \mathbf{A}\cdot\boldsymbol{x}\leq\boldsymbol{b}\\ \mathbf{A}_{eq}\cdot\boldsymbol{x}=\boldsymbol{b}_{eq}\end{cases} \tag{29}\]

where \(\boldsymbol{x}\) is the decision variable of length \(L\), \(\boldsymbol{c}^{T}\boldsymbol{x}\) is the objective function, \(\mathbf{A}\in\mathbb{R}^{Q\times L}\) and \(\boldsymbol{b}\in\mathbb{R}^{Q}\) are the matrix and vector that constitutes the \(Q\) numbers of inequality constraints, \(\mathbf{A}_{eq}\in\mathbb{R}^{R\times L}\) and \(\boldsymbol{b}\in\mathbb{R}^{R}\) are the matrix and vector of \(R\) numbers of equality constraints.

In addition to Eq. (29), the domain of the decision variable \(\boldsymbol{x}\) must be defined. The domain sets \(\mathbb{R}_{\geq 0}\), \(\mathbb{Z}_{\geq 0}\), and \(\mathbb{Z}_{2}\) induce the pure real and binary integer linear programming. It is also possible for mixed-integer linear programming to include both real and integer decision variables. Thus, the BILP has the same problem statement but constrains the domain of the decision variables as

\[\boldsymbol{x}\in\mathbb{Z}_{2}^{L} \tag{30}\]

The objective of optimization is to obtain a constellation pattern vector that minimizes the number of satellites while satisfying the coverage requirement. Because the summation of \(x\left[\tau\right]\) is equal to \(T\) by the definition of the constellation pattern vector in Eq. (26), the problem is formulated as

\[\min_{x}\mathbf{I}^{T}\mathbf{x}\text{ subject to }\begin{cases}\mathbf{V}_{0,j}\mathbf{x} \geq&\mathbf{f}_{j},\quad\forall j\in\mathcal{J}\\ \mathbf{x}\in\mathbb{Z}_{2}^{L}\end{cases} \tag{31}\]

where \(j\) is the index for the \(j\)th grid, \(\mathcal{J}\) is the set of grids in the area of interest, and \(\mathbb{Z}_{2}\) is the binary integer number set. The matrix \(\mathbf{V}_{0,j}\in\mathbb{Z}_{2}^{L\times L}\) is a seed-satellite access profile circulant matrix, which is addressed in detail in the next section.

## Coverage Analysis Methods

### Geometry of Earth Coverage

Figure (a)a shows the geometric relationships between the satellite, coverage edge, and center of the Earth and is advantageous for coverage analysis. The true horizon is tangential from the satellite to the Earth's surface. The angle between the true horizon and the subsatellite point (SSP) is called the maximum Earth central angle (ECA, \(\lambda_{0}\)) or the angular radius of the Earth (\(\rho\)) when measured from the center of the Earth and the satellite, respectively. When the satellite is located at an altitude of h km, the angular radius of the Earth is determined using Eq. (32):

\[\sin\rho=\frac{R_{E}}{R_{E}+h} \tag{32}\]

where \(R_{E}\) is the Earth's radius.

Usually, the payload's coverage determines the coverage performance of a single satellite that constitutes the constellation. The Earth central angle (\(\lambda\)) measures the size of payload coverage (\(\eta\)) on the Earth's surface and is defined as the angular distance between the SSP and the coverage edge. The coverage edge is the rim of the satellite coverage on the Earth. The elevation angle (\(\varepsilon\)) is measured at the coverage edge from the local horizontal to the satellite.

The coverage can be approached from two perspectives: the satellite and the target area (Figure (b)b). When considering the satellite perspective, it is important to evaluate payload's specifications. According to the definition of the coverage, the nadir angle (\(\eta=\eta(t)\)) should be smaller than

Figure 3: (a) Geometric relationships between the satellite, coverage edge, and center of the Earth and (b) geometric description of coverage

the payload beam coverage (\(\eta_{Max}\)). From the target point perspective, it is considered to be covered when the elevation angle of the satellite (\(\varepsilon=\varepsilon(t)\)) is greater than the target point's minimum elevation angle (\(\varepsilon_{min}\)).

The trigonometry of the blue shaded triangle in Figure 3a yields the formulae for \(\eta\), \(\varepsilon\), and \(\lambda\) as Eqs. (33) and (34).

\[\cos\varepsilon=\sin\eta/\sin\rho \tag{33}\]

\[\lambda=90\deg-\eta-\varepsilon \tag{34}\]

For communication constellations, constraints are imposed on both the payload specification and the elevation angle of the target point. Therefore, the trigonometry of Eqs. (33) and (34) is crucial, as it prevents redundant computational complexity. For example, suppose that the beam coverage of the spacecraft (\(\eta_{Max}\)) is \(45\deg\), and the ground station has a minimum elevation angle (\(\varepsilon_{min}\)) of \(30\deg\). If the satellite's altitude is \(1,200\) km, the angular radius of Earth (\(\rho\)) is \(57.31\deg\). The Eq. (33) immediately converts the payload's coverage to the elevation angle as

\[\overline{\varepsilon}=\arccos\left(\sin\eta_{Max}/\sin\rho\right)=32.84\deg \tag{35}\]

where \(\overline{\varepsilon}\) is the elevation angle corresponding to \(\eta_{Max}\) and does not have a physical meaning. The ECA (\(\overline{\lambda}\)) is calculated using Eq. (34) as

\[\overline{\lambda}=90-\eta_{Max}-\overline{\varepsilon}=12.16\deg \tag{36}\]

In the same manner, the minimum elevation angle (\(\varepsilon_{min}\)) yields its corresponding parameters as \(\bar{\eta}=46.79\deg\) and \(\overline{\lambda}=13.21\deg\). The ECA is the visualized size of the coverage on the Earth's surface; the smaller the ECA, the more degraded the coverage performance becomes. Therefore, a simulation with only \(\overline{\lambda}\), \(\eta_{Max}\), or \(\overline{\varepsilon}\) is enough to analyze if the constellation satisfies the coverage requirement. Since the coverage analyses with \(\overline{\lambda}\), \(\eta_{Max}\), or \(\overline{\varepsilon}\) show the same results but are conducted from different perspectives, the simulation with only one of the three constraints reduces the computational cost.

### Voronoi [PERSON]

The problem of a continuous coverage constellation can be reduced to obtaining the circumradius of three adjacent points. For a set of discretized points, the circumradius of three adjacent points can be defined. When the circumradius is smaller than a specified value, the distance from any point within the region is shorter than the specified value. References [2] and [3] introduced the satellite triad method as a coverage analysis technique for Walker constellations. The research subject of the references was a constellation of fewer than 20 satellites. This study utilizes the Delaunay triangulation method, which was first suggested in [4], to generalize the number of satellites in the constellation.

Delaunay triangulation is a computational geometry method that subdivides discretized points into triangles.[9] This algorithm defines the Delaunay criterion for constructing Delaunay conformant triangles that do not contain other points inside the circumcircles. The Voronoi diagram (VD) is a dual graph of the Delaunay triangle (DT) and is drawn by connecting the circumcenters of the Delaunay triangles. Voronoi tessellation refers to the tiling of a plane or sphere using Voronoi diagrams. If the tiled region is a restricted closed area on the sphere, the Voronoi diagrams have boundaries cut by the region and are called bounded Voronoi diagrams (BVD).[4, 10] The constellation the Earth's surface are discretized points on a three-dimensional spherical surface. The area of interest is not the entire globe, and the Voronoi diagram is bounded within the target region. The spherical Delaunay triangles and spherical bounded Voronoi diagrams derive the solution; however, the word'spherical' is omitted for brevity from here on.

Figure 4 depicts examples of the Delaunay triangle, Voronoi diagram, and bounded Voronoi diagram. In Figure 4a, the six DTs contain \(p_{k}\) as their vertices for an arbitrary subsetellite point \(p_{k}\), where \(k=1,2,...,T\). \(DT_{k,l}\) are depicted as red triangles, and the circumcenters \(C_{k,l}\) are blue dots, where \(l=1,2,...,N_{k}\). \(N_{k}\) is the number of triangles that have vertices \(p_{k}\) and can be different for each \(p_{k}\). Any subsatellite point possesses only one VD, and \(VD_{k}\) is drawn by connecting the blue dots to the circumcenters \(\mathbf{C}_{k}=\{C_{k,l}\mid l=1,2,...,N_{k}\}\), as shown in Figure 4b.

The Voronoi diagram in Figure 4b can be used to solve the global coverage problem. However, for the regional coverage problem, the Voronoi diagram must be bounded within the area of interest. In particular, for the regional continuous coverage problem, the Voronoi diagram bounded within the latitude range of the AoI as a circular band can efficiently analyzes the continuity of the constellation.[4] Considering the northern area of interest, the bounded Voronoi diagram appears in Figure 4c. Then, \(p_{k}\) has \(BVD_{k}\) with different vertices \(\overline{\mathbf{C}}_{k}=\left\{\overline{C}_{k,l}\right\}\mid\overline{l}= 1,2,...,\overline{N}_{k}\right\}\).

The angular distance \(\theta_{k,\overline{l}}\) is defined as the angular distance between the subsatellite point \(p_{k}\) and the vertices \(\overline{C}_{k,\overline{l}}\). Then, the maximum distance \(BVD_{k}\) of the \(k\)th satellite is expressed as:

\[\theta_{max,k}=\max_{\overline{l}}\theta_{k,\overline{l}} \tag{37}\]

Consequently, the maximum angular distance of the entire constellation is obtained as.

\[\theta_{max}=\max_{k}\theta_{max,k} \tag{38}\]

Assuming a homogeneous constellation, the coverage performances of all satellites are the same and can be expressed as \(\lambda^{*}\). Then, the continuous coverage problem statement is defined as

\[\theta_{max}\leq\lambda^{*}. \tag{39}\]

Figure 4: Example: (a) Delaunay triangle, (b) Voronoi diagram, and (c) bounded Voronoi diagram

For the global coverage problem, the maximum angular distance should be defined from \(\theta_{k,l}\) and \(C_{k,l}\), and the remaining procedures are the same.

**APC Decomposition**

The reference 7 developed the APC decomposition based on the circular convolution phenomenon between a seed satellite's access profile, a constellation pattern vector, and a coverage timeline. The access profile between the \(k\)th satellite and the \(j\)th target point (\(\mathbf{v}_{k,j}\)) defines its elements as follows:

\[v_{k,j}\left[\tau\right]\triangleq\begin{cases}1&\text{if }\varepsilon_{k,j} \left[\tau\right]\geq\varepsilon_{k,j,min}\left[\tau\right]\\ 0&\text{otherwise}\end{cases} \tag{40}\]

where \(\tau\) is the discretized time variable and \(\mathcal{J}\) is the set of target points.

The coverage timeline of constellation \(\mathbf{b}_{j}\) is derived as the summation of all access profiles as follows:

\[b_{j}\left[\tau\right]=\sum_{k=1}^{T}v_{k,j}\left[\tau\right] \tag{41}\]

The circular convolution phenomenon expresses the coverage timeline \(\mathbf{b}_{j}\) with respect to the seed satellite access profile \(\mathbf{v}_{0,j}\) and the coverage pattern vector \(\mathbf{x}\) as

\[b_{j}\left[\tau\right]=v_{0,j}\left[\tau\right]\oplus x\left[\tau\right] \tag{42}\]

where \(\mathbf{x}\) is defined in Eq. (25) and \(\oplus\) denotes the circular convolution operator.

This circular convolution operation can be described in a linearized form as follows:

\[\mathbf{b}_{j}=\mathbf{V}_{0,j}\mathbf{x} \tag{43}\]

where \(\mathbf{V}_{0,j}\) is the matrix in Eq. (31).

In summary, the coverage timeline of the entire constellation is obtained from the circular convolution of the seed satellite access profile and the constellation pattern vector. This concept of APC decomposition reduces the optimal CGT constellation design problem to a constellation pattern vector optimization problem.

**RELATIVE MOTION IN ADJACT ORBITAL PLANES**

The satellites in the adjacent orbital planes \(SAT_{m,n}\) and \(SAT_{m+1,n}\) have the angular distances in terms of the differential RAAN and mean anomaly as

\[\Delta u=M_{m+1,n}-M_{m,n}=\frac{360}{T}\cdot F\text{ deg} \tag{44}\]

\[\Delta\Omega=\Omega_{m+1,n}-\Omega_{m,n}=\frac{360}{P}\text{ deg} \tag{45}\]

Since the Walker-Delta constellation satellites are designed to have the same altitude and inclination, the relative motion between \(SAT_{m+1,n}\) and \(SAT_{m,n}\) can be described analytically.[11] The minimum and maximum relative angular distances (\(\theta_{min}\) and \(\theta_{max}\)) are formulated as follows:

\[\sin\left(\theta_{min}/2\right)=\sin\left(\phi_{R}/2\right)\cos\left(i_{R}/2\right) \tag{46}\]\[\cos{(\theta_{max}/2)}=\cos{(\phi_{R}/2)}\cos{(i_{R}/2)} \tag{47}\]

where \(i_{R}\) is the relative inclination and \(\phi_{R}\) is the relative phase.

The relative inclination \(i_{R}\) in Figure 5 is the angle between the orbital planes measured at the orbital intersection and is derived from spherical trigonometry as

\[\begin{split}&\cos{i_{R}}=\cos{i^{2}}+\sin{i^{2}}\cos{\Delta \Omega}\\ &\to i_{R}=i_{R}\left(i;P\right)\end{split} \tag{48}\]

where Eq. (45) is used.

The spherical triangle in Figure 5 derives the geometric relationship between the relative phase \(\phi_{R}\) and the angular distances \(\phi_{m}\) and \(\phi_{m+1}\) as follows:

\[\phi_{m}+\phi_{R}-\phi_{m+1}=180-2\phi_{m+1} \tag{49}\]

where the spherical trigonometric rule that the differential arc between the intersected orbits is \(180-2\phi_{m+1}\) is used. The relative phase \(\phi_{R}\) is obtained by reorganizing Eq. (49)

\[\begin{split}\phi_{R}&=180-2\phi_{m+1}+\left(\phi_ {m+1}-\phi_{m}\right)\\ &=180-2\phi_{m+1}+\Delta u\end{split} \tag{50}\]

where the differential angular distance \(\phi_{m+1}-\phi_{m}\) is the relative argument of the latitude \(\Delta u\) in the Walker-Delta constellation. The formula to calculate \(\phi_{m+1}\) is

\[\begin{split}&\tan{\phi_{m+1}}=\frac{\tan{(90-\Delta\Omega/2)}}{ \cos{i}}\\ &\rightarrow\phi_{m+1}=\phi_{m+1}\left(i;P\right)\end{split} \tag{51}\]

As a result, Eq. (51) provides the argument of \(\phi_{R}\) as follows:

\[\phi_{R}=\phi_{R}\left(i;T,P,F\right) \tag{52}\]

Figure 5: Relative motion of the satellites in the adjacent orbital planes

The inter-satellite link (ISL) constrains the range of relative motion so that the signal is not interfered within the link margin. Therefore, the minimum and maximum relative distances in Eqs. (46) and (47) within the specified range guarantee a smooth ISL communication.

The relative motion of the adjacent orbital plane is described in Eqs. (48), (50), and (51) and explains the relative motion between \(SAT_{m,n}\) and \(SAT_{m+1,n}\) where \(m=1,...,P-1\) and \(n=1,...,S\). When \(m=P\), the relative motion between \(SAT_{P,n}\) and \(SAT_{1,n+F}\) is proven to be the same as the one between \(SAT_{m,n}\) and \(SAT_{m+1,n}\) by Eqs. (1), (2), (48), (50) and (51). As a result, if Eqs. (46) and (47) satisfy the constraint on the ISL link, then all ISL links are connected without any isolated links.

## Simulation Results

### Continuous Coverage Analysis

The constellation is designed using the three constellation design methods introduced in the previous sections: Walker-Delta constellation, quasi-symmetric CGT, and BILP CGT constellations. The seed satellites for the three constellations are designed to have the repetition period of \(\
u=14/1\). The inclination is 42 deg which is 3 deg -5 deg higher than the area of interest [12, 13]. The minimum elevation angle \(\varepsilon_{min}\) is 15 deg and the target point is located in Seoul. The Walker-Delta constellation is analyzed assuming twobody motion, and the target area is a circle with a radius of 100 km around Seoul. The CGT constellations assume \(J_{2}\) perturbation and a single target point. The sampling time or time step \(t_{step}\) is 1 and 300 s for the Walker-Delta and CGT constellations, respectively, and the simulation time horizon is 1 day for both.

Walker-Delta ConstellationFigure 6 depicts the bounded Voronoi diagram simulation result of the Walker-Delta constellation. The global search of a smaller number of satellites obtains that 40 satellites at an inclination of 42 deg is the minimum number of satellites required to achieve the continuous coverage using the Walker-Delta constellation. The empty circles represent the \(T/P/F\)

Figure 6: Bounded Voronoi diagram result of Walker-Delta constellation (_i:_\(T\) = 42: 40)

parameters with duplicate positions in Eq. (14) and are precluded from the coverage analysis. The empty diamond markers indicate that the parameters did not achieve the continuous coverage. The continuous coverage solution is \(i\): \(T/P(S)/F=42\): \(40/40(1)/30\) and denoted as the black diamond. The ECA of this solution (\(\lambda^{*}\)) is \(15.86\deg\).

Figure 8: APC Decomposition of (a) quasi-symmetric and (b) BILP CGT constellation

Figure 7: Configurations of quasi-symmetric and BILP CGT constellations in (\(\Omega,M\)) space

_Common Ground-track Constellation_ The quasi-symmetric constellation pattern vector \(x_{qs}\) and BILP constellation pattern vector \(x_{bilp}\) are obtained as

\[x_{qs}=\begin{cases}1&\text{for }n=\{0,9,18,27,36,45,54,63,72,81,90,99,108,117,126,135,...\\ &144,153,162,171,180,189,198,207,216,225,234,243,252,261,270,279\}\\ 0&\text{otherwise}\end{cases} \tag{53}\]

\[x_{bilp}=\begin{cases}1&\text{for }n=\{9,14,22,27,29,55,60,63,68,96,101,104,1 09,114,137,...\\ &142,150,155,175,183,188,191,216,221,224,229,232,257,262,265,270\}\\ 0&\text{otherwise}\end{cases} \tag{54}\]

The CGT constellation's pattern reveals its characteristics in the \((\Omega,M)\) space, such as period ratio and symmetricity (Figure 7). The gradient of the admissible set is \(-N_{P}/N_{D}\) and is equal to \(-\
u\) by Eqs. (25) and (15). The constellation pattern vectors are laid on the points along the admissible set. The quasi-symmetric set configures symmetrically in Figure 7 as \(\mathbf{x}_{qs}\) in the second panel of Figure 8a is equally spaced. Because \(N_{qs}\) is 32 and \(L\) is 288, \(L/N_{qs}\) is divided into an integer 9, and the spacing is perfectly symmetric. On the other hand, the BILP constellation pattern vector is irregularly spaced in Figures 7 and 8b. However, the BILP constellation achieves the smaller number of satellites \(N_{bilp}\) as 31, while both constellations exhibit the single-fold coverage.

distinguish the number of planes, and the \(x\) axis represents the \(F\) numbers. As this graph shows the relative motion at a glance, it is a useful tool for ISL connectivity analysis. The continuous coverage solution \(i\): \(T/P(S)/F=42\): \(40/40(1)/30\) has a relative motion range from 9559.77 km to 9589.64 km.

Common Ground-track ConstellationThe relative motion equations, Eqs. (48), (50), and (51), imply that the relative motion of two orbits with the same altitude and inclination is a function of the inclination, relative RAAN, and relative argument of latitude. Let us define a set of temporal location \(\tau_{k}\) in Eq. (26) as \(\tau_{k}\). Then, \(\tau_{k,qs}\) and \(\tau_{k,bilp}\) are calculated as Eqs. (53) and (54). The temporal location \(\tau_{k}\) derives the RAAN \(\Omega_{k}\) as shown in Eq. (55).[7]

\[\Omega_{k}=\tau_{k}\cdot\frac{2\pi N_{D}}{L}+\Omega_{0} \tag{55}\]

where the subscript '0' means that the variable is relevant to the seed satellite. Equation (25) describes the relationship between \(\Omega_{k}\) and \(M_{k}\).

Let us define \(\Delta\tau_{k}\) as the difference between consecutive \(\tau_{k}\) values:

\[\Delta\tau_{k}=\begin{cases}\tau_{k+1}-\tau_{k}&\text{for }k=1,...,T-1\\ \tau_{k}+L-\tau_{1}&\text{for }k=T\end{cases} \tag{56}\]

Thus, Eqs. (53), (54), and (56) are used to calculate \(\Delta\tau_{k}\) for the two CGT constellations as

\[\Delta\tau_{k,qs}=9 \tag{57}\]

\[\Delta\tau_{k,bilp}=2,3,5,8,20,23,25,26,27,28 \tag{58}\]

Figure 10: Minimum and maximum relative distance between the adjacent orbital plane of quasi-symmetric and BILP CGT constellations

Equation (55) derives the relative RAAN \(\Delta\Omega_{k}\) and the relative mean anomaly \(\Delta M_{k}\) as

\[\begin{cases}\Delta\Omega_{k,qs}=11.25\deg\\ \Delta M_{k,qs}=202.50\deg\end{cases} \tag{59}\]

\[\begin{cases}\Delta\Omega_{k,bilp}=2.5,3.75,6.25,10.00,25.00,28.75,31.25,32.50, 33.75,35.00\deg\\ \Delta M_{k,bilp}=10.00,220.00,230.00,247.50,265.00,272.50,282.50,307.50,...\\ 317.50,325.00\deg\end{cases} \tag{60}\]

The minimum and maximum relative distances in Eqs. (46) and (47) are depicted in Figure 10. The minimum and maximum relative distances appear almost identical for some cases because the differences are less than 1000 km. The minimum and maximum relative distances for the quasi-symmetric CGT constellation are 13854.32 and 13886.49 km, respectively. The BILP CGT constellation has various values of \(\Delta\tau_{k}\). When \(\Delta\tau_{k}\) is 8, the minimum and maximum relative distances reach their largest values at 13164.56 and 13191.33 km, respectively.

## Conclusion

This paper investigates the continuous coverage analysis methods and the inter-satellite link connectivity analysis method for communication satellite constellations. The bounded Voronoi diagram is used to design a homogeneous constellation that ensures continuous regional and global coverage. The APC decomposition, based on the grid method, can be implemented for the CGT constellation's coverage analysis. The relative motion in adjacent orbital planes yields the analytical solutions that must be constrained within the inter-satellite link range.

The coverage performance of the Walker-Delta constellation was analyzed using the bounded Voronoi diagram as an example. Two types of CGT constellations, the quasi-symmetric and the BILP, were analyzed using APC decomposition to compare their coverage performance. The BILP optimal CGT constellation has an asymmetric configuration but achieves a smaller number of satellites. However, the relative motion range of the Walker-Delta constellation is shorter and more consistent, which implies that the Walker-Delta constellation has advantages for inter-satellite links. The relative motion of the BILP constellation has a variety of ranges due to its asymmetry, but satellites are located closer than the quasi-symmetric constellation. In summary, the BILP constellation is advantageous in terms of the number of satellites required for a single-fold coverage. However, the Walker-Delta constellation may have a shorter and more stable relative motion range, which is beneficial for inter-satellite links.

## Acknowledgment

This work was supported by the Korea Research Institute for defense Technology Planning and Advancement (KRIT) grant funded by the Korean government (DAPA (Defense Acquisition Program Administration)) (KRIT-CT-22-040, Heterogeneous Satellite Constellation-based ISR Research Center, 2024).

**NOTATION**

\begin{tabular}{r l} \(a\) & semi-major axis \\ \(b\) & coverage timeline \\ \(\delta\) & Kronecker delta function \\ \(e\) & eccentricity \\ \(f\) & coverage requirement vector \\ \(i\) & inclination \\ \(f\) & coverage requirement \\ \(h\) & altitude \\ \(j\) & index for grid point \\ \(J_{2}\) & coefficient for J2 perturbation \\ \(\mathcal{J}\) & set of grid points \\ \(k\) & index for satellites \\ \(L\) & number of discrete times (length of discrete time variable) \\ \(m\) & index for orbital planes \\ \(n\) & index for satellites on a plane \\ \(N_{P}\) & revolutions to repeat \\ \(N_{D}\) & days to repeat \\ \(P\) & number of orbital planes \\ \(F\) & Phasing parameter \\ \(R_{E}\) & Earth radius \\ \(p\) & semilatus rectum \\ \(\mu_{E}\) & standard gravitational parameter of Earth \\ \(S\) & number of satellites on an orbital plane \\ \(T\) & total number of satellites \\ \(T_{r}\) & repetition period of RGT orbit \\ \(T_{S}\) & nodal period of the satellite \\ \(T_{G}\) & nodal period of greenwich \\ \(T_{sim}\) & simulation time \\ \(t_{step}\) & time step \\ \(t\) & continuous time variable \\ \(t_{0}\) & epoch time \\ \(t_{F}\), \(t_{P}\) & Walker-Delta pattern repetition period \\ \(u\) & argument of latitude \\ \(v\) & access profile \\ \(\mathbf{V}\) & access profile circulant matrix \\ \(\mathbf{x}\) & constellation pattern vector \\ \(\mathbb{Z}_{2}\) & binary integer number set \\ \(\epsilon\) & elevation angle \\ \(\eta\) & angular size of payload's coverage \\ \(\rho\) & angular radius of Earth \\ \(\lambda\) & Earth central angle \\ \(\
u\) & period ratio \\ \(\phi\) & phase angle \\ \(\tau\) & discretized time variable \\ \(\omega\) & argument of perigee \\ \(\omega_{E}\) & Earth rotation speed \\ \(\omega_{orb}\) & orbital angular speed \\ \(\Omega\) & right ascension of ascending node \\ \(\xi\) & spacing constant \\ \(\theta\) & angular distance \\ \end{tabular}

## References

* [1] [PERSON], [PERSON], and [PERSON], \"A technical comparison of three low earth orbit satellite constellation system to provide global broadband,\" _Acta Astronautica_, Vol. 159, 2019, pp. 123-135.
* [2] [PERSON], \"Circular Orbit Patterns Providing Continuous Whole Earth Coverage,\" _Technical rept._, 1970, pp. 19-23.
* [3] [PERSON], \"Continuous Whole-Earth Coverage by Circular-Orbit Satellite Patterns,\" _Technical rept._, 1977, pp. 3-26.
* [4] [PERSON], [PERSON], [PERSON], and [PERSON], \"Communication Satellite Constellation Design of Minimum Number of Satellites: Analytic Approach to Walker-Delta Pattern Design,\" _Journal of the Korean Society for Aeronautical and Space Sciences_, Vol. 52, No. 9, 2024, pp. 749-760.
* [5] [PERSON], _Fundamentals of Astrodynamics and Applications_. Microcosm and Springer, 2013.
* [6] [PERSON], [PERSON], and [PERSON], \"The 2-D Lattice Theory of Flower Constellations,\" _Celestial Mechanics and Dynamical Astronomy_, Vol. 116, No. 4, 2013, pp. 325---337.
* [7] [PERSON], [PERSON], [PERSON], and [PERSON], \"Satellite Constellation Pattern Optimization for Complex Regional Coverage,\" _Journal of Spacecraft and Rockets_, Vol. 57, No. 6, 2020, pp. 1309-1327.
* [8] [PERSON], [PERSON], and [PERSON], _Integer Programming_. 2014.
* [9] [PERSON], \"Sur la sphere vide,\" _Bulletin de l'Academie des Sciences de l'URSS, Classe des Sciences Mathematiques et Naturelles_, Vol. 6, 1934, pp. 793-800.
* [10] [PERSON], [PERSON], [PERSON], [PERSON], [PERSON], and [PERSON], \"Analysis of Satellite Constellations for the Continuous Coverage of Ground Regions,\" _Journal of Spacecraft and Rockets_, Vol. 54, No. 6, 2017, pp. 1294-1303.
* [11] [PERSON], _Orbit and constellation design and management_. Springer, NewYork, 2009.
* [12] [PERSON], \"Coverage, Responsiveness, and Accessibility for Various 'Responsive Orbits',\" _3 rd Responsive Space Conference_, 2005.
* [13] [PERSON], [PERSON], and [PERSON], \"Design and Maintenance of Low-Earth Repeat-Groundtrack Successive-Coverage Orbits,\" _Journal of Guidance, Control, and Dynamics_, Vol. 35, No. 2, 2012, pp. 686-691.