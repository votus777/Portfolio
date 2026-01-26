---
icon: lucide/flask-conical
---

# Self-Driving Laboratories for Flavor Discovery

**로보틱스 기반 자동 디스펜싱 및 조합 시스템 설계**

Obj01. 조합 결과 데이터 수집

obj02. 시제품 탐색 공간 축소


#### Schematic for the autonomy levels of SDL
![model](https://github.com/user-attachments/assets/971e83a9-9d49-4afe-ad76-65b9d9837f90)

-> 
Search space: 시험 시료들을 배치 (Human)
Experiments selection: 알고리즘에 따른 시료 조합 탐색 (AI)

Level2를 목표

중앙 집중형(Workstation-based) 


## Hardware
상업용 하드웨어 vs 3D 오픈소스 하드웨어 

(1) 디스펜싱 유닛 (Dispensing Unit)
(2) 조합 및 교반 유닛 (Mixing Unit)
(3) 운송 및 파지 (Transportation & Gripping)
(4) 계량(Weighing) 및 보정 (Calibration) 유닛

## Software
LLM을 이용해 하드 코딩 없이 로봇 제어 명령으로 번역

각 하드웨어의 통신 프로토콜을 통합 및 제어하는 소프트웨어


- 후보군 발굴 AI (기존 데이터를 통한 타겟 예측)
- 실험 설계 최적화 AI 
- 데이터 후분석 AI 

Dataset

- TGSC Information System
    pubChemID 를 통해 FlavorDB 혹은 타 DB와 연결가능 
FEMA No.


- FlavorDB : CC BY-NC-SA 4.0 (크리에이티브 커먼즈 저작자표시-비영리-동일조건변경허락 4.0 국제) 라이센스 문제를 피하기 위해 원본 데이터셋을 그대로 쓰는 것이 아닌 해당 데이터의 분포를 학습하여 생성된 합성 데이터셋 사용 필요



- ES식품원료 

식품(첨가물)품목제조보고(원재료) API 
실질적인 제품 생산은 같은 건물에 있는 "주식회사 이음"이 담당
인허가번호 -> 식품 원료 추론 가능 
FlavorDB와 연결하여 미공개 원료 파악 테스트 


## 예상되는 문제
교차 오염
실험실 온도 제어
고체 디스펜싱은 물리적 변수가 많아 비추천


### Self-Driving Lab의 기본 구조
|구성 요소           | 설명                                                         |
|-------------------|-------------------------------------------------------------|
| Self-Driving Lab  | AI가 스스로 실험을 설계·수행·분석하는 자율 연구 환경             |
| AI Brain          | AI 에이전트가 실험 계획과 판단을 수행                          |
| Control Layer     | 장비 제어를 담당하는 ROS2/PLC 인터페이스                       |
| Feedback Loop     | 결과를 바탕으로 실험을 반복·개선                               |
| Data Layer        | 모든 실험 데이터를 저장하고 시각화                              |




웰 플레이트
피펫팅 툴(Liquid Handler)
원심관, 시험관
전자코,혀 
로봇팔 

	

sample Design

youtube.com/watch?time_continue=176&v=oq4Xbr3FDD0&embeds_referring_euri=https%3A%2F%2Fwww.mt.com%2F&embeds_referring_origin=https%3A%2F%2Fwww.mt.com&source_ve_path=MTM5MTE3LDEzOTExNywxMzkxMTcsMjM4NTE

