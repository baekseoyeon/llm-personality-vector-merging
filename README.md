# LLM Personality Control (성격 벡터 기반 제어 엔진)

## Paper

This repository is based on the following paper:

**Personality Vector: Modulating Personality of Large Language Models by Model Merging**  
EMNLP 2025 Main Conference  
[arXiv](https://arxiv.org/abs/2509.19727)

<p align="center">
  <img src="image/figure1_git.png" width="720" alt="Personality Vector Merging Architecture" />
</p>

## Overview

이 레포는 Personality Vector Merging 기반의 LLM 성격 제어 방법을 다룹니다.  
각 Big Five 성격 조건으로 fine-tuning된 모델과 base model의 파라미터 차이를 personality vector로 정의하고, 이를 모델에 다시 병합해 성격을 조절합니다.
즉, 프롬프트가 아니라 **모델 파라미터 차이**로 LLM의 성격을 정의하고, 이를 **α 스케일링**과 **모델 병합**으로 제어합니다.

이 프로젝트는 다음 질문에 답하는 기술 검증에 초점을 둡니다.

- 성격 강도를 연속적으로 조절할 수 있는가
- 여러 성격 trait를 함께 조합할 수 있는가
- 성격 벡터를 다른 도메인 모델에도 옮길 수 있는가

## What this repository covers

- personality vector 추출
- 단일 trait scaling
- 다중 trait composition
- model merging 전략 비교
- transferability 실험 코드 및 관련 자료

## Key contributions

- 프롬프트 의존이 아닌 모델 수준의 성격 제어 방식 제안
- α scaling을 통한 연속적 trait intensity 조절
- 다중 trait 병합을 통한 복합 성격 구성
- role-playing, cross-lingual, cross-modal 설정에서의 확장 가능성 검증

## Method at a glance

성격 조건별 fine-tuned model과 base model의 파라미터 차이를 personality vector로 정의합니다.

- Personality Vector: ϕp = θp − θbase
- Single-trait control: θ' = θbase + αϕp
- Multi-trait control: θ' = θbase + Σ αpϕp

이를 통해 추가 학습 없이 성격을 제어할 수 있도록 설계했습니다.

## Repository structure

- `model_merge/`  
  personality vector 병합 코드와 관련 유틸리티
  #### Merge models
  
  ```bash (아래 스크립트는 실행 예시입니다. 사용 전, 환경에 맞게 모델 경로와 API 설정을 수정하세요.)
  bash model_merge/merge.sh

- `interview/`  
  병합된 모델의 성격 발현을 확인하기 위한 평가 스크립트
  #### Evaluate the merged model
  
  ```bash (아래 스크립트는 실행 예시입니다. 사용 전, 환경에 맞게 모델 경로와 API 설정을 수정하세요.)
  bash interview/interview.sh

- `docs/PROJECT.md`  
  프로젝트 개요와 기술 범위 정리

- `image/`  
  README 및 문서에 사용한 구조 이미지

  
## Notes

이 레포는 성격 제어 기술 자체에 초점을 둔 연구 레포입니다.  
사용자 조절 인터페이스와 UX 검증 시스템은 별도 레포인 `LLaPo-chat`에서 다룹니다.
