---
icon: lucide/languages
---
# Bilingual AI Interaction

## 이중언어 사용자의 인지 변화가 AI 에이전트와의 음성 상호작용에 미치는 영향 (Cognitive Shifts in Bilingual Speakers)

## **TL;DR:**  
> 이중언어 화자는 사용하는 언어(한국어/영어)에 따라 인지 패러다임이 변화하며, 이는 AI 에이전트와의 음성 상호작용(발화 패턴, 감성, 인지 평가)에 직접적 영향을 미침.   
> 같은 AI라도 유저 배경(단일/이중언어)에 따라 응답 및 행동이 달라진다는 사실을 실험적 데이터 및 NLP/감성분석 기반으로 입증.

## 핵심 목적
**언어 상대성(Linguistic Relativity) 이론을 바탕으로, 이중언어 화자가 사용하는 언어에 따라 인지 패러다임이 어떻게 변화하며, 이것이 AI 에이전트와의 상호작용(음성 패턴, 감성, 인지적 평가)에 어떤 영향을 주는지 규명**

### 주요 기능
1. [x] 한국어/영어 이중언어(Bilingual) 및 단일언어(Monolingual) 비교 실험 설계
2. [x] DST 가상 환경 내 이중언어 대응 Social AI 에이전트 개발
3. [x] 코드 스위칭(Code-switching) 상황에서의 언어적 교차 효과(Crossover effects) 분석
4. [x] 음성 데이터 기반 NLP 분석 (발화 빈도, 중단 횟수, 감성 분석)
5. [x] 사용자 경험 및 사회적 실재감(Social Presence) 정량 측정

### 연구 방법론 - 멀티모달 분석
- **발화 Diarization**: Google Cloud API를 이용한 유저-AI 음성 분리 및 타임스탬프 추출
- **턴테이킹(Turn-taking) 분석**: Inter-pausal Unit(IPU) 분석을 통한 상호 중단(Interruption) 빈도 계산
- **감성 분석(Sentiment Analysis)**: VADER 및 한국어 전용 감성 사전을 활용한 발화 긍정/부정 수치화


## 데이터셋

| 항목         | 내용                                                                 |
|--------------|---------------------------------------------------------------------|
| 실험 대상    | 총 40명 (이중언어 20명, 한국어 단일 10명, 영어 단일 10명)               |
| 선정 기준    | 영어(TOEIC B2 이상), 한국어(TOPIK C1 이상) 숙련자                      |
| 분석 데이터  | 30분간의 게임 세션 녹화본(OBS), 실시간 음성 스크립트, HRI 설문 데이터 |
| 분석 도구    | Python, R, Microsoft Azure ASR, VADER Sentiment                      |

| 분석 지표 (Metric) | 설명 | 주요 발견 (Key Finding) |
|--------------------|------|-------------------------|
| **Utterance Count**| 발화 횟수 | 이중언어자는 한국어 사용 시에도 영어 화자와 유사한 발화 패턴을 보임 |
| **Interruption %** | 대화 중단 비율 | 이중언어 상황에서 AI의 유저 발화 중단 빈도가 유의미하게 변화함 |
| **Godspeed Scale** | 로봇 인지 평가 | 이중언어자는 단일언어자보다 AI의 지능/호감도를 더 낮게 평가하는 경향 |

## 주요 연구 결과
<div align="center">

<img src="https://github.com/user-attachments/assets/bbb89fbc-32ea-4e6a-9907-54890b953e55" alt="bilingual cognitive shift result" width="450"/>

<br/>

<img src="https://github.com/user-attachments/assets/d287a0ce-68a0-434c-ad8f-84e89fe43361" alt="bilingual cognitive shift result" width="600"/>

</div>

> bilingual cognitive shift result

### 1. 언어에 따른 "인지적 이동(Cognitive Shifts)" 입증
- 이중언어 화자는 모국어(한국어)를 사용할 때도 단일언어 화자와 다른 음성 패턴을 보이며, 이는 제2외국어(영어)의 인지 구조가 모국어 상호작용에 전이됨을 시사함.

### 2. AI 에이전트의 피드백 변화
- 동일한 알고리즘으로 프로그래밍된 AI임에도 불구하고, 상대 유저의 언어적 배경(단일 vs 이중)에 따라 AI의 발화 행동 및 턴테이킹 성공률이 동적으로 변화함.

## Limitation
- **표본의 다양성**: 대학생 위주의 표본으로 인한 일반화의 한계.
- **비언어적 요소**: 표정, 제스처 등 비언어적 멀티모달 데이터의 통합 분석 필요.
- **상황적 제약**: 게임 환경 외의 실제 임상/일상 환경에서의 검증 과제.

## 참고 문헌
> Bennett, C. C., Cho, H., et al. "Cognitive Shifts in Bilingual Speakers Affect Speech Interactions with Artificial Agents." International Journal of Human–Computer Interaction (2023).
