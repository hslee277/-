```mermaid
flowchart LR


subgraph Baseband
F[Fourier];
PS[Pulse Shaping RC RRC];
LC[Line Coding];
DPCM[DPCM];
OFDM[OFDM CP];
LDPC[LDPC Turbo];
HARQ[HARQ];
PLLCDR[PLL CDR];
F --> PS;
LC --> PLLCDR;
DPCM --> LC;
OFDM --> PS;
end


subgraph Channel
AW[AWGN];
SNR[SNR];
DS[Delay Spread];
Bc[Coherence BW];
ISI[ISI];
FZ[Fresnel Zone];
Lfs[Path Loss];
IONO[LUF MUF FOT];
PLAN[Freq Planning];
FADING[Fading];
DOPPLER[Doppler Tc];
PL[Path Loss Models];
AW --> SNR;
DS --> Bc;
Bc --> ISI;
FZ --> Lfs;
IONO --> PLAN;
FADING --> SNR;
DOPPLER --> Bc;
PL --> Lfs;
end


subgraph RF
PLL[PLL];
LOPN[Phase Noise];
RFF[RF Filter];
SEL[Selectivity];
RX[Double Superhet];
LNA[LNA];
MIX[Mixer];
PA[PA DPD];
DUP[Duplexer SAW BAW];
ANT[Antenna Pattern Pol];
AGC[AGC];
MIMO[MIMO Beamforming];
PLL --> LOPN;
RFF --> SEL;
RX --> SEL;
LNA --> RX;
MIX --> RX;
PA --> IMD;
DUP --> RFF;
ANT --> SNR;
AGC --> RX;
MIMO --> SNR;
end


subgraph Measure
DOPPLER --> EVM;
end
