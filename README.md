```mermaid
flowchart LR
%% ===== 영역 구분 =====
subgraph Baseband
F[푸리에] --> PS[펄스성형 RC/RRC]
LC[라인코딩] --> PLL_CDR[PLL/CDR]
DPCM --> LC
OFDM[OFDM/CP (연관)] --> PS
LDPC[채널코딩 LDPC/Turbo (연관)]
HARQ[HARQ (연관)]
end


subgraph Channel
AW[AWGN] --> SNR[SNR]
DS[지연확산 tau_rms] --> Bc[상관대역폭 Bc]
Bc -- "Bc down" --> ISI[ISI]
FZ[프레넬존] --> Lfs[경로손실 증가]
IONO[LUF/MUF/FOT] --> Plan[주파수계획]
Fading[페이딩 Rayleigh/Rice (연관)] --> SNR
Doppler[도플러 / Coherence time Tc (연관)] --> Bc
PL[경로손실모델 Okumura/Hata/CI (연관)] --> Lfs
end


subgraph RF
PLL[PLL] --> LOPN[위상잡음]
RFf[RF 필터] --> Sel[선택도]
RX[Double Superhet] --> Sel
LNA[LNA (연관)] --> RX
MIX[Mixer (연관)] --> RX
PA[PA/DPD (연관)] --> IMD
DUP[Duplexer/SAW/BAW (연관)] --> RFf
ANT[안테나 패턴/편파 (연관)] --> SNR
AGC[AGC (연관)] --> RX
MIMO[MIMO/Beamforming (연관)] --> SNR
end


subgraph Measure
SA[스펙트럼 분석기] --> ACPR[ACPR]
EVM[EVM] --> BER[BER]
IMD[IMD3] --> ACPR
EbN0[Eb/N0 (연관)] --> BER
end


%% ===== 관계선 =====
PS -- "roll-off up -> ISI down" --> EVM
AW -- "kTB up; NF up" --> SNR
SNR -- "SNR up" --> EVM
Lfs -- "loss up" --> SNR
LOPN -- "phase noise up" --> EVM
IMD -- "nonlinearity up" --> EVM
RX -- "MDS down -> quality up" --> EVM
FTN[FTN tau<1] -- "SE up; ISI up" --> MF[정합필터/MLSE]


OFDM -- "CP reduces ISI" --> ISI
EQ[등화 ZF/MMSE/DFE (연관)] -- "equalize channel" --> ISI
DIV[다이버시티 MRC/SC (연관)] -- "fading mitigation" --> SNR
LDPC -- "coding gain" --> BER
HARQ -- "retransmission -> BLER down" --> BER
MIMO -- "array gain/SE up" --> SNR
LNA -- "NF_sys down -> MDS better" --> SNR
PA -- "DPD -> IMD/ACPR better" --> IMD
DUP -- "image/adjacent rejection" --> Sel
ANT -- "Gt/Gr up" --> SNR
PL -- "predict path loss" --> Lfs
Fading -- "selective fading" --> Bc
Doppler -- "Tc ~ 1/(2 fd)" --> EVM
