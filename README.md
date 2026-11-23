# How InstructGPT Works

**사람의 선호 순위를 보상으로 쓰는 RLHF.** GPT-3는 다음 토큰을 예측하도록 학습했을 뿐 지시를 따르도록 학습한 적은 없습니다. InstructGPT는 사람이 매긴 "이 답이 저 답보다 낫다"는 순위로 보상 모델을 만들고, 그 보상 모델을 채점자로 세워 GPT-3를 PPO로 미세조정했습니다. 그 결과 13억 파라미터 InstructGPT의 답이 100배 큰 GPT-3의 답보다 선호되었고, 같은 방법이 열 달 뒤 ChatGPT가 됩니다. 「Training Language Models to Follow Instructions with Human Feedback」(Ouyang 외, NeurIPS 2022)을 따라가며 순위가 쌍 비교로, 쌍 비교가 보상으로, 보상이 정책으로 바뀌는 과정을 브라우저에서 직접 계산해 보는 인터랙티브 교육 자료입니다.

🔗 **[데모 바로가기](https://dev-jonghoonpark.github.io/how-instructgpt-works/)**

## 다루는 내용

1. **문제** · 다음 토큰 예측과 지시 따르기의 어긋남, 달 착륙 예시
2. **세 단계 한눈에 보기** · SFT → 보상 모델 → PPO
3. **데이터와 라벨러** · 프롬프트 출처(Plain · Few-shot · User-based · API 고객), 데이터셋 크기(1.3만 · 3.3만 · 3.1만), 라벨러 약 40명, 학습과 평가에서 달랐던 기준
4. **1단계 SFT** · 16 에폭, 검증 손실은 과적합해도 RM 점수는 오르는 이유
5. **2단계 보상 모델** · 순위 매기기 체험(순위 → K(K−1)/2 쌍), 쌍 손실 −log σ(Δ) 계산기, **브라우저에서 학습하는 보상 모델**(라벨러 잡음과 일치율 72.6%, 정확도 상한)
6. **3단계 PPO** · 밴딧 환경, PPO 클립 목적 함수, KL 벌점과 최적 정책 π_SFT · exp(r/β), **β를 내리면 보상 모델 점수와 사람 기준 점수가 갈라지는** 과최적화 데모
7. **PPO-ptx** · 사전학습 기울기를 섞는 이유(β = 0.02, γ = 27.8), 목적 함수 세 항의 역할
8. **결과** · 85 ± 3% · 71 ± 4% 선호, 환각 41% → 21%, FLAN·T0 비교, 정렬에 드는 계산(사전학습의 2% 미만)
9. **누구의 선호에 맞춘 것인가, 한계** · 거짓 전제, 과한 얼버무림, 해로운 지시
10. **ChatGPT로, 추론 모델로** · ChatGPT의 데이터 수집 차이, DeepSeek-R1의 규칙 기반 보상과 비교
11. **정리와 퀴즈 8문항**

## 참고

- Ouyang et al. (2022), *Training Language Models to Follow Instructions with Human Feedback* — [arXiv:2203.02155](https://arxiv.org/abs/2203.02155)
- OpenAI (2022), *Aligning Language Models to Follow Instructions* — [openai.com](https://openai.com/index/instruction-following/)
- OpenAI (2022), *Introducing ChatGPT* — [openai.com](https://openai.com/index/chatgpt/)
- Christiano et al. (2017), *Deep Reinforcement Learning from Human Preferences* — [arXiv:1706.03741](https://arxiv.org/abs/1706.03741)
- Stiennon et al. (2020), *Learning to Summarize from Human Feedback* — [arXiv:2009.01325](https://arxiv.org/abs/2009.01325)
- Schulman et al. (2017), *Proximal Policy Optimization Algorithms* — [arXiv:1707.06347](https://arxiv.org/abs/1707.06347)

[how-ai-works](https://github.com/dev-jonghoonpark/how-ai-works) 시리즈의 일부입니다.
