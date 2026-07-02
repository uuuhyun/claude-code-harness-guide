# Claude Code 하네스 & 플러그인 가이드

Claude Code(및 호환 코딩 에이전트)의 **하네스·플러그인·확장 도구**를 실사용 관점에서 정리하는 한국어 카탈로그.
"이게 뭐고, 어떻게 설치하고, 어떻게 발동시키는가"를 일관된 템플릿으로 문서화한다.

> 🇬🇧 English summary: [README.en.md](README.en.md)

## 왜 이 저장소인가

이런 도구들을 검색하면 대부분 "링크 모음(awesome-list)"만 나온다. 하지만 실제로 써보면 **이것들은 서로 같은 부류가 아니다.** 어떤 건 설정을 통째로 까는 팩이고, 어떤 건 개발 방법론이고, 어떤 건 에이전트에 원래 내장된 기능이다. 이 저장소는 그 **층위(카테고리)를 먼저 구분**하고, 각 도구를 **설치 → 발동 → 주의사항**까지 붙여넣기 가능한 수준으로 정리한다.

## 카테고리(층위) 분류

| 층위 | 정체 | 예시 |
|---|---|---|
| **A. 하네스 팩** | `.claude/`에 에이전트·스킬·훅·명령을 통째로 까는 올인원 세팅 | gstack, ECC, revfactory/harness |
| **B. 방법론** | 개발 프로세스(스펙→계획→구현) 하나를 강제하는 워크플로우 | spec-kit |
| **C. 규율** | "스킬/절차를 반드시 먼저 쓰게" 만드는 규율 계층 | **superpowers** |
| **D. 네이티브** | 별도 설치 없이 에이전트에 내장된 기능 | ultracode |

## 카탈로그

| 하네스 | 카테고리 | 설치 난이도 | 검증 상태 | 한 줄 요약 |
|---|---|---|---|---|
| [superpowers](harnesses/superpowers.md) | C. 규율 | 쉬움 (플러그인) | ✅ 써봄 | 스킬을 먼저 쓰게 강제하는 규율 + 개발 스킬 14종 |

> 📌 **작성 예정**: gstack · spec-kit · ECC · revfactory/harness · ultracode.
> 조사 자료는 준비돼 있고, [TEMPLATE.md](TEMPLATE.md) 형식으로 순차 추가 예정.

## Codex 사용자를 위한 대응표

Codex에서 [lazycodex](https://github.com/code-yeongyu/lazycodex)(oh-my-openagent 계열) 같은 하네스를 쓰다가 Claude Code로 넘어온다면, 결이 비슷한 대응 도구는 다음과 같다.

| Codex 쪽 | Claude Code 대응 후보 | 성격 |
|---|---|---|
| lazycodex / oh-my-openagent | gstack, oh-my-claudecode(OMC) | 올인원 하네스 팩 |
| (규율/절차) | **superpowers** | 스킬 규율 계층 |
| (멀티에이전트 자동화) | ultracode (네이티브) | 내장 오케스트레이션 |

## 기여하기

새 하네스를 추가하려면 [TEMPLATE.md](TEMPLATE.md)를 복사해서 `harnesses/<이름>.md`로 채우면 된다.
자세한 절차는 [CONTRIBUTING.md](CONTRIBUTING.md) 참고.

## 라이선스

[MIT](LICENSE) © 2026 김유현 (uuuhyun)
