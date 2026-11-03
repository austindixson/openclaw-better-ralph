# Better Ralph – OpenClaw Skill

An **OpenClaw skill** that runs one [Better Ralph](https://github.com/snarktank/ralph) iteration using only standard OpenClaw tools. No Aether-Claw or external runner required.

---

## What it does

When you invoke the skill (e.g. "run better ralph" or "do one better ralph iteration"), the agent:

1. Reads `prd.json` and `progress.txt`
2. Picks the next story (highest priority with `passes: false`)
3. Ensures the git branch matches `prd.json.branchName`
4. Implements that one story
5. Runs quality checks (e.g. `npm test`, lint)
6. Commits with `feat: [Story ID] - [Story Title]` if checks pass
7. Updates `prd.json` to set `passes: true` for that story
8. Appends a progress block to `progress.txt`

All steps use normal OpenClaw tools: read file, write file, edit, exec, git. No custom APIs or runners.

---

## Requirements

- **OpenClaw** (or an OpenClaw-compatible agent that loads skills from SKILL.md)
- A project with a **prd.json** in the workspace root (see `prd.json.example`)

---

## Install

### Option 1: ClawHub (if available)

```bash
npx clawhub@latest install better-ralph
```

(Use the correct slug if this skill is published to ClawHub.)

### Option 2: Manual – global

Copy the skill into OpenClaw’s global skills directory:

```bash
cp -r skills/better-ralph ~/.openclaw/skills/
```

### Option 3: Manual – workspace

Copy into your project so only this workspace has the skill:

```bash
mkdir -p skills
cp -r skills/better-ralph your-project/skills/
```

**Priority:** OpenClaw typically loads workspace `skills/` over global `~/.openclaw/skills/`. See [OpenClaw Skills](https://docs.clawd.bot/tools/skills) for your version.

---

## Usage

In OpenClaw, say for example:

- "Run better ralph"
- "Do one better ralph iteration"
- "Implement the next story from the PRD"
- "Next prd story"

The agent will load the skill and run one iteration (one story). Repeat to complete all stories, or run your agent in a loop.

---

## prd.json

Put a `prd.json` in the project root. Copy from `prd.json.example` and edit:

- **userStories**: Each has `id`, `title`, `description`, `acceptanceCriteria`, `priority`, `passes`.
- **priority**: Lower number = higher priority (run first).
- **passes**: Start as `false`; the skill sets to `true` after a story is done.

---

## References

- [Ralph](https://github.com/snarktank/ralph) – Original PRD-driven loop (Amp / Claude Code)
- [Better Ralph](https://github.com/austindixson/better-ralph) – Docs and Aether-Claw runtime
- [OpenClaw Skills](https://docs.clawd.bot/tools/skills) – How OpenClaw loads skills
