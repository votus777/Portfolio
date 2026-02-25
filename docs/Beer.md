---
icon: lucide/beer
--- 

# Beer 

## 맥주 화학-관능 공동 임베딩 모델 (Joint Embedding Model)

## **TL;DR:**  
> 맥주 화학 조성(ABV 등 수치)과 관능 특성(맛, 향, 질감 등)을 하나의 잠재 공간에 공동 임베딩하는 Dual AutoEncoder 모델 개발.  
> 양방향으로, (1) 화학 데이터로 맥주 맛/향을 예측하거나, (2) 원하는 맛/향을 주면 필요한 화학 조성을 역추론 가능  
> ONNX로 최적화해 웹에서도 실시간 탐색/시뮬레이션이 가능. 벨기에 맥주 250종 데이터 사용, R² ≈ 0.8

## 핵심 목적
**화학적 조성 ↔ 관능 특성(taste_, aroma_, palate_) 양방향 변환 가능한 공동 잠재 공간 생성**

### 주요 기능
1. [x] 화학 데이터 → 관능 특성 예측
2. [x] 관능 특성 → 필요한 화학 조성 역추론
3. [x] 공동 잠재 공간에서 상호 해석 가능
4. [x] 목표 맛 기반 맥주 설계

### 모델 아키텍처 - Dual AutoEncoder
- **Chemical Encoder**: 화학 데이터 → Latent Space (512dim)
- **Sensory Encoder**: 관능 데이터 → Latent Space (512dim)
- **Chemical Decoder**: Latent Space → 화학 데이터 재구성
- **Sensory Decoder**: Latent Space → 관능 데이터 재구성

### 손실 함수
1. **재구성 손실**: 입력 복원 정확도
2. **정렬 손실**: 같은 맥주의 화학/관능 임베딩 거리
3. **교차 재구성 손실**: 화학↔관능 변환 정확도


## 데이터셋

| 항목         | 내용                                                                 |
|--------------|---------------------------------------------------------------------|
| 데이터 소스  | Predicting and improving complex beer flavor through machine learning (2024)                           |
| 전체 샘플    | 250개 벨기에 맥주                                                      |
| 화학 변수    | 230개                                                      |
| 관능 변수    | 184개                                                    |
| 메타데이터   | beer_name, brand, Description 등                                    |


| 구분         | 카테고리      | 예시                                        | 설명/개수            |
|--------------|---------------|---------------------------------------------|----------------------|
| 화학 변수    | 휘발성 화합물 | ethyl_acetate, ethyl_octanoate              | 과일향, 꽃향 에스터  |
| 화학 변수    | 알코올        | ethanol, isoamyl_alcohol                    | 알코올 농도          |
| 화학 변수    | 산            | lactic_acid, acetic_acid                    | 신맛 성분            |
| 화학 변수    | 페놀          | phenylethyl_alcohol                         | 향미 화합물          |
| 화학 변수    | 기타          | pH, bitterness, protein                     | 물리화학적 특성      |
| 관능 변수    | Aroma (향)    | aroma_fruity, aroma_floral, aroma_hoppy     | 후각             |
| 관능 변수    | Taste (맛)    | taste_sweet, taste_bitter, taste_sour       | 미각              |
| 관능 변수    | Palate (질감) | palate_body, palate_smooth, palate_creamy   | 목넘김             | 



## 모델 구조 
![model](https://github.com/user-attachments/assets/f6e3de62-a596-4ffd-abfe-efd20bfeb490)

## 손실 함수

```python hl_lines="1" title="Loss Function"

def compute_joint_loss_beer(x, y, z_x, z_y, x_recon, y_recon, x_from_y, y_from_x,
                            alpha=1.0, beta=2.0, gamma=0.5):
    """
    - 화학 데이터: 이상치 가능성 → Smooth L1
    - 정렬: 시각화 중요 → Cosine
    - 교차: 정확한 변환 → MSE
    """
    recon_loss_x = nn.SmoothL1Loss()(x_recon, x)
    recon_loss_y = nn.SmoothL1Loss()(y_recon, y)
    recon_loss = (recon_loss_x + recon_loss_y) / 2
    
    alignment_loss = 1 - F.cosine_similarity(z_x, z_y, dim=1).mean()
    
    cross_recon_loss_x = nn.MSELoss()(x_from_y, x)
    cross_recon_loss_y = nn.MSELoss()(y_from_x, y)
    cross_recon_loss = (cross_recon_loss_x + cross_recon_loss_y) / 2
    
    total_loss = alpha * recon_loss + beta * alignment_loss + gamma * cross_recon_loss
    
    return total_loss, recon_loss, alignment_loss, cross_recon_loss

```


## 모델 훈련 및 평가

| 예측 방향         | 평균 R²    | 중앙값 R²  | MSE     |
|------------------|-----------|-----------|---------|
| 화학 → 관능 예측  | 0.7994    | 0.8466    | 0.2006  |
| 관능 → 화학 역추론 | 0.7851    | 0.7883    | 0.2149  |


## Joint Embedding 시각화

![joint](https://github.com/user-attachments/assets/491f4c57-510c-44e5-8e21-8d875c6a1281)

## 모델 배포 
 - ONNX   
 PyTorch 모델 → ONNX 변환  
 - 서로 다른 머신러닝 프레임워크(예: PyTorch, TensorFlow) 간에 모델을 쉽게 교환하고 배포할 수 있도록 만든 개방형 표준 포맷  
 - 특정 프레임워크 설치 없이도 여러 환경(클라우드, 엣지 디바이스)에서 빠르게 추론을 수행  

- 파일 크기 비교:  
   PyTorch (.pth): 15.43 MB  
   ONNX (.onnx):   7.64 MB  
   감소율: 50.5%  


## 웹페이지

![web](https://github.com/user-attachments/assets/93690dd9-146a-495a-bcf9-e9874674a352)

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

> 원본데이터셋의 Beer_id는 EAN(European Article Number)를 의미

| 순위 | 맥주명                      | 브랜드       | 유사도   | 대표 특성                                      |
|-----|------------------------------|------------|---------|------------------------------------------------|
| 1   | Jupiler 0,0% 25 CL Fles      | Jupiler    | 0.7228  | taste_flour, aroma_flour, aroma_cabbage        |
| 2   | nan                          | nan        | 0.6706  | palate_horse, taste_solvent, taste_carbonation |
| 3   | Dorée                        | Chimay     | 0.6645  | taste_acetaldehyde, taste_bread, aroma_coriander|


## Limitation
    - Chemical -> Sensory 변환과 달리 Sensory -> Chemical는 1:1 매칭이 되지 않는 비가역적인 관계  
    - 현재 학습된 Latent Space는 데이터셋의 분포에 한정됨
    - 얀 르쿤이 제시한 JEPA(Joint-Embedding Predictive Architecture)로 확장 가능 


## 참고 문헌
> Schreurs, Michiel, et al. "Predicting and improving complex beer flavor through machine learning." Nature Communications 15.1 (2024): 2368.

