```mermaid
flowchart LR
ISI[ISI]
FZ[Fresnel Zone]
Lfs[Path Loss]
IONO[LUF/MUF/FOT]
PLAN[Freq Planning]
FADING[Fading Rayleigh/Rice]
DOPPLER[Doppler / Tc]
PL[Path Loss Models]
AW --> SNR
DS --> Bc
Bc --> ISI
FZ --> Lfs
IONO --> PLAN
FADING --> SNR
DOPPLER --> Bc
PL --> Lfs
end


subgraph RF
PLL[PLL]
LOPN[Phase Noise]
RFf[RF Filter]
SEL[Selectivity]
RX[Double Superhet]
LNA[LNA]
MIX[Mixer]
PA[PA/DPD]
DUP[Duplexer SAW/BAW]
ANT[Antenna Pattern/Pol]
AGC[AGC]
MIMO[MIMO/Beamforming]
PLL --> LOPN
RFf --> SEL
RX --> SEL
LNA --> RX
MIX --> RX
PA --> IMD
DUP --> RFf
ANT --> SNR
AGC --> RX
MIMO --> SNR
end


subgraph Measure
SA[Spectrum Analyzer]
ACPR[ACPR]
EVM[EVM]
BER[BER]
IMD[IMD3]
EbN0[Eb/N0]
SA --> ACPR
EVM --> BER
IMD --> ACPR
EbN0 --> BER
end


%% Cross-links (라벨 없이 안정성 우선)
PS --> EVM
AW --> SNR
SNR --> EVM
Lfs --> SNR
LOPN --> EVM
IMD --> EVM
RX --> EVM
FTN[FTN tau<1] --> MF[Matched Filter/MLSE]
OFDM --> ISI
EQ[Equalizer ZF/MMSE/DFE] --> ISI
DIV[Diversity MRC/SC] --> SNR
LDPC --> BER
HARQ --> BER
MIMO --> SNR
LNA --> SNR
PA --> IMD
DUP --> SEL
ANT --> SNR
PL --> Lfs
FADING --> Bc
DOPPLER --> EVM
