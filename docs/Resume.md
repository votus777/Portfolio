---
icon: lucide/user-round
--- 

# A Doer who does things with Data 
> 데이터 기반 AI 서비스의 시작과 끝을 설계하는 데이터 프로덕트 엔지니어

## 🚀 5가지 핵심 역량
| 주체성 | 빌더 마인드셋 | 조력자형 | 호기심·학습 탄력성 | 불확실성 내성 |
|:---:|:---:|:---:|:---:|:---:|
| ✓ | ✓ | ✓ | ✓ | ✓ |

- **주체성:** 문제 정의부터 배포까지 전 과정을 스스로 리드
- **빌더 마인드셋:** 이론에 머물지 않고 실제 동작하는 MVP를 빠르게 구축
- **불확실성 내성:** 정답이 정해지지 않은 상황에서도 끊임없이 탐색하고 해답을 찾아내는 능력

---

## 💼 Work Experience

| 기간 | 소속/회사 | 역할 및 주요 성과 |
|:---|:---|:---|
| **2025.05 ~** | **(주) 헤렘** | **사업기획팀 연구원** |
| 2022.03 ~ 2024.02 | DSIL (Hanyang Univ.) | **M.S Researcher** (지도교수: Casey C. Bennett[^1]) |
| 2021.06 ~ 2021.12 | Episci. Inc | **Data Engineer** (데이터 파이프라인 구축) |
| 2019.06 ~ 2019.09 | Cologne Game Lab (CGL) | **Game Designer** |


[^1]: https://www.caseybennett.com/


---

## 🎓 Education

- **한양대학교(서울) 데이터사이언스 석사** (2022.03 ~ 2024.02)
- **한양대학교(서울) 스포츠사이언스 학사** (2014.03 ~ 2021.08)
  - 부전공: 미래인문학융합전공

---

## 🛠️ Main Projects

- **실시간 공공데이터 기반 프롭테크(PropTech) MVP 개발 및 시장 검증**
  - **핵심 기술:** Python, Supabase, ML Modeling (Time-series), Public API Integration
    - 데이터 자동화: 국토교통부 API를 연동하여 수도권 아파트 실거래 데이터 수집 및 전처리 파이프라인 구축
    - 예측 모델링: 시계열 계약 데이터를 분석하여 매물 발생 시점 및 계약 규모를 예측하는 ML 알고리즘 개발
    - 서비스 런칭: 예측 모델을 적용한 실시간 플랫폼([when-move-in.com](https://when-move-in.com))을 직접 기획·운영하며 시장 검증 수행

___

- **Beer Flavor Analysis: 화학 성분-관능 데이터 Joint Embedding 및 역추론 모델 개발**
  - **핵심 기술:** PyTorch, Dual AutoEncoder, Joint Embedding, ONNX, Streamlit
    - 맥주의 화학적 수치(ABV, IBU 등)와 관능 데이터(Flavor, Aroma)를 동일 잠재 공간(Latent Space)에 투영하는 멀티모달 모델 설계
    - 역설계(Inverse Design) 알고리즘: 목표 향미 프로필에 적합한 최적의 화학 조성을 제안하는 양방향 매핑 구현
    - 배포 최적화: PyTorch 모델을 ONNX로 변환하여 모델 용량 50% 절감 및 Streamlit 기반 실시간 향미 시뮬레이션 웹 서비스 배포

___

- **텍스트 기반 향료 레시피 생성 AI 솔루션 구축 | (Joomidang 사내 해커톤 초청)**
  - **핵심 기술:** LLM (Intent Extraction), RAG (AromaDB/FlavorDB), SLSQP Optimization
    - End-to-End 파이프라인: 사용자의 추상적 묘사를 LLM으로 분석하고, 도메인 지식(RAG)을 결합하여 정밀한 향료 배합비로 변환
    - 수치 최적화: SLSQP 알고리즘을 도입하여 화학적 제약 조건 및 조향 가이드라인을 100% 만족하는 최적 레시피 산출
    - 검증: 생성된 레시피로 100µL 분량의 **실제 향수를 제조 및 테스트**하여 모델의 실무 적용 가능성 입증

___ 
 

- **AI 성격이 인간의 행동 요인에 미치는 영향 분석 | (석사 학위 논문)**
    - 가상 협업 환경에서 AI 에이전트와 유저 간의 상호작용 데이터를 수집하는 실험 설계 및 파이프라인 구축
    - HCI 인사이트: AI와 유저 간의 심리적·물리적 거리(Proximity)가 행동 무작위성에 미치는 상관관계 입증 ($r = -0.5024$)
    - 대외 인정: 연구 결과를 바탕으로 IJHCI(IF: 4.7) 국제 저널에 논문 게재 및 학술적 기여 인정

___ 

- **DSKUS Global Lab: 효율적 개발 원조(ODA) 데이터 분석 협업** | (주한미국대사관 후원)
    - 글로벌 협업: 한양대·Indiana Univ·DePaul Univ과 공동으로 데이터 사이언스 프로젝트 수행
    - 주요 성과: 'Well-targeted ODA' 주제의 효율적 개발 원조를 위한 인터랙티브 시각화 대시보드 구축
    - 프로젝트 설명: [DSKUS Dashboard](https://cds.cdm.depaul.edu/dskus/)

___ 

- **차량용 디스플레이 생산 품질 개선 모델 개발 (LG Aimers 해커톤)** | 
  - **핵심 기술:** Feature Engineering, Data Quality Validation, Ensemble Learning
    - 제조 공정 내 실시간 품질 데이터를 분석하여 불량률을 최소화하는 최적화 모델 개발
    - 체계적인 전처리 및 검증 프로세스로 모델 신뢰성을 확보하여 3,000명의 참가자 중 상위 3% 이내 기록 (오프라인 본선 진출)

---

## 📝 Publications

- **Exploring Factors Influence Human Behavior of AI Personality in a Virtual Collaborative Environment**
*Master's Thesis, Hanyang University (2023)*
- **Cognitive Shifts in Bilingual Speakers Affect Speech Interactions with Artificial Agents**
  - *International Journal of Human–Computer Interaction (IJHCI), 2023*
  - **IF: 4.7 / Acceptance Rate: 27%**

---

## 📞 Contact & Links
- **GitHub:** [https://github.com/votus777]
- **Email:** [chohansae@gmail.com]