# Finetuning

- 모델이 점점 커지고 데이터셋 크기도 커짐에 따라 전체 모델을 Tuning하는 것이 불가능해짐
  : 비용, 시간, 용량
- 효과적으로 Tuning할 수 있는 방법으로 PEFT 등장하게 됨 

### PEFT (Parameter Efficient Fine-Tuning)
- 적은 매개변수 학습으로 빠른 시간에 새로운 문제를 해결하는 Fine-tuning 방법
- 다양한 언어, 다양한 도메인의 데이터 모델 적용시 유용
- 각 도메인 또는 언어별 체크포인트를 로컬에 저장하면 효율적으로 작동함
- 잘 안쓰는 대부분 파라미터를 Freezing, 일부 파라미터만 finetuning
- 저장 공간 관리에도 큰 도움
- HuggingFace에 많은 기술들이 업로드 되고 있음
- LoRA, Prefix tuning, P-Tuning 등
- PEFT 종류 6가지
  
    **Knowledge Distillation**
    - 성능 좋은 모델로 지식이 작은 모델에 지식 전달하는 방법
  
    **Pruning**
    - 불필요한 가중치, 연결을 끊어내는 방법
  
    **Quantization**
    - 모델 변수의 가중치 정밀도를 맞춰 메모리, 계산 요구사항을 낮춤
      - 32bit 부동소수점 > 8bit로 압축 (잘라내는 것) : 1/4
      - 비용, 공간, 시간 절약
  
    **Low-Rank Factorization**
    - 사전학습된 모델의 가중치 행렬을 Low-Rank matrix 공간에 근사시킴
    - 행렬의 양을 줄이는 방식
  
    **Knowledge injection**
    - 모델 파라미터를 수정하진 않음
    - 태스크별 정보 주입해 특정 테스크별 성능 향상시키는 방법
      
    **Adapter Modules**
    - 원래 파라미터 수정하지 않음
    - 특정 작업 위해 사전 작업 모델을 추가하는 경량 모듈
   ---
**LoRA** (Low Rank Adaptation)
- 사전 훈련된 LLM을 적은 컴퓨팅 메모리로 학습하기 위해 나온 방법
- 필요한 작은 부분의 파라미터만 수정하기 위해 등장
- 대부분 Freezing하고 일부만 finetuning 하는 방식
- 위에 가벼운 경량 모델들을 얹어서 씀

**Prefix Tuning**
- 적은 매개변수 학습으로 빠른 시간에 새로운 문제 해결하는 방법
- 다양한 언어, 도메인에 데이터 모델 적용시 유용
- 각 도메인, 언어 별 작은 체크 포인트 로컬에 저장하면 효율적으로 작동
- 인풋 앞에 prefix, 일련의 연속적 태스크 특화 벡터를 붙이는 방식

**Prompt Tuning**
- Prefix Tuning과 유사하나 간소화된 형태
- 특정 다운스트림 태스크 수행 위해 언어 모델의 가중치를 고정
- 개발 태스크마다 프롬프트의 파라미터를 업데이트하는 Soft Prompt 학습 방식

**P Tuning**
- 사전 학습된 LLM에 인풋으로 프롬프트 역할을 하는 연속적인 파라미터를 사용하는 방식
