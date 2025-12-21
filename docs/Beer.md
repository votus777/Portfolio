---
icon: lucide/beer
--- 

## Joint Embedding 기반 맥주 화학-관능 양방향 매핑 시스템

![joint_embedding]([https://user-images.githubusercontent.com/xxxx/xxxx.png](https://private-user-images.githubusercontent.com/51744036/528993829-f1521a21-b22f-4fca-acff-d72e3d77cf2c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjYzMzk1OTAsIm5iZiI6MTc2NjMzOTI5MCwicGF0aCI6Ii81MTc0NDAzNi81Mjg5OTM4MjktZjE1MjFhMjEtYjIyZi00ZmNhLWFjZmYtZDcyZTNkNzdjZjJjLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjIxVDE3NDgxMFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTY4YzMzYzI5Njg0Njc3NGU1Y2U4MzdiMjgxNTAzY2Y2NjFlZmMwMGEwMzc2MzkxNGM4NTQ3MzYxMmQwNjc4MGMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.HwHhuVXFWLdTgStOAmZBAqPgWzbx5vr3PH0KRR5NnkI))



## 모델 훈련 및 평가

| 예측 방향         | 평균 R²    | 중앙값 R²  | MSE     |
|------------------|-----------|-----------|---------|
| 화학 → 관능 예측  | 0.7994    | 0.8466    | 0.2006  |
| 관능 → 화학 역추론 | 0.7851    | 0.7883    | 0.2149  |


## 모델 배포 
 - ONNX   
 PyTorch 모델 → ONNX 변환  
 - 서로 다른 머신러닝 프레임워크(예: PyTorch, TensorFlow) 간에 모델을 쉽게 교환하고 배포할 수 있도록 만든 개방형 표준 포맷  
 - 특정 프레임워크 설치 없이도 여러 환경(클라우드, 엣지 디바이스)에서 빠르게 추론을 수행  


## 예시 시나리오

### 1. 입력 화학 조성

| 화합물                | 수치   |
|-----------------------|--------|
| ethyl_acetate         | +2.00  |
| ethanol               | +0.00  |
| ethyl_octanoate       | +1.50  |
| ethyl_phenylacetate   | +0.50  |
| lactic_acid           | +0.00  |
| protein               | +0.00  |

---

### 2. 예측된 주요 관능 특성

| 관능 특성              | 예측값   |
|------------------------|---------|
| aroma_hops_sum         | +2.091  |
| palate_anise           | -0.064  |
| palate_pineapple       | -0.061  |
| palate_aftertaste      | +0.061  |
| aroma_mango            | -0.059  |
| palate_grainy          | +0.054  |
| aroma_buttery          | -0.053  |
| palate_candy           | -0.053  |
| palate_medicinal       | +0.047  |
| taste_hay              | -0.046  |

---

### 3. 유사한 실제 맥주 찾기 (Validation)

| 순위 | 맥주명                      | 브랜드       | 유사도   | 대표 특성                                      |
|-----|------------------------------|------------|---------|------------------------------------------------|
| 1   | Jupiler 0,0% 25 CL Fles      | Jupiler    | 0.7228  | taste_flour, aroma_flour, aroma_cabbage        |
| 2   | nan                          | nan        | 0.6706  | palate_horse, taste_solvent, taste_carbonation |
| 3   | Dorée                        | Chimay     | 0.6645  | taste_acetaldehyde, taste_bread, aroma_coriander|



## 참고 문헌
> Schreurs, Michiel, et al. "Predicting and improving complex beer flavor through machine learning." Nature Communications 15.1 (2024): 2368.


