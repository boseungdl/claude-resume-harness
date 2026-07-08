<!-- OMC:START -->
<!-- OMC:VERSION:4.14.7 -->

# oh-my-claudecode - Intelligent Multi-Agent Orchestration

You are running with oh-my-claudecode (OMC), a multi-agent orchestration layer for Claude Code.
Coordinate specialized agents, tools, and skills so work is completed accurately and efficiently.

<operating_principles>
- Delegate specialized work to the most appropriate agent.
- Prefer evidence over assumptions: verify outcomes before final claims.
- Choose the lightest-weight path that preserves quality.
- Consult official docs before implementing with SDKs/frameworks/APIs.
</operating_principles>

<delegation_rules>
Delegate for: multi-file changes, refactors, debugging, reviews, planning, research, verification.
Work directly for: trivial ops, small clarifications, single commands.
Route code to `executor` (use `model=opus` for complex work). Uncertain SDK usage → `document-specialist` (repo docs first; Context Hub / `chub` when available, graceful web fallback otherwise).
</delegation_rules>

<model_routing>
`haiku` (quick lookups), `sonnet` (standard), `opus` (architecture, deep analysis).
Direct writes OK for: `~/.claude/**`, `.omc/**`, `.claude/**`, `CLAUDE.md`, `AGENTS.md`.
</model_routing>

<skills>
Invoke via `/oh-my-claudecode:<name>`. Trigger patterns auto-detect keywords.
Tier-0 workflows include `autopilot`, `ultrawork`, `ralph`, `team`, and `ralplan`.
Keyword triggers: `"autopilot"→autopilot`, `"ralph"→ralph`, `"ulw"→ultrawork`, `"ccg"→ccg`, `"ralplan"→ralplan`, `"deep interview"→deep-interview`, `"deslop"`/`"anti-slop"`→ai-slop-cleaner, `"deep-analyze"`→analysis mode, `"tdd"`→TDD mode, `"deepsearch"`→codebase search, `"ultrathink"`→deep reasoning, `"cancelomc"`→cancel.
Team orchestration is explicit via `/team`.
Detailed agent catalog, tools, team pipeline, commit protocol, and full skills registry live in the native `omc-reference` skill when skills are available, including reference for `explore`, `planner`, `architect`, `executor`, `designer`, and `writer`; this file remains sufficient without skill support.
</skills>

<verification>
Verify before claiming completion. Size appropriately: small→haiku, standard→sonnet, large/security→opus.
If verification fails, keep iterating.
</verification>

<execution_protocols>
Broad requests: explore first, then plan. 2+ independent tasks in parallel. `run_in_background` for builds/tests.
Keep authoring and review as separate passes: writer pass creates or revises content, reviewer/verifier pass evaluates it later in a separate lane.
Never self-approve in the same active context; use `code-reviewer` or `verifier` for the approval pass.
Before concluding: zero pending tasks, tests passing, verifier evidence collected.
</execution_protocols>

<hooks_and_context>
Hooks inject `<system-reminder>` tags. Key patterns: `hook success: Success` (proceed), `[MAGIC KEYWORD: ...]` (invoke skill), `The boulder never stops` (ralph/ultrawork active).
Persistence: `<remember>` (7 days), `<remember priority>` (permanent).
Kill switches: `DISABLE_OMC`, `OMC_SKIP_HOOKS` (comma-separated).
</hooks_and_context>

<cancellation>
`/oh-my-claudecode:cancel` ends execution modes. Cancel when done+verified or blocked. Don't cancel if work incomplete.
</cancellation>

<worktree_paths>
State: `.omc/state/`, `.omc/state/sessions/{sessionId}/`, `.omc/notepad.md`, `.omc/project-memory.json`, `.omc/plans/`, `.omc/research/`, `.omc/logs/`
</worktree_paths>

## Setup

Say "setup omc" or run `/oh-my-claudecode:omc-setup`.

<!-- OMC:END -->

## 이력서 하네스 규칙

이력서·자기소개서 작업은 `resume` 스킬(`.claude/skills/resume/SKILL.md`)의 3단계(분석→초안→퇴고)를 따른다.

- **단일 진실 원천**: 커리어·경력·자격은 `about-me/프로필-원천정보.md`, 프로젝트 사실은 `about-me/프로젝트-원천정보.md`. 모든 사실(수치·기간·자격·경험·역할)은 이 두 파일에서만 인출한다. 두 파일 모두 **직접 수정 금지** — 갱신은 사용자 확인 후에만. 콘텐츠 정직성 규칙은 프로필-원천정보.md 최상단 "LLM 사용 규칙" 섹션이 원본이며, 다른 곳에 복사하지 않고 매번 원본을 로드해 준수한다.
- **폴더 구조**: 공고별 작업은 `about-me/지원/{회사}-{직무}-{YYYYMM}/`의 00~03 파일 구조를 쓴다.
- **순서 강제**: `01-분석.md`가 없으면 이력서·자소서 초안을 작성하지 않는다 — 분석 단계로 유도한다.
- **자기승인 금지**: 퇴고는 작성 컨텍스트와 격리된 recruiter(screen)·editor 서브에이전트 패스로만 수행한다(OMC의 작성/검토 분리 원칙과 동일). 치명 지적이 남아 있으면 "제출가능" 판정을 내리지 않는다.
- recruiter/storyteller/essayist/copywriter/editor(`.claude/agents/`)는 OMC에 없는 채용 도메인 관점의 보완이며, OMC의 검증 체계를 대체하지 않는다. 자소서 초안 작성은 essayist(문항 유형별 주력 작성), 설득·공감 포장은 copywriter, 문장 퇴고는 editor로 역할이 분리된다.
