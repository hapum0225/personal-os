# 발동 테스트 (trigger-tests)

`personal-os` 스킬이 **발동해야 할 때 발동하고, 발동하면 안 될 때 안 하는지**를 검증한다.

## 실행 방법
- 각 발화를 **새 세션에서 최소 3회** 실행한다(모델이 비결정적이므로).
- 발동 여부는 답변의 문체로 추정하지 말고, **실제 Skill invocation 흔적**으로 판정한다(Claude Code debug/log, 또는 스킬이 시작 게이트대로 출력 폴더·상태 저장을 안내하는지).
- 실행 환경(모델·Claude Code 버전·OS)을 결과에 기록한다. 결과는 `evals/results/`에 남긴다.

## 합격 기준 (게이트)
| 지표 | 기준 |
|---|---|
| Trigger recall | should 10종 × 3회에서 발동 성공률 **≥ 90%** |
| Trigger precision | should-not 9종 × 3회에서 발동 **0건** |

## should-trigger (10) — 발동해야 함

한국어 (7):
1. 내 OS를 만들고 싶어. 어디서부터 시작하지?
2. 나만의 워크플로우를 시스템으로 만들고 싶어요.
3. 반복되는 업무를 자동화하고 싶은데 뭘 만들어야 할지 모르겠어.
4. 나만의 Claude 스킬을 만들어서 내 일에 쓰고 싶어.
5. 매주 하는 잡무를 Claude한테 넘기고 싶어. 뭐부터 만들면 돼?
6. 내 업무 시스템을 처음부터 설계해보고 싶어.
7. 강의에서 배운 대로 내 개인 OS 청사진을 그려보고 싶어요.

영어 (3):
8. I want to build my personal OS. Help me figure out where to start.
9. I'd like to automate my repetitive workflow but don't know what to build first.
10. Help me design my own skill to run my work.

## should-NOT-trigger (9) — 발동하면 안 됨 (near-miss)

1. Windows에서 부팅이 안 돼요. 운영체제를 재설치해야 하나요? *(컴퓨터 OS 질문)*
2. 리눅스 커널의 프로세스 스케줄링이 어떻게 동작하는지 설명해줘. *(커널/프로세스)*
3. macOS 업데이트하다가 설치가 멈췄어요. 어떻게 고치죠? *(OS 설치 문제)*
4. 이 제품에 대한 PRD 하나 써줘. *(일반 PRD 작성 — 인터뷰 맥락 없음)*
5. 내가 설치한 이 플러그인이 에러가 나는데 디버깅 좀 도와줘. *(기존 부품 디버깅)*
6. 업무 자동화 팁 몇 개만 알려줘. *(가벼운 팁 요청 — 인터뷰 원치 않음)*
7. 우리 회사 이름이 "OS"인데 로고를 만들어줘. *("OS"가 고유명사)*
8. 생산성 높이는 습관 같은 거 추천해줄 수 있어? *(가벼운 생산성 조언)*
9. Can you explain how an operating system manages memory? *(영어 운영체제 질문)*

## 기록 양식 (results/에 저장)
```
- date: 2026-07-24
- model: <모델명>
- claude_code_version: <버전>
- os: <Windows 11 / macOS ...>
- recall: 9/10 (28/30 runs)   ← 판정 근거(invocation 흔적) 한 줄
- precision: 9/9 (0 발동)
- 실패 케이스와 원인:
```
