---
icon: lucide/book-open-check
--- 
# Thesis 

## 가상 협업 환경에서의 AI 성격이 인간 행동에 미치는 영향 탐색 (Exploring Factors Influencing Human Behavior of AI Personality)

## 핵심 목적
**가상 협업 환경(DST)에서 AI 에이전트의 성격(Behavioral Personality) 변화가 인간의 행동 패턴 및 인지적 반응에 미치는 영향을 정량적으로 분석**

### 주요 기능
1. [x] DST(Don't Starve Together) 내 자율 행동 AI 에이전트 구축
2. [x] AI 성격(Adventurer, Camper, Supporter)별 파라미터 튜닝 및 Behavior Tree 설계
3. [x] 멀티모달 데이터 수집 (음성 대화, 게임 내 이동 경로, 액션 로그, 설문)
4. [x] Shannon's Entropy 기반 인간 행동의 무작위성(Randomness) 수치화
5. [x] AI 성격 분류 예측 모델링 (Few-Shot Learning 시도)

### 시스템 아키텍처 - Autonomous AI System
- **FAtiMA-Toolkit**: AI의 감정 상태 및 의사결정 프로세스 엔진
- **Behavior Tree (BT)**: 성격별 우선순위에 따른 행동 제어 (Sequence, Selector, Loop)
- **Speech System**: Microsoft Azure ASR/TTS + KoNLPy 기반 실시간 음성 상호작용
- **HRI Mod**: 게임 내 상태(State) 및 유저 행동 데이터 실시간 ETL

### 분석 방법론: Shannon's Entropy
인간의 이동 경로를 그리드(Grid)로 나누어 방문 빈도를 확률로 계산하고, 행동의 복잡도를 정량화함.

```python title="Shannon's Entropy Calculation"
import numpy as np

def calculate_entropy(probabilities):
    """
    행동 패턴의 복잡도(무작위성)를 산출
    """
    # 0인 확률값 제외 (log 계산 불가)
    probabilities = probabilities[probabilities > 0]
    return -np.sum(probabilities * np.log2(probabilities))
```


## 데이터셋

| 항목         | 내용                                                                 |
|--------------|---------------------------------------------------------------------|
| 실험 환경    | Don't Starve Together (Open-world Survival Game)                     |
| 전체 샘플    | 36명의 한국인 성인 (각 AI 성격당 12명 배정)                             |
| 행동 변수    | X, Y, Z 좌표, 현재 액션(PICK, ATTACK 등), 인벤토리 상태 등 25개 피처 |
| 음성 데이터  | 발화 횟수, 대화 스크립트, 발화 시간대                                 |
| 심리 측정    | Godspeed Scale, Networked Minds (Social Presence)                    |


| AI 성격 (Label) | 주요 목표 (Goal) | 기술적 파라미터 (Parameters) |
|-----------------|------------------|------------------------------|
| **Adventurer**  | 지도 탐험 (Vision) | max_player_dist (High), travel_chance (0.5) |
| **Camper**      | 자원 수집 (Resource)| pick_chance (1.0), gohome_chance (0.8) |
| **Supporter**   | 유저 조력 (Proximity)| max_player_dist (Low), pick_chance (1.0) |



## 모델 구조 (AI Personality System)
<div align="center">
  <img src="https://github.com/user-attachments/assets/2d860159-f46b-471c-8713-f3e23350386f" alt="system_structure" width="500"/>
</div>


> FAtiMA-Toolkit과 DST 게임 엔진 간의 HTTP 통신 및 Behavior Tree 구조

## 주요 연구 결과

### 1. AI와의 거리와 인간 행동 엔트로피의 상관관계
- **발견:** AI와 인간의 거리(Proximity)가 가까울수록, 인간의 이동 패턴 엔트로피가 낮아짐 (행동이 덜 무작위적이고 안정적임).
- **상관계수:** $r = -0.5024$ (유의미한 음의 상관관계)

### 2. AI 성격 분류 모델 성과
| 모델         | Accuracy | AUC     | 비고                                      |
|--------------|----------|---------|-------------------------------------------|
| RF + SMOTE   | 0.4500   | 0.4081  | 데이터 부족(N=36)으로 인한 낮은 일반화 성능 |

## 데이터 시각화 (Heatmap & Analysis)
<div align="center">
  <img src="https://github.com/user-attachments/assets/4d9556d0-5592-4149-b99a-4cfb60165e20" alt="heatmap" width="500"/>
</div>
> 좌: 정적인 이동 패턴(Low Entropy) / 우: 능동적/복잡한 이동 패턴(High Entropy)

## Limitation
- **표본 크기:** 면대면 실험의 한계로 인한 샘플 수 부족 (N=36).
- **AI 자연스러움:** 룰 기반 Behavior Tree의 한계로 인해 인간 수준의 유연한 상호작용 부족.
- **향후 과제:** 강화학습(RL) 기반 에이전트 및 LLM(Large Language Model) 연동 대화 시스템 도입 필요.

## 참고 문헌
> Cho, Han Sae. "Exploring factors that Influence Human Behavior of AI Personality in Virtual Collaborative Environment." Master's Thesis, Hanyang University (2023).
