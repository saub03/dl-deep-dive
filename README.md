# dl-deep-dive

> **딥러닝을 '사용하는 것'에서 '이해하고, 구현하고, 실험하고, 연구하는 것'으로.**
>
> 교재와 원 논문을 나란히 학습하고, 축소 재현 실험을 거쳐 스스로 연구 질문을 찾기 위한 학습·연구 저장소.

## 목차

1. [프로젝트 개요 및 목표](#1-프로젝트-개요-및-목표)
2. [학습 원칙과 완료 기준](#2-학습-원칙과-완료-기준)
3. [학습 체크리스트](#3-학습-체크리스트)
4. [학습 기록·프로젝트·산출물 링크](#4-학습-기록프로젝트산출물-링크)
5. [교재·논문·아티클 라이브러리](#5-교재논문아티클-라이브러리)
6. [연구 주제 탐색 및 실험 규칙](#6-연구-주제-탐색-및-실험-규칙)
7. [저장소 구조 및 문서 템플릿](#7-저장소-구조-및-문서-템플릿)

---

## 1. 프로젝트 개요 및 목표

**프로젝트명:** `dl-deep-dive`  
**학습 방법:** 교재 이해 → 논문 정독 → 핵심 알고리즘 구현 → 비교 실험 → 학습 정리 → 연구 질문 도출  
**핵심 교재:** 『밑바닥부터 시작하는 딥러닝』 **1·2·4·5·6권**, *Hands-On Machine Learning with Scikit-Learn and PyTorch*  
**범위:** 딥러닝 기초, CNN, NLP, Transformer, LLM, RL, 생성 모델, 멀티모달, 학습 효율화  
**최종 지향점:** 학교의 GPU 자원을 활용한 **재현 가능한 독립 연구 프로젝트**

### 목표

- [ ] 역전파·최적화·일반화·주요 신경망 구조를 수식과 코드로 설명할 수 있다.
- [ ] PyTorch로 데이터 준비부터 학습·평가·모델 저장까지 독립적으로 구현한다.
- [ ] 대표 논문을 읽고 **문제 → 핵심 기여 → 실험 설계 → 한계**를 요약한다.
- [ ] 주요 아키텍처를 작은 규모로 구현하거나 기존 구현의 핵심 부분을 재현한다.
- [ ] 여러 연구 분야를 탐색하고 집중 연구할 주제와 가설을 선정한다.
- [ ] Baseline·비교 실험·Ablation을 포함한 연구 결과를 문서화한다.
- [ ] 코드, 환경, 설정, 평가 방법을 공개 가능한 수준으로 정리한다.

> **학습 범위 원칙:** '밑시딥 3권'은 정규 학습 범위에서 제외한다. 자동미분 프레임워크 내부 구현이 필요한 경우에만 선택적으로 참고한다. 『핸즈온』 1~8장은 이미 익숙한 머신러닝 개념의 부족한 부분을 보충할 때 사용한다.

## 2. 학습 원칙과 완료 기준

### 자료별 학습 방법

| 자료 | 목표 | 완료 판단 기준 |
|---|---|---|
| 교재 | 원리·직관·선수지식 정립 | 핵심 수식을 설명하고 예제를 직접 수정할 수 있음 |
| 논문 | 학술적 문제 정의와 기여 이해 | 문제, 방법, Baseline, 결과, 한계를 자신의 언어로 정리 |
| 구현 | 모델과 알고리즘 내부 이해 | 작은 입력에 대해 동작 검증, 최소 1개 테스트 작성 |
| 실험 | 주장 검증 및 비교 | 동일 데이터·평가 기준으로 Baseline과 비교, 결과 기록 |
| 보고서 | 지식 정착 및 연구 질문 발굴 | 관찰 결과, 실패 사례, 후속 가설 1개 이상 포함 |

### 체크박스 운영 규칙

- **[ ] → [x]**: *실제로 수행하고 결과물을 남긴 경우*에만 체크한다.
- 한 논문을 **읽는 것**과 **실험으로 검증하는 것**은 별개 작업으로 관리한다.
- `**[핵심]**`은 우선 완료할 항목, `**[확장]**`은 관심 분야 탐색용 항목이다.
- 모든 논문을 정밀 재현할 필요는 없다. 각 주제에서 **대표 논문을 최소 한 편 깊게** 다룬다.
- 아래 순서는 *개념 의존성에 따른 권장 순서*이며, **학습 기간이나 마감일을 지정하지 않는다.**

---

## 3. 학습 체크리스트

### 3.1 딥러닝 기초: 역전파·최적화·CNN

**연계 교재:** 밑시딥 1권 · 핸즈온 9~12장, 부록 A(자동미분)

#### 신경망과 역전파

- [ ] **[핵심]** 밑시딥 1권 4~5장, 핸즈온 9~10장: 손실함수·수치미분·계산 그래프·오차역전파 복습
- [ ] **[핵심]** [Learning Representations by Back-Propagating Errors](https://doi.org/10.1038/323533a0) 논문 학습
- [ ] Affine, ReLU, SoftmaxWithLoss 계층의 Forward/Backward를 NumPy로 구현
- [ ] 수치미분과 역전파 기울기를 비교하는 Gradient Check 실습
- [ ] 학습 정리 보고서 작성: 연쇄법칙, 계산 그래프, Gradient Check 오차

#### 최적화와 일반화

- [ ] **[핵심]** 밑시딥 1권 6장, 핸즈온 11장: SGD, Momentum, Adam, 초기화, 정규화 학습
- [ ] **[핵심]** [Adam: A Method for Stochastic Optimization](https://arxiv.org/abs/1412.6980) 논문 학습
- [ ] **[확장]** [Batch Normalization](https://arxiv.org/abs/1502.03167) 논문 학습
- [ ] **[확장]** [Dropout](https://jmlr.org/papers/v15/srivastava14a.html) 논문 학습
- [ ] **[확장]** [Super-Convergence](https://arxiv.org/abs/1708.07120) 논문 학습
- [ ] 동일 모델·데이터에서 SGD, Momentum, Adam의 수렴 속도와 검증 손실 비교
- [ ] PyTorch 학습 파이프라인 구현: DataLoader, train/validation/test, 체크포인트, 시드, 지표 기록
- [ ] 학습 정리 보고서 작성: 옵티마이저·학습률·과적합·실험 결과

#### CNN과 잔차 연결

- [ ] **[핵심]** 밑시딥 1권 7장, 핸즈온 12장: 합성곱·풀링·CNN 구조 학습
- [ ] **[확장]** [AlexNet](https://proceedings.neurips.cc/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html) 논문 학습
- [ ] **[핵심]** [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385) 논문 학습
- [ ] CNN과 Residual Block을 PyTorch로 구현
- [ ] 일반 CNN과 ResNet 계열의 학습 곡선·기울기 흐름 비교
- [ ] 학습 정리 보고서 작성: CNN 특징, 잔차 연결의 역할, 실험 결과

### 3.2 NLP의 발전: 단어 표현·RNN·Attention·Transformer

**연계 교재:** 밑시딥 2권 · 핸즈온 13~15장

#### Word Embedding

- [ ] **[핵심]** 밑시딥 2권 2~4장: 말뭉치, 분산 표현, CBOW, Skip-gram, Negative Sampling 학습
- [ ] **[핵심]** [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/abs/1301.3781) 논문 학습
- [ ] **[확장]** [GloVe](https://aclanthology.org/D14-1162/) 논문 학습
- [ ] 단어 임베딩 학습 후 유사도·유추 연산 실습
- [ ] 학습 정리 보고서 작성: 분산 표현의 가정과 한계

#### RNN, LSTM, Seq2Seq

- [ ] **[핵심]** 밑시딥 2권 5~7장, 핸즈온 13~14장: RNN, LSTM, Encoder–Decoder 학습
- [ ] **[확장]** [Generating Sequences with Recurrent Neural Networks](https://arxiv.org/abs/1308.0850) 논문 학습
- [ ] **[핵심]** [Long Short-Term Memory](https://www.bioinf.jku.at/publications/older/2604.pdf) 논문 학습
- [ ] **[핵심]** [Sequence to Sequence Learning with Neural Networks](https://arxiv.org/abs/1409.3215) 논문 학습
- [ ] 작은 시퀀스 문제에서 RNN/LSTM/Seq2Seq 구현 및 성능 비교
- [ ] 학습 정리 보고서 작성: 장기 의존성, 기울기 소실, Encoder–Decoder

#### Attention에서 Transformer까지

- [ ] **[핵심]** 밑시딥 2권 8장, 핸즈온 14~15장: Attention·Transformer 학습
- [ ] **[핵심]** [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473) 논문 학습
- [ ] **[핵심]** [Attention Is All You Need](https://arxiv.org/abs/1706.03762) 논문 정독
- [ ] Bahdanau Attention과 Scaled Dot-Product Attention을 직접 구현
- [ ] Multi-Head Attention, Positional Encoding, Masking 구현 및 Tensor Shape 검증
- [ ] 기본 Seq2Seq와 Attention-Seq2Seq 비교, Attention 가중치 시각화
- [ ] 작은 Decoder-only Transformer를 학습해 텍스트 생성
- [ ] 학습 정리 보고서 작성: RNN→Attention→Transformer로 발전한 이유

### 3.3 강화학습: 가치 기반에서 정책 최적화까지

**연계 교재:** 밑시딥 4권 · 핸즈온 19장

#### 강화학습 기초와 가치 기반 방법

- [ ] **[핵심]** 밑시딥 4권 1~6장: MDP, 벨만 방정식, Monte Carlo, TD, Q-Learning 학습
- [ ] **[확장]** [Finite-time Analysis of the Multiarmed Bandit Problem](https://link.springer.com/article/10.1023/A:1013689704352) 논문 학습
- [ ] **[핵심]** [Q-learning](https://link.springer.com/article/10.1007/BF00992698) 논문 학습
- [ ] GridWorld에서 Dynamic Programming/TD/Q-Learning 구현
- [ ] 학습 정리 보고서 작성: 가치함수, 탐색·활용, Bellman Update

#### Deep RL 및 정책 경사

- [ ] **[핵심]** 밑시딥 4권 7~10장 및 핸즈온 19장: DQN, REINFORCE, Actor-Critic, PPO 학습
- [ ] **[핵심]** [Playing Atari with Deep Reinforcement Learning](https://arxiv.org/abs/1312.5602) 논문 학습
- [ ] **[확장]** [Rainbow](https://arxiv.org/abs/1710.02298) 논문 학습
- [ ] **[핵심]** [Simple Statistical Gradient-Following Algorithms for Connectionist Reinforcement Learning](https://link.springer.com/article/10.1007/BF00992696) 논문 학습
- [ ] **[확장]** [Asynchronous Methods for Deep Reinforcement Learning](https://arxiv.org/abs/1602.01783) 논문 학습
- [ ] **[핵심]** [Proximal Policy Optimization Algorithms](https://arxiv.org/abs/1707.06347) 논문 학습
- [ ] **[확장]** [Soft Actor-Critic](https://arxiv.org/abs/1801.01290) 논문 학습
- [ ] CartPole/LunarLander에서 DQN 또는 PPO 구현·학습
- [ ] 여러 시드로 보상·샘플 효율·분산 비교 및 학습 곡선 기록
- [ ] 학습 정리 보고서 작성: Value-based vs Policy-based, PPO Clipping

### 3.4 생성 모델: VAE·GAN·Diffusion·Flow Matching

**연계 교재:** 밑시딥 5권 · 핸즈온 18장

#### 확률모형과 잠재변수

- [ ] **[핵심]** 밑시딥 5권 1~7장: 확률분포, 최대가능도, EM, 잠재변수, VAE 학습
- [ ] **[확장]** [Maximum Likelihood from Incomplete Data via the EM Algorithm](https://doi.org/10.1111/j.2517-6161.1977.tb01600.x) 논문 학습
- [ ] **[핵심]** [Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114) 논문 학습
- [ ] **[확장]** [Generative Adversarial Nets](https://arxiv.org/abs/1406.2661) 논문 학습
- [ ] VAE의 Reparameterization Trick와 ELBO를 설명하고 작은 데이터셋에서 구현
- [ ] 학습 정리 보고서 작성: Likelihood, KL Divergence, ELBO

#### Diffusion과 효율적 샘플링

- [ ] **[핵심]** 밑시딥 5권 8~10장, 핸즈온 18장: Diffusion의 전방·역방향 과정 학습
- [ ] **[핵심]** [Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2006.11239) 논문 학습
- [ ] **[핵심]** [Denoising Diffusion Implicit Models](https://arxiv.org/abs/2010.02502) 논문 학습
- [ ] **[핵심]** [High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/abs/2112.10752) 논문 학습
- [ ] **[확장]** [Scalable Diffusion Models with Transformers (DiT)](https://arxiv.org/abs/2212.09748) 논문 학습
- [ ] **[확장]** [Flow Matching for Generative Modeling](https://arxiv.org/abs/2210.02747) 논문 학습
- [ ] 작은 이미지 데이터셋에서 DDPM의 노이즈 예측 학습 구현
- [ ] 같은 모델에 DDPM/DDIM 샘플러를 적용해 단계 수·속도·품질 비교
- [ ] 생성 샘플 그리드·측정 지표·실험 설정 저장
- [ ] 학습 정리 보고서 작성: Diffusion 샘플링의 병목 및 새로운 가설

### 3.5 현대 LLM: GPT·사전학습·SFT·선호도 학습

**연계 교재:** 밑시딥 6권 1~6장 · 핸즈온 15장

#### Tokenizer, GPT 및 Scaling

- [ ] **[핵심]** 밑시딥 6권 1~3장: BPE, GPT 구조, 사전학습 학습
- [ ] **[핵심]** [Neural Machine Translation of Rare Words with Subword Units](https://arxiv.org/abs/1508.07909) 논문 학습
- [ ] **[핵심]** [Language Models are Unsupervised Multitask Learners (GPT-2)](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf) 보고서 학습
- [ ] **[핵심]** [Language Models are Few-Shot Learners (GPT-3)](https://arxiv.org/abs/2005.14165) 논문 학습
- [ ] **[확장]** [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361) 논문 학습
- [ ] **[핵심]** [Training Compute-Optimal Large Language Models (Chinchilla)](https://arxiv.org/abs/2203.15556) 논문 학습
- [ ] BPE 토크나이저와 Mini-GPT 사전학습 파이프라인 구현
- [ ] 모델 크기·학습 토큰 수에 따른 작은 규모의 손실 변화 비교
- [ ] 학습 정리 보고서 작성: Tokenizer, Causal LM, Scaling Law

#### SFT, Preference Optimization, Reasoning RL

- [ ] **[핵심]** 밑시딥 6권 3·6장, 핸즈온 15장: SFT, RLHF, DPO, GRPO 학습
- [ ] **[핵심]** [Training Language Models to Follow Instructions with Human Feedback (InstructGPT)](https://arxiv.org/abs/2203.02155) 논문 학습
- [ ] **[핵심]** [Direct Preference Optimization](https://arxiv.org/abs/2305.18290) 논문 학습
- [ ] **[핵심]** [DeepSeekMath](https://arxiv.org/abs/2402.03300) 논문 학습: GRPO 도출·목적함수
- [ ] **[핵심]** [DeepSeek-R1](https://arxiv.org/abs/2501.12948) 논문 학습
- [ ] **[확장]** [DAPO](https://arxiv.org/abs/2503.14476) 논문 학습
- [ ] 작은 공개 모델로 SFT 실험 및 Base/SFT 모델 평가 비교
- [ ] 검증 가능한 보상을 이용한 소규모 GRPO 또는 DPO 실험 설계·수행
- [ ] 학습 정리 보고서 작성: SFT vs Preference Learning vs RL, 평가 한계

### 3.6 LLM 효율화: LoRA·RoPE·Attention·분산 학습

**연계 교재:** 밑시딥 6권 4~9장 · 핸즈온 11·15·17장 및 부록 B

#### 파라미터 효율적 학습

- [ ] **[핵심]** 핸즈온 15장 파인튜닝 및 부록 B 양자화 학습
- [ ] **[핵심]** [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685) 논문 학습
- [ ] **[확장]** [QLoRA](https://arxiv.org/abs/2305.14314) 논문 학습
- [ ] Full Fine-tuning과 LoRA를 동일 조건에서 비교 (성능·학습 시간·GPU 메모리)
- [ ] 학습 정리 보고서 작성: Low Rank, Quantization, PEFT의 장단점

#### 효율적 아키텍처와 시스템

- [ ] **[핵심]** 밑시딥 6권 5·8~9장, 핸즈온 17장: RoPE, GQA, KV Cache, MoE, 분산 학습 학습
- [ ] **[핵심]** [RoFormer / RoPE](https://arxiv.org/abs/2104.09864) 논문 학습
- [ ] **[핵심]** [FlashAttention](https://arxiv.org/abs/2205.14135) 논문 학습
- [ ] **[핵심]** [GQA](https://arxiv.org/abs/2305.13245) 논문 학습
- [ ] **[확장]** [Switch Transformers](https://arxiv.org/abs/2101.03961) 논문 학습
- [ ] **[핵심]** [ZeRO](https://arxiv.org/abs/1910.02054) 논문 학습
- [ ] **[확장]** [Muon is Scalable for LLM Training](https://arxiv.org/abs/2502.16982) 논문 학습
- [ ] **[확장]** [The Polar Express](https://proceedings.iclr.cc/paper_files/paper/2026/hash/df88b275bef31ac96c85f0c4013734fc-Abstract-Conference.html) 논문 학습
- [ ] RoPE와 KV Cache를 직접 구현하고 출력을 검증
- [ ] Prefill/Decode 시퀀스 길이에 따른 시간·메모리 측정
- [ ] 학습 정리 보고서 작성: Attention의 계산·메모리 병목, 분산 학습의 조건

### 3.7 멀티모달·음성·RAG·Agent

**연계 교재:** 핸즈온 16장 및 15장 확장 학습

- [ ] **[핵심]** 핸즈온 16장: Vision Transformer와 멀티모달 표현학습 학습
- [ ] **[핵심]** [An Image Is Worth 16x16 Words (ViT)](https://arxiv.org/abs/2010.11929) 논문 학습
- [ ] **[핵심]** [Learning Transferable Visual Models From Natural Language Supervision (CLIP)](https://arxiv.org/abs/2103.00020) 논문 학습
- [ ] **[확장]** [BLIP-2](https://arxiv.org/abs/2301.12597) 논문 학습
- [ ] **[확장]** [DINOv2](https://arxiv.org/abs/2304.07193) 논문 학습
- [ ] **[확장]** [Segment Anything](https://arxiv.org/abs/2304.02643) 논문 학습
- [ ] **[확장]** [Whisper: Robust Speech Recognition via Large-Scale Weak Supervision](https://arxiv.org/abs/2212.04356) 논문 학습
- [ ] **[확장]** [Retrieval-Augmented Generation (RAG)](https://arxiv.org/abs/2005.11401) 논문 학습
- [ ] **[확장]** [ReAct](https://arxiv.org/abs/2210.03629) 논문 학습
- [ ] ViT 또는 CLIP의 특징 표현을 활용한 분류·검색 실험
- [ ] 음성 전사 품질이 후속 정보 추출/RAG에 주는 영향 분석
- [ ] 학습 정리 보고서 작성: 멀티모달 표현학습과 실제 Agent 신뢰성

### 3.8 최신 연구 탐색 · 교재 밖 확장

**목적:** 원 논문의 핵심 아이디어가 현재 연구에서 어떻게 확장·반박·개선되는지 확인한다.

- [ ] **[확장]** [Qwen3 Technical Report](https://arxiv.org/abs/2505.09388): Thinking/Non-thinking 모델 연구
- [ ] **[확장]** [s1: Simple Test-Time Scaling](https://arxiv.org/abs/2501.19393): Test-Time Compute 연구
- [ ] **[확장]** [Large Language Diffusion Models (LLaDA)](https://arxiv.org/abs/2502.09992): Diffusion 기반 언어모델
- [ ] **[확장]** [The Flexibility Trap](https://proceedings.mlr.press/v306/ni26e.html): Diffusion LM의 생성 순서와 RL
- [ ] **[확장]** [LaDiR: Latent Diffusion Enhances LLMs for Text Reasoning](https://proceedings.iclr.cc/paper_files/paper/2026/hash/843e1d8ab4819c8c8a4221fce2c8d455-Abstract-Conference.html): 잠재공간 추론
- [ ] **[확장]** [Qwen3.5-Omni Technical Report](https://arxiv.org/abs/2604.15804): 음성·영상·텍스트 통합
- [ ] **[확장]** [LLMs Get Lost In Multi-Turn Conversation](https://arxiv.org/abs/2505.06120): 대화 안정성 평가
- [ ] **[확장]** 최신 연구 가운데 2편 이상을 골라 기존 논문과 **연구 질문·방법·실험·한계** 비교
- [ ] 최신 연구 리뷰 보고서 작성: 재현 가능한 아이디어와 필요한 자원 추정

### 3.9 최종 연구 프로젝트

- [ ] 관심 연구 분야 2~3개를 선정하고 관련 논문 지도를 작성
- [ ] 후보 주제마다 **연구 질문, 가설, 데이터, 측정 지표, Baseline, 위험요인** 정리
- [ ] 집중 연구 분야 1개 선정 및 연구 제안서 작성
- [ ] 연구와 가장 가까운 논문 1편의 핵심 실험을 작은 규모로 재현
- [ ] 고정된 데이터 분할, 랜덤 시드, 환경, 하이퍼파라미터 설정 관리
- [ ] GPU 자원 사용 계획과 예상 메모리·학습 비용 산정
- [ ] Baseline 및 제안 방법의 비교 실험 수행
- [ ] 최소 1개의 Ablation 실험 수행
- [ ] 정량 지표, 실패 사례, 재현 한계를 포함한 결과 분석
- [ ] 환경 설치·실행 명령·데이터 준비·재현 절차를 README/보고서에 기록
- [ ] 최종 연구 보고서 작성 및 GitHub에 산출물 연결

---

## 4. 학습 기록·프로젝트·산출물 링크

> 아래 경로는 **권장 저장 위치**다. 아직 파일이 없으므로 가짜 링크를 만들지 않았으며, 생성 후 `링크` 칸을 실제 Markdown 상대경로로 교체한다. 예: `[역전파 노트](notes/fundamentals/backpropagation.md)`.

| 유형 | 주제 / 결과물 | 권장 저장 위치 | 링크 | 상태 |
|---|---|---|---|---|
| 학습 노트 | 오차역전파·자동미분 | `notes/fundamentals/backpropagation.md` | 추가 예정 | 복습 예정 |
| 학습 노트 | 최적화·일반화 | `notes/fundamentals/optimization.md` | 추가 예정 | 미시작 |
| 학습 노트 | CNN·ResNet | `notes/vision/cnn-resnet.md` | 추가 예정 | 미시작 |
| 학습 노트 | NLP·Attention | `notes/nlp/attention-transformer.md` | 추가 예정 | 미시작 |
| 학습 노트 | 강화학습·PPO | `notes/rl/policy-optimization.md` | 추가 예정 | 미시작 |
| 학습 노트 | VAE·Diffusion | `notes/generative/diffusion.md` | 추가 예정 | 미시작 |
| 학습 노트 | LLM·SFT·GRPO | `notes/llm/training-and-reasoning.md` | 추가 예정 | 미시작 |
| 학습 노트 | LoRA·효율화 | `notes/llm/efficient-training.md` | 추가 예정 | 미시작 |
| 논문 리뷰 | 개별 논문 요약 | `paper-reviews/` | 추가 예정 | 미시작 |
| 구현 실습 | 핵심 알고리즘 재구현 | `implementations/` | 추가 예정 | 미시작 |
| 비교 실험 | 재현 및 Ablation | `experiments/` | 추가 예정 | 미시작 |
| 연구 제안서 | 독립 연구 주제 | `research/proposal.md` | 추가 예정 | 미시작 |
| 최종 보고서 | 연구 결과 및 한계 | `research/final-report.md` | 추가 예정 | 미시작 |

### 주요 참고 코드 및 공개 자료

- [Hands-On Machine Learning with Scikit-Learn and PyTorch — 저자 실습 저장소](https://github.com/ageron/handson-mlp)
- [PyTorch 공식 문서](https://pytorch.org/docs/stable/index.html)
- [Hugging Face Transformers](https://huggingface.co/docs/transformers/index)
- [Hugging Face PEFT](https://huggingface.co/docs/peft/index)
- [Hugging Face TRL](https://huggingface.co/docs/trl/index)
- [Gymnasium 공식 문서](https://gymnasium.farama.org/)
- [Papers with Code](https://paperswithcode.com/)
- [arXiv cs.LG](https://arxiv.org/list/cs.LG/recent) · [OpenReview](https://openreview.net/) · [PMLR](https://proceedings.mlr.press/)

---

## 5. 교재·논문·아티클 라이브러리

### 5.1 교재 목록

| 유형 | 자료 | 학습 범위 / 역할 | 학습 상태 | 정리 링크 |
|---|---|---|---|---|
| 도서 | 『밑바닥부터 시작하는 딥러닝 1』 | 오차역전파, 최적화, CNN | **기존 1회독 완료 · 복습 예정** | 추가 예정 |
| 도서 | 『밑바닥부터 시작하는 딥러닝 2』 | NLP, 임베딩, RNN, Attention | 미시작 | 추가 예정 |
| 도서 | 『밑바닥부터 시작하는 딥러닝 4』 | 강화학습과 Deep RL | 미시작 | 추가 예정 |
| 도서 | 『밑바닥부터 시작하는 딥러닝 5』 | 확률적 생성 모델, VAE, Diffusion | 미시작 | 추가 예정 |
| 도서 | 『밑바닥부터 시작하는 딥러닝 6』 | GPT, 사전학습, SFT, GRPO, 효율화 | 미시작 | 추가 예정 |
| 도서 | [Hands-On Machine Learning with Scikit-Learn and PyTorch](https://www.oreilly.com/library/view/hands-on-machine-learning/9798341607972/) — Aurélien Géron | **9~19장**, 필요한 경우 1~8장 및 부록 | 미시작 | 추가 예정 |

*3권은 이번 학습 경로에서 제외. 상태와 정리 링크는 학습 후 갱신한다.*

### 5.2 논문·기술 보고서 인덱스

표는 **참고 문헌 목록**이며, 실제 완료 여부는 [3. 학습 체크리스트](#3-학습-체크리스트)의 체크박스로 관리한다. `핵심`은 우선순위, `확장`은 선택 심화다.

| 분야 | 논문 / 보고서 | 연결 주제 | 우선순위 |
|---|---|---|---|
| 기초 | [Learning Representations by Back-Propagating Errors](https://doi.org/10.1038/323533a0) | 역전파 | 핵심 |
| 기초 | [Adam](https://arxiv.org/abs/1412.6980) | 최적화 | 핵심 |
| 기초 | [Batch Normalization](https://arxiv.org/abs/1502.03167) | 학습 안정성 | 확장 |
| 기초 | [Dropout](https://jmlr.org/papers/v15/srivastava14a.html) | 일반화 | 확장 |
| 기초 | [Super-Convergence](https://arxiv.org/abs/1708.07120) | 학습률 | 확장 |
| CNN | [AlexNet](https://proceedings.neurips.cc/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html) | CNN | 확장 |
| CNN | [ResNet](https://arxiv.org/abs/1512.03385) | 잔차 연결 | 핵심 |
| NLP | [word2vec](https://arxiv.org/abs/1301.3781) | 임베딩 | 핵심 |
| NLP | [GloVe](https://aclanthology.org/D14-1162/) | 임베딩 | 확장 |
| NLP | [Generating Sequences with Recurrent Neural Networks](https://arxiv.org/abs/1308.0850) | RNN | 확장 |
| NLP | [LSTM](https://www.bioinf.jku.at/publications/older/2604.pdf) | 긴 시퀀스 | 핵심 |
| NLP | [Seq2Seq](https://arxiv.org/abs/1409.3215) | Encoder–Decoder | 핵심 |
| NLP | [Bahdanau Attention](https://arxiv.org/abs/1409.0473) | Attention | 핵심 |
| NLP/LLM | [Attention Is All You Need](https://arxiv.org/abs/1706.03762) | Transformer | 핵심 |
| RL | [Multi-Armed Bandit](https://link.springer.com/article/10.1023/A:1013689704352) | 탐색과 활용 | 확장 |
| RL | [Q-learning](https://link.springer.com/article/10.1007/BF00992698) | TD 학습 | 핵심 |
| RL | [DQN](https://arxiv.org/abs/1312.5602) | Deep RL | 핵심 |
| RL | [Rainbow](https://arxiv.org/abs/1710.02298) | DQN 개선 | 확장 |
| RL | [REINFORCE](https://link.springer.com/article/10.1007/BF00992696) | Policy Gradient | 핵심 |
| RL | [A3C](https://arxiv.org/abs/1602.01783) | Actor-Critic | 확장 |
| RL | [PPO](https://arxiv.org/abs/1707.06347) | 정책 최적화 | 핵심 |
| RL | [Soft Actor-Critic](https://arxiv.org/abs/1801.01290) | 연속 제어 | 확장 |
| 생성 | [EM Algorithm](https://doi.org/10.1111/j.2517-6161.1977.tb01600.x) | 잠재변수 | 확장 |
| 생성 | [Auto-Encoding Variational Bayes](https://arxiv.org/abs/1312.6114) | VAE | 핵심 |
| 생성 | [Generative Adversarial Nets](https://arxiv.org/abs/1406.2661) | GAN | 확장 |
| 생성 | [DDPM](https://arxiv.org/abs/2006.11239) | Diffusion | 핵심 |
| 생성 | [DDIM](https://arxiv.org/abs/2010.02502) | 샘플링 | 핵심 |
| 생성 | [Latent Diffusion Models](https://arxiv.org/abs/2112.10752) | 잠재공간 생성 | 핵심 |
| 생성 | [DiT](https://arxiv.org/abs/2212.09748) | Diffusion Transformer | 확장 |
| 생성 | [Flow Matching](https://arxiv.org/abs/2210.02747) | 생성 경로 | 확장 |
| LLM | [BPE Subword Units](https://arxiv.org/abs/1508.07909) | 토큰화 | 핵심 |
| LLM | [GPT-2](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf) | Decoder-only | 핵심 |
| LLM | [GPT-3](https://arxiv.org/abs/2005.14165) | In-Context Learning | 핵심 |
| LLM | [Scaling Laws](https://arxiv.org/abs/2001.08361) | 모델·데이터·연산량 | 확장 |
| LLM | [Chinchilla](https://arxiv.org/abs/2203.15556) | Compute-Optimal Training | 핵심 |
| LLM | [InstructGPT](https://arxiv.org/abs/2203.02155) | SFT·RLHF | 핵심 |
| LLM | [DPO](https://arxiv.org/abs/2305.18290) | 선호도 최적화 | 핵심 |
| LLM/RL | [DeepSeekMath](https://arxiv.org/abs/2402.03300) | GRPO | 핵심 |
| LLM/RL | [DeepSeek-R1](https://arxiv.org/abs/2501.12948) | Reasoning | 핵심 |
| LLM/RL | [DAPO](https://arxiv.org/abs/2503.14476) | RL 학습 안정화 | 확장 |
| 효율화 | [LoRA](https://arxiv.org/abs/2106.09685) | PEFT | 핵심 |
| 효율화 | [QLoRA](https://arxiv.org/abs/2305.14314) | 양자화 파인튜닝 | 확장 |
| 효율화 | [RoFormer](https://arxiv.org/abs/2104.09864) | RoPE | 핵심 |
| 효율화 | [FlashAttention](https://arxiv.org/abs/2205.14135) | GPU 메모리 효율 | 핵심 |
| 효율화 | [GQA](https://arxiv.org/abs/2305.13245) | KV Head 공유 | 핵심 |
| 효율화 | [Switch Transformers](https://arxiv.org/abs/2101.03961) | MoE | 확장 |
| 효율화 | [ZeRO](https://arxiv.org/abs/1910.02054) | 분산 학습 | 핵심 |
| 효율화 | [Muon](https://arxiv.org/abs/2502.16982) | 최적화 | 확장 |
| 멀티모달 | [ViT](https://arxiv.org/abs/2010.11929) | Vision Transformer | 핵심 |
| 멀티모달 | [CLIP](https://arxiv.org/abs/2103.00020) | 이미지·텍스트 정렬 | 핵심 |
| 멀티모달 | [BLIP-2](https://arxiv.org/abs/2301.12597) | Vision-Language | 확장 |
| 멀티모달 | [DINOv2](https://arxiv.org/abs/2304.07193) | 자기지도 시각 표현 | 확장 |
| 멀티모달 | [Segment Anything](https://arxiv.org/abs/2304.02643) | 이미지 분할 | 확장 |
| 음성 | [Whisper](https://arxiv.org/abs/2212.04356) | 음성 인식 | 확장 |
| Agent | [RAG](https://arxiv.org/abs/2005.11401) | 외부 지식 활용 | 확장 |
| Agent | [ReAct](https://arxiv.org/abs/2210.03629) | 도구 사용 | 확장 |
| 최신 | [s1: Simple Test-Time Scaling](https://arxiv.org/abs/2501.19393) | 추론 시간 연산 | 확장 |
| 최신 | [Qwen3 Technical Report](https://arxiv.org/abs/2505.09388) | 하이브리드 추론 | 확장 |
| 최신 | [LLaDA](https://arxiv.org/abs/2502.09992) | 언어 Diffusion | 확장 |
| 최신 | [The Flexibility Trap](https://proceedings.mlr.press/v306/ni26e.html) | Diffusion LM 평가 | 확장 |
| 최신 | [LaDiR](https://proceedings.iclr.cc/paper_files/paper/2026/hash/843e1d8ab4819c8c8a4221fce2c8d455-Abstract-Conference.html) | 잠재공간 추론 | 확장 |
| 최신 | [Qwen3.5-Omni Technical Report](https://arxiv.org/abs/2604.15804) | 통합 멀티모달 | 확장 |
| 최신 | [LLMs Get Lost In Multi-Turn Conversation](https://arxiv.org/abs/2505.06120) | 대화 신뢰성 | 확장 |
| 최신 | [The Polar Express](https://proceedings.iclr.cc/paper_files/paper/2026/hash/df88b275bef31ac96c85f0c4013734fc-Abstract-Conference.html) | Muon 행렬 계산 | 확장 |

### 5.3 아티클·강의·추가 자료 로그

공식 문서, 해설 글, 강의, 세미나 등은 **읽은 뒤에만** 아래 표에 추가한다.

| 유형 | 제목 | 원문 링크 | 핵심 배운 점 | 내 정리 링크 |
|---|---|---|---|---|
| 공식 문서 | [PyTorch Tutorials](https://pytorch.org/tutorials/) | https://pytorch.org/tutorials/ | 학습 후 작성 | 추가 예정 |
| 공식 문서 | [Hugging Face Course](https://huggingface.co/learn) | https://huggingface.co/learn | 학습 후 작성 | 추가 예정 |
| 아티클 / 강의 | 추가 예정 | 추가 예정 | 추가 예정 | 추가 예정 |

---

## 6. 연구 주제 탐색 및 실험 규칙

### 관심 분야 비교표

| 연구 분야 | 대표 논문 | 가장 흥미로웠던 질문 | 구현 경험 | 관심도 (1~5) | 연구 후보 |
|---|---|---|---|---|---|
| 아키텍처 / 표현학습 | ResNet, Attention, ViT | 미작성 | 미작성 | - | - |
| 최적화 / RL | Adam, PPO, GRPO | 미작성 | 미작성 | - | - |
| 생성 모델 | VAE, DDPM, Flow Matching | 미작성 | 미작성 | - | - |
| LLM 학습 / 효율화 | LoRA, QLoRA, FlashAttention | 미작성 | 미작성 | - | - |
| 멀티모달 / Agent | CLIP, Whisper, RAG, ReAct | 미작성 | 미작성 | - | - |

### 논문을 읽을 때 답할 질문

1. **Problem** — 어떤 기존 한계를 해결하려는가?
2. **Method** — 무엇을 새롭게 제안했고, 왜 동작할 것이라고 기대하는가?
3. **Experiments** — 어떤 데이터셋·Baseline·평가 지표·Ablation을 사용했는가?
4. **Limitations** — 어떤 제약, 실패 사례, 재현의 어려움이 있는가?
5. **My Hypothesis** — 내가 검증하거나 개선하고 싶은 질문은 무엇인가?

### 재현 가능한 실험 규칙

- 훈련/검증/테스트 데이터를 분리하고 **테스트셋을 튜닝에 사용하지 않는다.**
- 실험별 설정 파일, 코드 버전, 데이터 버전, 라이브러리 환경, 랜덤 시드를 기록한다.
- 가능한 경우 복수 시드의 평균과 변동성을 보고한다.
- Baseline과 제안 방법의 데이터·연산 예산·평가 방식이 비교 가능한지 확인한다.
- 정확도 외에 학습 시간·GPU 메모리·추론 속도·비용을 필요한 만큼 함께 측정한다.
- 수렴 실패와 부정적 결과도 기록한다. 결과에 유리한 시행만 선택하지 않는다.
- 개인정보·라이선스·데이터 이용 조건을 확인하고 원본 데이터와 비밀 키를 커밋하지 않는다.
- 모델 체크포인트와 대용량 데이터는 Git LFS, 외부 스토리지 등을 필요에 따라 사용한다.

---

## 7. 저장소 구조 및 문서 템플릿

### 권장 구조

```text
 dl-deep-dive/
 ├── README.md                    # 이 파일: 전체 학습 로드맵
 ├── notes/                       # 교재·개념별 정리
 │   ├── fundamentals/
 │   ├── vision/
 │   ├── nlp/
 │   ├── rl/
 │   ├── generative/
 │   └── llm/
 ├── paper-reviews/               # 논문별 독서 기록
 ├── implementations/             # 직접 구현한 알고리즘·모델
 ├── experiments/                 # 비교 실험, 설정, 결과
 ├── research/                    # 연구 질문·제안서·최종 보고서
 ├── assets/                      # 직접 생성한 그림·도식
 ├── requirements/                # 재현 환경 정보
 └── .gitignore
```

### 논문 리뷰 템플릿

```markdown
# [논문 제목]

- 원문:
- 연결 교재·장:
- 핵심 키워드:
- 학습 상태: 읽는 중 / 정리 완료 / 구현 완료 / 재현 완료

## 1. 해결하려는 문제

## 2. 배경 지식 및 핵심 아이디어

## 3. 주요 수식·모델 구조

## 4. 논문의 실험 설정·결과

## 5. 한계와 의문점

## 6. 내 구현·재현 결과

## 7. 후속 연구 아이디어
```

### 실험 보고서 템플릿

```markdown
# [실험 이름]

- 연구 질문:
- 가설:
- 기준 논문 / Baseline:
- 코드 버전 / 환경:
- 데이터셋 / 분할:
- 모델 / 하이퍼파라미터 / 시드:
- 평가 지표 / 자원 사용량:

## 1. 실험 설계

## 2. 결과 및 시각화

## 3. Baseline 비교·Ablation

## 4. 실패 사례·한계

## 5. 결론 및 다음 실험
```

### 변경 기록

| 업데이트 날짜 | 변경 내용 |
|---|---|
| 2026-10-19 | 초기 학습 로드맵, 책-논문 매칭 체크리스트, 연구 템플릿 작성 |

---

**최종 체크리스트 업데이트 날짜: 2026-10-19**
