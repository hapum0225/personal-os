# Personal OS Interview 🐜

**개인 워크플로우·반복 업무를 자동화하는 '나만의 OS'를 6단계 인터뷰로 설계하고, 첫 부품 1개를 실제 산출물(스킬/플러그인/PRD)로 만들어 주는 Claude Code 스킬입니다.**

인터뷰가 끝나면 손에 **OS 청사진 1장 + 첫 부품 결과물 1개**가 실제 파일로 남습니다.

- 여기서 **OS** = 컴퓨터 운영체제가 아니라, *내가 매일 켜서 내 일을 굴리는 개인 업무 시스템*입니다.
- 6단계 인터뷰(3 Phase): 풍경 → 통점 → 이상향 → 부품 매핑 → 첫 부품 결정 → 결과물.
- 중간에 끊겨도 **이어서** 할 수 있습니다(세션 상태 저장).

> 이 스킬은 MIT 라이선스로 공개된 [`selfishclub/os-interview-skill`](https://github.com/selfishclub/os-interview-skill)의 구조에서 출발해 재설계·확장했습니다. 저작권 관계는 [NOTICE.md](./NOTICE.md)를 참고하세요.

---

## 설치 (수강생용)

Claude Code에서 아래 한 줄이면 됩니다. 나머지는 Claude가 안내에 따라 설치합니다.

```
https://github.com/hapum0225/personal-os 이 스킬을 사용할 수 있는 상태로 세팅해줘
```

설치가 끝나면 이렇게 시작하세요:

```
내 OS를 만들고 싶어. personal-os 인터뷰 시작해줘
```

---

## Claude가 설치할 때 (Instructions for Claude) ⚙️

> 사용자가 이 저장소 URL로 "설치/세팅"을 요청하면, 아래 절차를 따르세요. **먼저 출처(이 GitHub 저장소)와 설치 범위를 사용자에게 확인받은 뒤** 진행합니다. 플러그인은 신뢰된 코드로 취급되므로, 설치 전에 사용자가 저장소를 확인하도록 안내하세요.

### 기본 경로 — 플러그인 마켓플레이스 (권장)

이 저장소는 Claude Code **플러그인 마켓플레이스**입니다. 표준 명령으로 설치합니다.

```bash
claude plugin marketplace add hapum0225/personal-os
claude plugin install personal-os@personal-os --scope user
```

- `personal-os@personal-os` = `<플러그인 이름>@<마켓플레이스 이름>` (둘 다 `personal-os`).
- 설치 후 현재 세션에 반영하려면 `/reload-plugins`를 실행하거나 Claude Code를 재시작하라고 안내하세요.
- 명령 플래그(`--scope` 등)는 Claude Code 버전에 따라 다를 수 있습니다. 최신 사용법은 `claude plugin --help`로 확인하세요.
- 설치 검증: `/plugin`(또는 `claude plugin list`)에 `personal-os`가 보이고, 스킬 `personal-os`가 발동 가능하면 성공입니다.

### 업데이트 / 제거

```bash
# 업데이트 (저장소에 새 버전이 올라온 뒤)
claude plugin marketplace update personal-os
# 필요 시 /reload-plugins

# 제거
claude plugin uninstall personal-os@personal-os
```

> 서드파티 마켓플레이스는 자동 업데이트가 기본 비활성일 수 있습니다. 업데이트는 위 명령으로 직접 수행하세요.

### 폴백 — 수동 설치 (플러그인 명령을 못 쓰는 환경)

플러그인 기능을 쓸 수 없을 때만 사용하세요. 스킬 폴더(`plugins/personal-os/skills/personal-os/`)를 개인 스킬 위치로 복사합니다. **`git clone`이 안 되면 GitHub에서 ZIP을 내려받아 압축을 풀어** 같은 폴더를 복사하세요.

**Windows (PowerShell):**
```powershell
$src  = "plugins/personal-os/skills/personal-os"   # 클론/압축해제한 저장소 안 경로
$dest = Join-Path $env:USERPROFILE ".claude\skills\personal-os"
New-Item -ItemType Directory -Force -Path (Split-Path $dest) | Out-Null
Copy-Item -LiteralPath $src -Destination $dest -Recurse -Force
```

**macOS / Linux (bash):** *(문서 제공 — 아직 실검증 전)*
```bash
mkdir -p ~/.claude/skills
cp -R plugins/personal-os/skills/personal-os ~/.claude/skills/personal-os
```

복사 후 새 세션에서 스킬 `personal-os`가 발동하는지 확인하세요. (심볼릭 링크는 쓰지 마세요.)

---

## 이 스킬이 원본보다 나아진 점

| 항목 | 원본 | personal-os |
|---|---|---|
| 설치 | 수동 파일 복사(안내 모순) | 표준 마켓플레이스 설치 + 수동 폴백 |
| 세션 중단 | 재개 불가 | **상태 파일로 이어서 진행** |
| 플랫폼 | macOS/Linux 전제 | Windows 지원(실검증) |
| 트리거 | 한국어 전용 | 한국어·영어 병기 + OS 오발동 방어 |
| 산출물 | 채팅 텍스트 | **실제 파일 생성 + 규격 검증** |
| 품질 검증 | 없음 | 재현 가능한 평가 세트 |

## 저장소 구조

```
personal-os/
├── .claude-plugin/marketplace.json     # 마켓플레이스 정의
├── plugins/personal-os/                # 설치되는 플러그인 (스킬 본체)
│   ├── .claude-plugin/plugin.json
│   ├── skills/personal-os/SKILL.md     # 인터뷰 본체
│   │   ├── templates/                  # A/B/C 결과물 골격
│   │   └── references/                 # 상태 규격·블루프린트·방법론
│   ├── LICENSE / NOTICE.md
├── examples/                           # 예제 (참고용)
├── evals/                              # 평가 세트
├── LICENSE / NOTICE.md / CHANGELOG.md
```

## 수강생이 만든 산출물의 권리

이 저장소의 MIT 라이선스가 여러분이 인터뷰에 입력한 내용에까지 자동으로 적용되는 것은 아닙니다. 생성된 산출물(청사진·스킬 등)의 이용·권리 관계는 적용 법률, 사용 중인 AI 서비스 약관, 산출물에 포함된 제3자 자료에 따라 달라질 수 있습니다. 산출물에 이 저장소의 템플릿이나 제3자 표현의 상당 부분이 포함되는 경우, 관련 고지를 확인하세요.

## 라이선스

[MIT](./LICENSE). 원본 `selfishclub/os-interview-skill`(MIT)의 구조에서 파생했습니다 — [NOTICE.md](./NOTICE.md).

## 검증 환경

- 테스트한 Claude Code 버전·OS는 릴리스 시 `evals/results/`에 기록합니다.
- 현재 검증: Windows 11 / Claude Code 2.1.x (설치·발동). macOS/Linux는 문서 제공(실검증 예정).
