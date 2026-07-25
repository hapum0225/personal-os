# Changelog

이 프로젝트의 주요 변경 사항을 기록합니다.
버전은 [plugin.json](./plugins/personal-os/.claude-plugin/plugin.json)의 `version`을 단일 출처로 삼으며,
릴리스마다 plugin.json 버전 · 이 CHANGELOG · git tag가 일치해야 합니다.

형식은 [Keep a Changelog](https://keepachangelog.com/ko/1.1.0/)을,
버전 규칙은 [유의적 버전(SemVer)](https://semver.org/lang/ko/)을 따릅니다.

## [1.0.0] - 2026-07-25

첫 공개 버전. `selfishclub/os-interview-skill`(MIT, commit `8d08c4e`)의 구조에서 출발해 재설계·확장했습니다.
자세한 저작권 관계는 [NOTICE.md](./NOTICE.md) 참고.

### Added
- 6단계 인터뷰(3 Phase)로 개인 OS를 설계하고 첫 부품 1개를 산출물로 만드는 `personal-os` 스킬
  - 단계: 생활 환경 → 반복 소모 → OS Core → 부품 지도 → 첫 부품 결정 → 결과물
  - **OS Core**: 지켜야 할 핵심 구조/가치를 한 문장으로 압축(구조형·가치형)
- Claude Code 플러그인 마켓플레이스 방식 배포 (URL 추가 → 설치)
- 세션별 상태 파일 기반 중단·재개 프로토콜 (손상 복구·주입 방어 포함)
- 한국어·영어 병기 트리거와 운영체제(OS) 질문 오발동 방어
- 산출물 A(스킬 폴더) / B(플러그인 디렉터리) / C(PRD) 분기와 각 산출물 규격 검증
- **OS 유형 태깅**: 개인 / 삶 / 업무(›세부 카테고리) 배지를 청사진·결과물에 표기
- **참고 사례 차용 논의**: 결과물 생성 전 '물어본 뒤 검색'으로 후보를 근거·비용과 함께 제시(토큰 상한·출처 기록)
- 인터뷰 방법론 도구상자(스위치 스토리·Five Whys·Four Forces·래더링)
- 재현 가능한 평가 세트(트리거·시나리오·중단재개·손상복구·baseline 비교)
- Windows/macOS/Linux 설치 안내 (Windows 실검증)

### 배경
- 원본은 수동 파일 복사 설치, 세션 중단 시 재개 불가, 트리거 한국어 전용, 평가 부재 등의 한계가 있었습니다.

[1.0.0]: https://github.com/hapum0225/personal-os/releases/tag/v1.0.0
