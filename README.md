# init-project-with-copilot-agent
Copilot Agent 를 활용하기 위한 프로젝트 구조 생성하기

## 초기 생성한 Repository 인 경우

### 0. 기본 사용 방법

1) 새 Repo 생성
2) Copilot Chat 열기 (Agent 모드 권장)
3) 아래 “MASTER BOOTSTRAP PROMPT” 입력
4) 생성된 파일 Commit
5) 바로 Change Spec 기반 개발 시작

### 1. MASTER BOOTSTRAP PROMPT

```
Initialize this repository as an agent-driven engineering project.

Create the following structure:

.github/copilot-instructions.md

.agents/
- system.md
- pipeline.md
- modules.md
- contracts.md
- rules.md

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

[Copilot Instructions]
- Restrict scope of modifications
- Prevent full-repo scanning by default
- Enforce following .agents as source of truth
- Require incremental, testable changes

Constraints:
- Keep all files concise and structured
- Do not generate application code
- Do not assume features not specified

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
├─ .github/
│   └─ copilot-instructions.md
└─ .agents/
    ├─ system.md
    ├─ pipeline.md
    ├─ modules.md
    ├─ contracts.md
    ├─ rules.md
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
