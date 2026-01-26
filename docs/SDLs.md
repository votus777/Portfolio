---
icon: lucide/flask-conical
---

# Self-Driving Laboratories for Flavor Discovery

**로보틱스 기반 자동 디스펜싱 및 조합 시스템 설계**


## OKR

| Objective                                                      | Key Results                                                                                                                        |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| 맛 데이터 수집 시스템의 정량화 및 자동화 구현              | Isaac Sim 기반 디지털 트윈 구축 및 가상-실제 환경 동작 일치율(Pick-and-place 성공률 등) 98% 이상 달성                        |
|                                                               | 수동 대비 데이터 수집 속도 5배 이상 향상 및 주당 500개 이상 신규 배합 조합 데이터 생성                                       |
| 데이터 기반 재현 가능한 맛 분석 인프라 완성               | 분석 장비(Sensor/GC-MS 등)의 데이터를 DB에 실시간 적재하는 파이프라인 구축|
|                                                               | 데이터셋 재현성 테스트를 통한 동일 레시피 화학적 조성 일치도 95% 이상 확보                                                   |
| 자율 최적화를 통한 탐색 공간 축소                                   |  베이지안 최적화(Bayesian Optimization) 또는 RL 알고리즘을 도입하여, 목표 맛 프로필에 도달하기 위한 실험 횟수를 기존 랜덤 샘플링 대비 80% 이상 감축                                  |
|                                                               |  AI 에이전트가 실험 결과가 '실패'일 경우, 그 원인을 분석하여 다음 실험의 Search Space를 스스로 재정의(Refinement)하는 기능을 구현                                                  |


#### Schematic for the autonomy levels of SDL
![model](https://github.com/user-attachments/assets/971e83a9-9d49-4afe-ad76-65b9d9837f90)

- **Search space**: 사람(인간)이 시험 시료 배치  
- **Experiment selection**: AI 알고리즘 기반 조합 실험 설계

- **소프트웨어/하드웨어 수준**: Level 0 → Level 1 전환 단계  
- **목표:** 중앙 집중형(Workstation-based) SDL Level 2 달성



## 하드웨어 및 인프라 아키텍처

**Isaac Sim 기반 Digital Twin**  
ROS2 Bridge로 **Sim-to-Real** 전이 지원  
가상 센서 데이터(RGB-D, LiDAR 등) ROS2 토픽 전송  
MoveIt2 등 ROS2 제어 명령을 가상·실제 로봇에 동일 적용  
Digital Twin에서 검증한 로직 그대로 현실 이식 가능  


**1. 센싱 시스템 (Sensing System)**  
- **화학 센서:**  
    - **전자혀(Electronic Tongue):** 맛 성분 감지용 센서 어레이  
    - **전자코(Electronic Nose):** 휘발성 유기화합물(VOC) 패턴 분석  
    - **기본 분석:** pH 센서, 당도계(Brix), 염도 센서  
- **물리 센서:**    
    - **점도계:** 식감 관련 데이터 측정  
    - **환경 센서:** 실험실 온도, 습도 모니터링 및 기록  

**2. 샘플 처리 및 조제 시스템 (Sample Handling)**    
- **로봇 시스템:**    
    - **6축 로봇 팔:** 정밀 제어 및 시료 이송 (Interbotix VX300S 또는 xArm 6)
    - **디지털 트윈:** NVIDIA Isaac Sim을 활용한 물리 시뮬레이션 및 Sim-to-Real 환경 구축  
- **조제 장치:**  
    - **자동 피펫팅 시스템:** Liquid Handler(OpenTrons OT-2 등) 연동  
    - **자동 디스펜서:** 액체/반고체 시료의 정량 분주  
    - **환경 제어:** 온도 조절 챔버 및 교반 장치  

**3. 데이터 수집 인프라**  
- **제어기:** ROS2 Humble 기반 통합 제어 PC  
- **네트워크:** 실시간 데이터 적재를 위한 컴퓨팅 서버  

**분석 자동화**: 센서 모듈(전자코, e-tongue 등)과 측정 데이터를 실시간 DB로 적재하는 파이프라인 구축  


### 하드웨어 구매 및 예산 측정 
 - 나라장터의 입찰공고, 낙찰정보, 발주계획을 통해 타 연구실 및 실험실의 하드웨어 견적을 살펴볼 수 있음 
 - 국가연구시설장비진흥센터(ZEUS)에서 실제 연구실에 어떤 장비가 도입되어 있는지 검색할 수 있음

---

## 소프트웨어 스택 및 AI 에이전트 워크플로우


| 단계            | 역할                               | 주요 기술/라이브러리                  |
|----------------|-----------------------------------|----------------------------------------|
| 하드웨어 제어 AI | 실험 장비·로봇 작업 지시 및 상태 모니터링 | OCTOPUS (고수준 명령),ROS2(저수준 명령), Isaac Sim(시뮬레이션)|
| 후보군 발굴 AI | FlavorDB 등 기반 궁합 예측           | GNN(Graph Neural Networks), Joint Embedding |
| 실험 설계 최적화 AI| Search Space 축소, 최적 조합 제안    | Bayesian Optimization, LangGraph      |
| 후분석 AI      | 센서 데이터 해석, 결과 기록           | Data Analysis  |

- ROS2 : Robot Operating System 2, 로봇의 각종 부품(센서, 모터, 카메라)들이 서로 대화할 수 있게 해주는 공용 언어
- LLM을 활용해 하드 코딩 없이 자연어 실험 지침→로봇 제어 명령으로 번역
- 각 하드웨어 통신 프로토콜 통합 제어 소프트웨어 제공(ROS2 기반)  
- 실험 결과($y$)를 반영해 목적함수 업데이트 및 다음 실험 설계—특히 **베이지안 최적화(BO) 도입**으로 무작위 샘플링 대비 압도적 효율을 낼 수 있음  
- 실험 실패(예: "농도 초과로 센서 임계치 발생")의 원인을 AI가 장비 로그→자연어로 해석할 수 있도록 데이터 파이프라인/LLM 연계 필요  

---

## 데이터셋 전략

- **TGSC, FlavorDB**: 분자 수준의 맛/향 화합물 데이터로 AI가 **'이론적 궁합'**을 학습
    - pubChemID 등 식별자를 활용해 양방향 연동 구축
    - 저작권 이슈 방지를 위해 원본 Data 대신 데이터 분포를 학습해 합성(Synthetic) Dataset 사용 코어 전략 필요
- **식품안전나라(식품첨가물 API)**: 실제 상용 제품 레시피 정보(인허가번호 등)로 현실 조건 반영, 레시피 신뢰도 향상
    - 사내 생산(주식회사 이음) 데이터와 연계, 미공개 원료 추론 실험 추진

Dataset 전체를 효율적으로 관리·연결하고, LLM·AI가 활용하기 쉬운 구조(예: SQL/NoSQL/GraphDB)로 표준화 구축 필요

---

## 예상되는 문제점 및 현실 조언

- **교차 오염 방지**: 실험 간 로봇 자동 세척 시스템(Arm/Tool Cleaning)을 하드웨어 설계 단계에서 반드시 내재화할 것(주당 500개 이상 데이터 생성 목표 달성에 '크리티컬')
- 실험실 온도·환경 자동 제어
- 고체 시료 자동 디스펜싱의 한계: 변수 복잡성 상 높은 난이도로 초반에는 액체 시료로 실험하는 것이 합리적
- Sim-to-Real 시 ROS2/DDS 통신 지연 등 시스템 레이턴시를 최소화하기 위한 세팅 필요
- 자동 피펫팅 시스템(Liquid Handler) 운영 시 일회용 팁 가격 고려 필요 
- 

---

## 기술 검토 체크리스트

- [ ] **ROS2 버전**: Isaac Sim 2023.x 이상 → ROS2 Humble 호환성이 가장 우수
- [ ] **통신 레이턴시 최적화**: DDS 세팅 최적화
- [ ] **데이터 파이프라인**: 센서 Raw Data → 인메모리 DB(Redis 등) → 실시간 DB 적재 구조 권장
- [ ] **실험 Fail 로그→AI 해석 파이프라인**: LLM·AI가 해석 가능한 자연어 로그 자동 변환

---

### Self-Driving Lab의 기본 구조

|구성 요소           | 설명                                                         |
|-------------------|-------------------------------------------------------------|
| Self-Driving Lab  | AI가 스스로 실험을 설계·수행·분석하는 자율 연구 환경             |
| AI Brain          | AI 에이전트가 실험 계획과 판단을 수행                          |
| Control Layer     | 장비 제어를 담당하는 ROS2/PLC 인터페이스                       |
| Feedback Loop     | 결과를 바탕으로 실험을 반복·개선                               |
| Data Layer        | 모든 실험 데이터를 저장하고 시각화                              |

---

#### 대표 실험 장비 예시

- 웰 플레이트
- 피펫팅 툴(Liquid Handler)
    https://www.selectscience.net/product/ot-2

- 원심관·시험관
- 전자코(e-nose)/전자혀(e-tongue)
- 로봇팔

https://www.selectscience.net/product/ot-2


sample Design

youtube.com/watch?time_continue=176&v=oq4Xbr3FDD0&embeds_referring_euri=https%3A%2F%2Fwww.mt.com%2F&embeds_referring_origin=https%3A%2F%2Fwww.mt.com&source_ve_path=MTM5MTE3LDEzOTExNywxMzkxMTcsMjM4NTE

