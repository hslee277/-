# -flowchart LR
subgraph Channel[Channel]
AW[AWGN]-->SNR[SNR]
DS[지연확산 τ_rms]-->Bc[상관대역폭 B_c]
Bc-- B_c↓ -->ISI[ISI]
FZ[프레넬존]-->Lfs[경로손실↑]
IONO[LUF/MUF/FOT]-->Plan[주파수계획]
Fading[페이딩(Rayleigh/Rice)
(연관)]-->SNR
Doppler[도플러/Coherence time T_c
(연관)]-->Bc
PL[경로손실모델
Okumura/Hata/CI
(연관)]-->Lfs
end


subgraph RF[RF/Frontend]
PLL[PLL]-->LOPN[위상잡음]
RFf[RF필터]-->Sel[선택도]
RX[Double Superhet]-->Sel
LNA[LNA
(연관)]-->RX
MIX[Mixer
(연관)]-->RX
PA[PA/DPD
(연관)]-->IMD
DUP[Duplexer/SAW/BAW
(연관)]-->RFf
ANT[안테나 패턴/편파
(연관)]-->SNR
AGC[AGC
(연관)]-->RX
MIMO[MIMO/Beamforming
(연관)]-->SNR
end


subgraph Measure[Measure/Quality]
SA[스펙트럼 분석기]-->ACPR
EVM[EVM]-->BER
IMD[IMD3]-->ACPR
EbN0[Eb/N0
(연관)]-->BER
end


%% ===== 상호관계 =====
PS-- α↑·BW↑; ISI↓ -->EVM
AW-- kTB↑; NF↑ -->SNR
SNR-- SNR↑ -->EVM
Lfs-- 손실↑ -->SNR
LOPN-- 위상잡음↑ -->EVM
IMD-- 왜곡↑ -->EVM
SA-- RBW↓→DANL↓ -->
RX-- 감도(MDS)↓ →EVM
FTN[FTN τ<1]-- SE↑; ISI↑ -->MF[정합필터/MLSE]


%% ===== 추가 연관 엣지 =====
OFDM-- CP로 ISI↓ -->ISI
EQ[등화 ZF/MMSE/DFE
(연관)]-- 주파수선택성 보상 -->ISI
DIV[다이버시티 MRC/SC
(연관)]-- 페이딩 보상; SNR↑ -->SNR
LDPC-- 코딩이득; BER↓ -->BER
HARQ-- 재전송; BLER↓ -->BER
MIMO-- 배열이득/SE↑ -->SNR
LNA-- NF_sys↓; MDS 개선 -->SNR
PA-- DPD로 IMD/ACPR 개선 -->IMD
DUP-- 이미지/인접 차단 -->Sel
ANT-- G_t/G_r↑; 경로개선 -->SNR
PL-- 환경별 손실 예측 -->Lfs
Fading-- 주파수선택성/시간선택성 ↑ -->Bc
Doppler-- T_c≈1/(2f_d) → 시간선택성 -->EVM
EbN0-- BER 성능 기준 -->8PSK[8-PSK]
