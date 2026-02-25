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

<div align="center">
  <img src="https://github.com/user-attachments/assets/2d860159-f46b-471c-8713-f3e23350386f" alt="system_structure" width="500"/>
</div>

<p align="center">
  <i>FAtiMA-Toolkit과 DST 게임 엔진 간의 HTTP 통신 및 Behavior Tree 구조</i>
</p>

- **FAtiMA-Toolkit**: AI의 감정 상태 및 의사결정 프로세스 엔진
- **Behavior Tree (BT)**: 성격별 우선순위에 따른 행동 제어 (Sequence, Selector, Loop)
- **Speech System**: Microsoft Azure ASR/TTS + KoNLPy 기반 실시간 음성 상호작용
- **HRI Mod**: 게임 내 상태(State) 및 유저 행동 데이터 실시간 ETL


### 실험 및 시스템 시연 영상  
<div align="center">
  <a href="https://youtu.be/eJQ-J4fJ_uM">
    <img src="https://img.youtube.com/vi/eJQ-J4fJ_uM/0.jpg" alt="관련 영상 썸네일"/>
  </a>
</div>


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


## 주요 연구 결과

- **가상 협업 환경에서의 AI Proximity에 따른 인간 행동 엔트로피 분석**
    - **측정 지표**
      - *Proximity (근접도)*: 실험 중 AI 에이전트와 유저 간의 물리적 거리의 평균값
      - *Shannon’s Entropy (행동 엔트로피)*: 유저의 이동 경로를 그리드(Grid) 단위로 나누어 각 영역의 방문 빈도를 확률 분포로 변환, 행동의 무작위성(Randomness)을 정량화
    - **분석 방법**
      - 실시간 행동 로그(X, Z 좌표) 데이터를 기반으로 한 시공간 궤적 분석(Spatio-temporal Trajectory Analysis)

  - **핵심 발견 및 해석**
    - *결과*
      - AI와 유저 간의 거리가 가까울수록 인간의 이동 패턴 엔트로피가 낮아지는 유의미한 음의 상관관계($r = -0.5024$) 확인
    - *기술적 해석*
      - **행동의 구조화(Behavioral Structuring):** 유저가 AI를 단순 객체가 아닌 협업 파트너로 인식할 때 AI의 동선에 맞춰 자신의 이동 경로를 최적화하거나 동기화(Social Synchronization)하는 경향이 나타남
      - **예측 가능성 증대:** 높은 근접도는 인간 행동의 불확실성을 감소시키고, 이는 인간-AI 협업 시스템에서 인간 행동의 예측 가능성(Predictability)을 높이는 중요한 요인으로 작용함
    - *데이터 시각화 인사이트*
      - **Low Entropy (좌측 이미지군):** 특정 목표(예: AI와의 협동, 베이스캠프 중심 활동)를 중심으로 안정적이고 반복적인 경로 형성
      - **High Entropy (우측 이미지군):** AI와의 상호작용이 적을 때 탐색 중심의 무작위적이고 복잡한 이동 패턴이 나타남


<div align="center">
  <img src="https://github.com/user-attachments/assets/4d9556d0-5592-4149-b99a-4cfb60165e20" alt="heatmap" width="500"/>
</div>
<p align="center">좌: 정적인 이동 패턴(Low Entropy) / 우: 능동적·복잡한 이동 패턴(High Entropy)</p>

## Limitation
- **표본 크기:** 면대면 실험의 한계로 인한 샘플 수 부족 (N=36).
- **AI 자연스러움:** 룰 기반 Behavior Tree의 한계로 인해 인간 수준의 유연한 상호작용 부족.
- **향후 과제:** 강화학습(RL) 기반 에이전트 및 LLM(Large Language Model) 연동 대화 시스템 도입 필요.

## 참고 문헌
> Cho, Han Sae. "Exploring factors that Influence Human Behavior of AI Personality in Virtual Collaborative Environment." Master's Thesis, Hanyang University (2023).
