# init-project-with-copilot-agent
Copilot Agent 를 활용하기 위한 프로젝트 구조 생성하기

## 이 README 사용 순서 (권장)

1) 신규 저장소라면, 상단의 "초기 생성한 Repository 인 경우"를 0 -> 6 순서로 진행한다.
2) 기존 저장소라면, "이미 작업이 진행중인 Repository 인 경우"를 1 -> 6 순서로 진행한다.
3) 두 경우 모두 마지막에 "추가 보완 내용" 섹션을 반영해 운영 규칙을 고정한다.
4) 실제 개발 세션에서는 AGENTS.md, CLAUDE.md, .agents/handoff.md, .agents/active-task.md를 항상 최신 상태로 유지한다.

## 초기 생성한 Repository 인 경우

### 0. 기본 사용 방법

1) 새 Repo 생성
2) Copilot Chat 열기 (Agent 모드 권장)
3) 아래 “MASTER BOOTSTRAP PROMPT” 입력
4) 생성된 파일 Commit
5) 바로 Change Spec 기반 개발 시작
6) 아래 파일이 모두 생성되었는지 확인 후 진행
  - AGENTS.md
  - CLAUDE.md
  - .agents/handoff.md
  - .agents/active-task.md
  - .agents/changes/

### 1. MASTER BOOTSTRAP PROMPT

```
Initialize this repository as an agent-driven engineering project.

Create the following structure:

.github/copilot-instructions.md

AGENTS.md
CLAUDE.md

.agents/
- system.md
- pipeline.md
- modules.md
- contracts.md
- rules.md
- handoff.md
- active-task.md

Requirements:

[System]
- Define clear system purpose and boundaries
- Keep it implementation-agnostic

[Architecture]
- Design modular structure with clear responsibilities
- Ensure components can evolve independently

[Contracts]
- Define API/data contracts even if not fully implemented
- Use simple, explicit structures

[Pipeline]
- Describe runtime/data flow in sequence form

[Rules]
- Enforce minimal-change principle
- Disallow unnecessary refactoring
- Require contract-first modifications
- Include session finalization rule:
  → persist decisions into .agents/changes/
- Include cross-agent handoff rule:
  → persist resumable state into .agents/handoff.md and .agents/active-task.md

[Copilot Instructions]
- Restrict scope of modifications
- Prevent full-repo scanning by default
- Enforce following .agents as source of truth
- Require incremental, testable changes

Constraints:
- Keep all files concise and structured
- Do not generate application code
- Do not assume features not specified
- Ensure Copilot Agent and Claude Code can resume each other's in-progress session

Goal:
Establish a stable foundation for long-term Copilot Agent usage.
```

### 2. 생성 후 정제(Refine) 프롬프트

```
Refine the generated .agents and copilot-instructions:

- Remove ambiguity
- Eliminate assumptions
- Align terminology across all files
- Ensure modules are independently implementable
- Strengthen rules to enforce minimal change behavior

Do not expand scope.
Only improve clarity and consistency.
```

### 3. Copilot 행동 교정 ( 안정화 프롬프트 )

```
From now on:

- Follow .agents as the single source of truth
- Apply minimal and localized changes only
- Do not refactor unrelated code
- Do not infer architecture beyond defined specifications
```

### 4. 첫 Change Spec 생성 ( 개발 시작용 )

```
Create an initial change specification in .agents/changes/.

Goal:
Bootstrap minimal project structure.

Constraints:
- Minimal scope
- No additional features
- Must be testable
```

### 5. 세션 종료 시 사용할 프롬프트

```
Finalize this session according to .agents/rules.md
```

### 6. 최종 생성 결과 구조

```
repo/
├─ AGENTS.md
├─ CLAUDE.md
├─ .github/
│   └─ copilot-instructions.md
└─ .agents/
    ├─ system.md
    ├─ pipeline.md
    ├─ modules.md
    ├─ contracts.md
    ├─ rules.md
    ├─ handoff.md
    ├─ active-task.md
    └─ changes/
```

## 이미 작업이 진행중인 Repository 인 경우

### 1. 현재 구조를 추출

먼저 핵심 엔트리포인트와 주요 서비스 파일 몇 개만 연 상태에서 시작하는 편이 좋습니다.

```
Analyze this existing repository and extract the current engineering structure.

Focus on:
- actual system purpose
- entry points
- major modules and responsibilities
- runtime/data flow
- existing API or data contracts
- external dependencies

Constraints:
- reflect only what already exists
- do not redesign architecture
- do not propose refactoring yet
- keep the result concise and implementation-grounded
```

### 2. .github/copilot-instructions.md 생성

```
Create .github/copilot-instructions.md for this existing repository.

Purpose:
Guide GitHub Copilot to work safely and predictably in a partially mature codebase.

Include:
- prefer minimal, localized changes
- do not refactor unrelated code
- do not scan the entire repository unless necessary
- follow existing architecture and naming patterns
- preserve current contracts unless explicitly changed
- prefer incremental, testable modifications
- when uncertain, align with existing implementation rather than inventing new patterns
- persist finalized decisions into .agents/changes/
- require cross-agent resumability via AGENTS.md, CLAUDE.md, .agents/handoff.md, and .agents/active-task.md

Keep it concise, strict, and repository-wide.
Do not include generic advice unrelated to this codebase.
```

### 3. .agents/ 생성

```
Based on the extracted repository structure, generate an .agents reference structure for this existing project.

Create:

.agents/
- system.md
- pipeline.md
- modules.md
- contracts.md
- rules.md
- handoff.md
- active-task.md

Requirements:
- reflect the current implementation only
- do not invent features or target architecture
- system.md: define purpose and boundaries
- pipeline.md: describe current runtime/data flow
- modules.md: describe major modules and responsibilities
- contracts.md: capture current API/data contracts
- rules.md: define safe Copilot working rules for this repository

Keep all files concise and operational.
These files should help Copilot follow the existing codebase safely.
```

### 4. 생성 결과 검증

```
Validate the generated .github/copilot-instructions.md and .agents files against the current repository.

Check for:
- incorrect assumptions
- missing key modules
- mismatched terminology
- contract mismatches
- invented architecture not present in code

Constraints:
- refine only
- do not expand scope
- keep existing structure
```

### 5. rules.md 강화

```
Refine .agents/rules.md for GitHub Copilot Agent usage in an existing repository.

Include strict operational rules:
- minimal-scope changes only
- no unrelated refactoring
- preserve existing contracts by default
- align with established patterns before introducing new ones
- create or update .agents/changes/ records for finalized work
- prefer small, reviewable modifications
- when session is interrupted (e.g., token limit), write resumable handoff to .agents/handoff.md and update .agents/active-task.md

Make the rules short, strict, and actionable.
```

### 6. Change Spec 방식 도입

```
Create the first change specification in .agents/changes/ for a small, safe improvement in this repository.

Requirements:
- choose a low-risk, isolated change
- keep scope minimal
- reference current architecture and contracts
- make it suitable for GitHub Copilot Agent execution
```

## 추가 보완 내용

### agent 가 수정 완료 후 내부 문서를 업데이트하도록 보완

.github/copilot-instructions.md 에 추가

```
## 작업 완료 규칙 (Definition of Done)
코드 변경이 발생한 모든 작업은 종료 전에 반드시 아래를 수행한다.
1. .agents 문서(system/modules/pipeline/contracts/rules 및 changes) 중 영향 범위를 업데이트한다.
2. README.md의 사용자 관점 영향(설치/실행/설정/기능)이 있으면 반영한다. 필요시 requirements.txt도 업데이트한다.
3. 최종 보고 시 문서 반영 여부를 함께 보고한다.
```

### Copilot Agent와 Claude Code 병행 사용

두 Agent가 같은 저장소를 안전하게 이어서 작업할 수 있도록 아래 규칙을 추가합니다.

공유 원칙

1) .agents 문서를 단일 기준으로 사용한다.
2) 에이전트별 채팅 이력은 상태 저장소가 아니며, 상태는 반드시 파일로 남긴다.
3) 세션 종료 또는 token 소진 전에 .agents/handoff.md 와 .agents/active-task.md 를 최신화한다.
4) 완료된 의사결정은 .agents/changes/ 에 기록한다.

### 추가 파일 구조

```
repo/
├─ AGENTS.md
├─ CLAUDE.md
├─ .github/
│  └─ copilot-instructions.md
├─ .agents/
│  ├─ system.md
│  ├─ pipeline.md
│  ├─ modules.md
│  ├─ contracts.md
│  ├─ rules.md
│  ├─ handoff.md
│  ├─ active-task.md
│  └─ changes/
└─ .claude/
   ├─ agents/
   │  ├─ planner.md
   │  ├─ implementer.md
   │  └─ reviewer.md
   └─ commands/
      ├─ continue.md
      └─ finalize.md
```

### AGENTS.md 권장 템플릿

신규/기존 저장소 모두 아래 템플릿을 기본값으로 사용하면 됩니다.

```markdown
# AGENTS.md

This repository uses .agents/ as the shared source of truth for AI coding agents.

Before starting any task:
1. Read .agents/system.md
2. Read .agents/modules.md
3. Read .agents/contracts.md
4. Read .agents/rules.md
5. Read .agents/active-task.md if it exists
6. Read .agents/handoff.md if continuing previous work

Core rules:
- Make minimal, localized changes.
- Do not refactor unrelated code.
- Preserve existing contracts unless explicitly changed.
- Update .agents/changes/ after finalized work.
- Update .agents/handoff.md before ending a session.
- Keep .agents/active-task.md aligned with current scope and acceptance criteria.
```

### CLAUDE.md 권장 템플릿

Claude Code가 공통 상태 파일을 읽고 이어받도록 아래 템플릿을 기본값으로 사용합니다.

```markdown
# CLAUDE.md

@AGENTS.md
@.agents/system.md
@.agents/pipeline.md
@.agents/modules.md
@.agents/contracts.md
@.agents/rules.md
@.agents/handoff.md
@.agents/active-task.md

## Claude Code Rules

- Use .agents/ as the source of truth.
- When continuing interrupted work, read .agents/handoff.md first.
- Before editing files, summarize current task and planned changes.
- After meaningful edits, update .agents/handoff.md.
- Keep .agents/active-task.md in sync with current progress.
- Do not create new architecture unless explicitly requested.
```

### Copilot에서 Claude Code로 작업 인계하기

1) Copilot Agent가 변경 작업을 수행한다.
2) 중단 전 .agents/handoff.md 에 완료/미완료/다음 단계/검증 결과를 기록한다.
3) .agents/active-task.md 의 목표/범위/수용 기준을 최신 상태로 맞춘다.
4) 완료 의사결정은 .agents/changes/ 에 반영한다.
5) Claude Code는 CLAUDE.md -> AGENTS.md -> .agents/handoff.md -> .agents/active-task.md 순서로 읽고 이어서 작업한다.

Copilot Agent -> Claude Code 인계 프롬프트 예시

```
Continue this task using AGENTS.md and .agents/ as the source of truth.

Read first:
- CLAUDE.md
- AGENTS.md
- .agents/handoff.md
- .agents/active-task.md
- .agents/rules.md
- related .agents/changes/*

Requirements:
- Do not redo completed work
- Preserve existing decisions and contracts
- Apply minimal, localized changes only
- After completion, update .agents/handoff.md, .agents/active-task.md, and .agents/changes/
```

### Claude Code에서 중단 작업 이어받기

1) CLAUDE.md 를 먼저 읽는다.
2) AGENTS.md 와 .agents/rules.md 를 읽어 공통 제약을 확인한다.
3) .agents/handoff.md 와 .agents/active-task.md 기준으로 미완료 항목만 진행한다.
4) 완료 시 handoff와 changes를 갱신하고, 다음 에이전트가 바로 실행 가능한 상태를 남긴다.

Claude Code -> Copilot Agent 인계 프롬프트 예시

```
Resume implementation from the latest shared state.

Read first:
- AGENTS.md
- .agents/handoff.md
- .agents/active-task.md
- .agents/rules.md
- related .agents/changes/*

Requirements:
- Continue from remaining items only
- Keep architecture/contracts unchanged unless explicitly required
- Make incremental, testable edits
- Finalize by updating .agents/handoff.md, .agents/active-task.md, and .agents/changes/
```

### 세션 종료 시 Handoff 작성 규칙

아래 형식을 최소 기준으로 사용합니다.

```
# Handoff

## Current Status
- State: in-progress | blocked | done
- Last agent: Copilot Agent | Claude Code
- Last updated: YYYY-MM-DD HH:mm

## Current Goal
-

## Completed
-

## In Progress
-

## Next Steps
1.
2.
3.

## Modified Files
-

## Important Decisions
-

## Known Issues
-

## Validation
- Build:
- Test:
- Manual check:
```

.github/copilot-instructions.md 보강 권장 문구

```
## Claude Code Handoff Rule

When a session is likely to end or after any meaningful change:
1. Update .agents/handoff.md.
2. Record completed work, remaining work, changed files, and validation status.
3. Do not rely on chat history as the only source of progress.
4. Ensure Claude Code can continue the work by reading CLAUDE.md and .agents/handoff.md.
```

.agents/rules.md 보강 권장 문구

```
## Multi-Agent Continuity Rules

- .agents/ is the shared state layer between Copilot Agent and Claude Code.
- Agent chat history is not considered persistent project state.
- All finalized decisions must be written to .agents/changes/.
- All unfinished work must be written to .agents/handoff.md.
- Before continuing work, read .agents/handoff.md and .agents/active-task.md.
```

## 세션 운영 체크리스트

세션 시작

1) AGENTS.md를 읽고 공통 규칙을 확인한다.
2) .agents/handoff.md와 .agents/active-task.md를 읽고 현재 상태를 확인한다.

세션 진행

1) 최소 범위 변경만 수행한다.
2) 완료된 결정은 .agents/changes/에 누적한다.

세션 종료 또는 token 소진 직전

1) .agents/handoff.md에 완료/미완료/다음 단계/검증 상태를 업데이트한다.
2) .agents/active-task.md를 현재 목표와 범위에 맞게 갱신한다.
3) 다음 Agent가 바로 실행 가능한 next step 문장을 handoff에 남긴다.

## 인계 프롬프트 파일 표준 절차

상황마다 프롬프트를 새로 작성하지 않고, 고정 프롬프트 파일 + handoff 상태 갱신 방식으로 운영합니다.

표준 원칙

1) 고정 문장(규칙/절차)은 파일로 관리한다.
2) 가변 문장(현재 작업 상태)은 .agents/handoff.md 와 .agents/active-task.md 에 기록한다.
3) 에이전트는 프롬프트 파일을 실행하기 전에 handoff/active-task를 먼저 읽는다.
4) 인계 방향이 Copilot -> Claude, Claude -> Copilot 중 어느 쪽이든 같은 상태 파일을 사용한다.

권장 파일

1) .claude/commands/continue.md
2) .claude/commands/finalize.md
3) .agents/prompts/copilot-continue.md
4) .agents/prompts/copilot-finalize.md

.claude/commands/continue.md 템플릿

```markdown
Read first:
- CLAUDE.md
- AGENTS.md
- .agents/handoff.md
- .agents/active-task.md
- .agents/rules.md
- related .agents/changes/*

Continue from remaining items only.

Rules:
- Keep changes minimal and localized.
- Preserve existing contracts unless explicitly changed.
- Do not redo completed work.

Before finishing:
- Update .agents/handoff.md
- Update .agents/active-task.md
- Append finalized decisions to .agents/changes/
```

.claude/commands/finalize.md 템플릿

```markdown
Finalize this session using .agents/rules.md.

Required updates before ending:
1. Update .agents/handoff.md with completed/in-progress/next steps/validation.
2. Sync .agents/active-task.md with latest scope and acceptance criteria.
3. Record finalized decisions in .agents/changes/.

Output format:
- What was completed
- What remains
- Validation status
- Exact next step for the next agent
```

.agents/prompts/copilot-continue.md 템플릿

```markdown
Continue from shared handoff state.

Read first:
- AGENTS.md
- .agents/handoff.md
- .agents/active-task.md
- .agents/rules.md
- related .agents/changes/*

Requirements:
- Continue from remaining items only.
- Keep changes minimal and localized.
- Preserve contracts unless explicitly changed.

Before finishing:
- Update .agents/handoff.md
- Update .agents/active-task.md
- Append finalized decisions to .agents/changes/
```

.agents/prompts/copilot-finalize.md 템플릿

```markdown
Finalize this session according to .agents/rules.md.

Required updates:
1. Update .agents/handoff.md with completed/in-progress/next steps/validation.
2. Sync .agents/active-task.md with current scope and acceptance criteria.
3. Record finalized decisions in .agents/changes/.

Return:
- Completed work
- Remaining work
- Validation status
- Exact first step for the next agent
```

인계 방향별 사용 방법

1) Copilot -> Claude: Copilot 종료 직전에 copilot-finalize 프롬프트를 사용한다.
2) Copilot -> Claude: Claude 시작 시 .claude/commands/continue.md를 사용한다.
3) Claude -> Copilot: Claude 종료 직전에 .claude/commands/finalize.md를 사용한다.
4) Claude -> Copilot: Copilot 시작 시 copilot-continue 프롬프트를 사용한다.

Copilot에서도 같은 방식으로 적용

1) Copilot Chat 시작 시 AGENTS.md + .agents/handoff.md + .agents/active-task.md를 먼저 읽도록 지시한다.
2) 세션 종료 시 finalize 프롬프트와 동일한 체크리스트를 적용한다.
3) 핵심은 프롬프트 자체보다 handoff/active-task 최신화이다.
