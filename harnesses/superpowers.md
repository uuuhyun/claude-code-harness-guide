# Superpowers

> Claude Code(및 여러 코딩 에이전트)에 "스킬을 반드시 먼저 쓰게" 강제하는 규율 계층 + 재사용 가능한 개발 스킬(브레인스토밍·TDD·체계적 디버깅·코드리뷰 등) 묶음.

| 카테고리 | 제작자 | 라이선스 | 지원 에이전트 | 검증 상태 | 최종 업데이트 |
|---|---|---|---|---|---|
| C. 규율 | Jesse Vincent ([obra](https://github.com/obra)) | MIT | Claude Code, Codex(App/CLI), Cursor, Gemini CLI, GitHub Copilot CLI, OpenCode, Kimi, Antigravity, Factory Droid, Pi | ✅ 써봄 (v6.0.2) | 2026-07-02 |

## 1. 소개

Superpowers는 코딩 에이전트를 위한 **하나의 개발 방법론**을 "합성 가능한 스킬(skill) 묶음 + 그 스킬을 반드시 쓰게 만드는 초기 지침"으로 구현한 플러그인이다. 에이전트가 뭔가 만들려는 순간 바로 코드부터 짜지 않고, **한발 물러나 요구사항을 캐묻고(brainstorming) → 계획을 세우고(writing-plans) → 승인받은 뒤 → 서브에이전트로 실행하고(subagent-driven-development) → 완료 전 실제로 검증(verification-before-completion)** 하도록 흐름을 잡아 준다.

이 저장소 분류상 **C. 규율**에 속한다. gstack·ECC 같은 "설정 팩(A)"이 에이전트·명령을 통째로 까는 것과 달리, superpowers는 무엇을 만들지보다 **"어떻게 일하게 만들 것인가"** 라는 규율을 얹는 계층이기 때문이다.

번들된 스킬(14개): `brainstorming`, `writing-plans`, `executing-plans`, `subagent-driven-development`, `dispatching-parallel-agents`, `test-driven-development`, `systematic-debugging`, `verification-before-completion`, `requesting-code-review`, `receiving-code-review`, `finishing-a-development-branch`, `using-git-worktrees`, `writing-skills`, `using-superpowers`.

## 2. 설치

전제조건: Claude Code CLI.

```bash
# Claude Code 안에서 (슬래시 명령)
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

- 사용자(user) 스코프로 설치되어 **모든 프로젝트/디렉토리에 전역 적용**된다.
- 다른 에이전트(Codex·Cursor·Gemini 등)는 각 플랫폼별 설치법이 다르다 → 공식 저장소의 Quickstart 참고.

## 3. 발동·사용법

**발동 방식 — "자동"의 실체를 알아두자.**

| 트리거 | 하는 일 |
|---|---|
| SessionStart 훅 (세션 시작·`/clear`·`/compact` 시 자동) | `using-superpowers` 지침을 컨텍스트에 자동 주입 → "관련 스킬이 있으면 먼저 발동하라"고 에이전트에 지시 |
| `/superpowers:<skill>` | 특정 스킬을 명시적으로 호출 (예: `/superpowers:brainstorming`) |
| 자연어 | 상황이 맞으면 에이전트가 스스로 스킬을 발동 (예: "이 기능 만들자" → brainstorming) |

> ⚠️ **핵심**: 훅이 자동으로 하는 일은 "스킬을 쓰라는 **지침 주입**"까지다. `brainstorming`·`TDD` 같은 **개별 스킬의 실제 실행은 에이전트(모델)의 판단**에 달려 있다. 그래서 조용히 발동되면 겉으로는 티가 안 나고, "자동인데 잘 안 느껴진다"는 인상을 준다. 확실히 쓰고 싶으면 `/superpowers:<skill>`로 직접 부르거나 아래처럼 말로 유도하면 된다.

**프롬프트 예시**

```text
# 1) 기능 설계를 브레인스토밍부터 — 바로 코드 짜지 말고 요구사항부터 캐물어줘
brainstorming 스킬 써서 "외국인 로컬버디 매칭" 기능의 요구사항과 설계부터 같이 정리하자.
```

```text
# 2) 버그를 체계적으로 — 추측으로 고치지 말고 원인부터
이 테스트가 간헐적으로 실패해. systematic-debugging 스킬대로 원인을 먼저 좁혀줘.
```

```text
# 3) "다 됐다"고 말하기 전에 실제 검증
구현 끝났다고 하기 전에 verification-before-completion 스킬대로
실제로 돌려서 통과하는지 근거를 보여줘.
```

## 4. 언제 쓰나 / 언제 안 쓰나

- **쓰면 좋을 때**
  - 코드부터 짜고 보는 습관을 막고 "요구사항 → 계획 → 승인" 규율을 강제하고 싶을 때
  - 디버깅·검증·코드리뷰 절차를 일관되게 유지하고 싶을 때
  - 여러 독립 태스크를 서브에이전트로 병렬 실행하고 싶을 때
- **안 쓰는 게 나을 때**
  - 단순 조회/질문 (매칭되는 스킬이 없어 어차피 조용함)
  - 이미 자체 워크플로우 규칙(예: 개인 CLAUDE.md의 정제→계획→승인)이 강하게 잡혀 있어 역할이 겹칠 때 → 겹치는 스킬은 접고 디버깅·검증·리뷰처럼 빈칸을 메우는 스킬만 살리는 편이 낫다

## 5. 주의 · 트레이드오프

- **우선순위**: 플러그인 스스로 "사용자 지침 > superpowers 스킬 > 기본 동작"이라고 명시한다. 개인 지침(CLAUDE.md/AGENTS.md)이 항상 우선이다.
- **다른 하네스와 충돌 가능**: A층 설정 팩(gstack·ECC 등)과 동시에 깔면 SessionStart 훅·스킬 이름·명령이 겹칠 수 있다. 한 번에 하나만 쓰는 것을 권장.
- **재주입 타이밍**: 지침은 세션 시작/`/clear`/`/compact` 때만 다시 들어온다. 아주 긴 세션 중반에는 존재감이 옅어질 수 있다.
- **체감 문제**: 위 3번의 경고처럼, 개별 스킬 실행이 모델 재량이라 "켜져 있는데 안 도는 것처럼" 보일 수 있다.

## 6. 함께 보기

- **gstack** (A. 하네스 팩) — 역할 기반 올인원 팩. superpowers가 "규율"이라면 gstack은 "팀 세팅".
- **ECC** (A. 하네스 팩) — 스킬·메모리·훅을 대규모로 얹는 팩. 규율 계층과 겹칠 수 있으니 병행 주의.
- **ultracode** (D. 네이티브) — Claude Code 내장 멀티에이전트 오케스트레이션. superpowers의 `subagent-driven-development`/`dispatching-parallel-agents`와 결이 비슷.

## 7. 출처

- 공식 저장소: https://github.com/obra/superpowers
- 마켓플레이스: https://github.com/obra/superpowers-marketplace
- 플러그인 메타: `superpowers@superpowers-marketplace` v6.0.2 (author: Jesse Vincent / jesse@fsck.com, MIT)
