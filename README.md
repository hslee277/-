```mermaid
flowchart LR


RX --> SEL


LNA --> RX


MIX --> RX


PA --> IMD


DUP --> RFF


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
EBN0[Eb N0]


SA --> ACPR


EVM --> BER


IMD --> ACPR


EBN0 --> BER
end


%% Cross links
PS --> EVM


AW --> SNR


SNR --> EVM


Lfs --> SNR


LOPN --> EVM


IMD --> EVM


RX --> EVM


FTN[FTN] --> MF[Matched Filter MLSE]


OFDM --> ISI


EQ[Equalizer] --> ISI


DIV[Diversity] --> SNR


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
