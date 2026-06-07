# IPTV vs 미다팀 채널 시청점유율 동등성 검증

**Author:** 김가현 (Korea University, Dept. of Statistics)  
**Report:**  https://rpubs.com/khyitty/1382402 

# IPTV Viewing-Share Equivalence Analysis

Statistical equivalence analysis assessing whether Mida Team's 
viewing-share dataset can independently substitute for IPTV-based 
measurement across 254 matched channels.

Methods: Wilcoxon signed-rank test, TOST, Tolerance Interval (Howe's method)  
Tools: R, Quarto

## 분석 개요

KT IPTV에서 자체 산출한 채널 시청점유율 데이터와 미다팀 데이터 간의
동등성을 통계적으로 검증합니다.
채널명 기준 1:1 매핑을 통해 두 데이터셋을 대응시킨 후,
평균 수준의 동등성과 개별 채널 수준의 동등성을 모두 검정하였습니다.

## 분석 흐름

1. **데이터 전처리** — 채널명 기준 1:1 매핑, 결측 및 제외 채널 처리
2. **시각화 (EDA)** — 산점도 (Y=X 기준선), 차이값 분포 히스토그램
3. **정규성 검정** — Shapiro-Wilk (원본 및 로그 변환)
4. **기초 통계 검정** — 대응표본 t-검정, Wilcoxon 부호순위 검정
5. **동등성 검정**
   - TOST (Mean Equivalence): δ = 0.01 / 0.02 / 0.05 조건별 검정
   - Individual Equivalence: Tolerance Interval 방법 (normtol.int)
   - 민감도 분석: 신뢰수준·포함 비율 조건 변화에 따른 강건성 확인

## 사용 패키지

| 패키지 | 용도 |
|--------|------|
| `readxl` | 엑셀 데이터 로드 |
| `dplyr` | 데이터 전처리 |
| `ggplot2` | 시각화 |
| `TOSTER` | TOST 동등성 검정 |
| `tolerance` | Tolerance Interval 계산 |
| `gridExtra` | 다중 플롯 배치 |

## 주요 결과

- Pearson 상관계수 r ≈ 0.97 — 두 데이터 간 높은 선형 일치도 확인
- 대응표본 t-검정 및 Wilcoxon 검정: 평균/중앙값 차이 유의하지 않음 (p > 0.05)
- TOST: δ = 0.05 기준에서 평균 동등성 확인
- Individual Equivalence: 95% Tolerance Interval [-0.403, 0.422]이 목표 허용 한계 ±0.5 내에 포함 → **PASS**
- 민감도 분석: 모든 조건(신뢰수준 90%, 포함 비율 85%)에서 PASS — 결과 강건함

## 파일 구조

```
IPTV-Data-Analysis/
├── iptv2.qmd        # 분석 소스 코드 (Quarto)
├── iptv2.html       # 렌더링된 분석 보고서
├── odata.xlsx       # 원본 데이터 (비공개)
└── README.md
```

> `odata.xlsx`는 데이터 보안상 레포에 포함되지 않습니다.
