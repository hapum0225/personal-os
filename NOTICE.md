# NOTICE

이 저장소(`personal-os`)는 아래 원본 스킬의 **구조와 개념에서 출발해 재설계·확장**한 파생 저작물입니다.
MIT 라이선스의 고지 유지 의무에 따라, 원 저작권 고지와 그 관계를 여기에 명시합니다.

## 원본 (upstream)

- **저장소**: https://github.com/selfishclub/os-interview-skill
- **라이선스**: MIT
- **기준 커밋(SHA)**: `8d08c4ea003cd00b6574e013e2f6ff6bad58a78a` (원본 v0.2, 2026-05-03)
- **원 저작권 고지**: `Copyright (c) 2026 selfishclub (Sponge Club 1st cohort)`

원본 MIT 라이선스 전문은 이 저장소 루트의 [`LICENSE`](./LICENSE)에 원 저작권 고지와 함께 그대로 보존되어 있습니다.

## 원본에서 유래한 부분 (concept·structure)

다음 설계 개념은 원본에서 이어받았습니다. 해당 표현·구조에는 위 원 저작권 고지가 적용됩니다.

- 3 Phase / 6 Step 인터뷰 흐름과, 핵심을 한 문장으로 압축해 중심에 두는 구조(원본의 "OS 선언문" → 이 버전의 "OS Core")
- R 톤(사고 파트너) / Q 톤(발판형) 이원화
- 첫 부품 결과물을 A(스킬) / B(플러그인) / C(PRD) 세 형태로 분기하는 방식과 "처음엔 A부터" 권장
- 사용자 답변이 추상어·회피·선택 마비에 빠질 때 개입하는 harness 규칙의 개념

## 이 저장소에서 새로 만든 부분 (new in this work)

아래는 원본에 없던 신규 저작분이며, 루트 [`LICENSE`](./LICENSE)의 `Copyright (c) 2026 hapum0225`가 적용됩니다.

- Claude Code 플러그인 마켓플레이스 방식의 배포 패키징(`.claude-plugin/`, `plugins/`)
- 세션별 상태 파일 기반 중단·재개 프로토콜과 손상 복구·주입 방어 규칙
- Windows/macOS/Linux 설치 안내와 크로스플랫폼 경로 처리
- 한국어·영어 병기 트리거와 운영체제 질문 오발동 방어
- 재현 가능한 평가 세트(트리거·시나리오·중단재개·손상복구·baseline 비교)
- 인터뷰 방법론 도구상자(JTBD 스위치 스토리, Five Whys, Four Forces, 래더링)를 "자유 응답 우선, 막힐 때만 투입" 원칙으로 편성
- 산출물을 실제 파일로 생성하는 출력 프로토콜과 A형 산출물의 콜드리더 자립성 점검

## 참고한 다른 프로젝트

설계 과정에서 아래 프로젝트들의 **아이디어를 참고**했으나, 이들의 코드·문서·템플릿 표현을 복제하지는 않았습니다.
(향후 이들의 표현을 실제로 차용할 경우 각 프로젝트의 라이선스를 확인해야 합니다. 특히 `anthropics/skills`의 예제 스킬은 Apache-2.0입니다.)

- anthropics/skills — skill-creator, doc-coauthoring (Apache-2.0)
- obra/superpowers — brainstorming
- Sorbh/interview-me (MIT)
- nateherkai/AIS-OS (MIT)
