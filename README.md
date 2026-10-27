# Plan Optimizer

An agent skill that turns a vague idea, rough plan, strategy, or prompt into a clear, stress-tested, actionable version. It scores the input, closes intent gaps, offers real alternatives, runs an adversarial audit, and returns a ready-to-use artifact.

Works on product features, research directions, business plans, agent instructions, roadmaps, and one-off prompts.

## What it does

1. **Classify and score** — idea / plan / prompt / strategy, rated 1–10 on clarity, specificity, completeness, actionability, and risk awareness.
2. **Extract intent** — asks only the questions that change the outcome: success, audience, constraints, non-goals, failure modes.
3. **Generate approaches** — two or three genuine alternatives with trade-offs, plus a recommendation; waits for a pick.
4. **Adversarial audit** — hunts contradictions, untestable acceptance criteria, missing edge cases, oversized scope, unsafe assumptions, and unguarded irreversible actions. Each finding gets severity, evidence, and a patch.
5. **Deliver** — analysis, optimized artifact, open questions, next step.

It also works in quick mode: stop after the audit and skip the rewrite.

## Install

The skill is a folder with a `SKILL.md`. It ships as two archives in this repo; extract one, then copy the folder into your agent's skills directory:

```bash
tar -xf plan-optimizer-skill-aio.tar -C /tmp

# OpenCode
mkdir -p ~/.config/opencode/skills && cp -r /tmp/plan-optimizer ~/.config/opencode/skills/

# Claude Code
mkdir -p ~/.claude/skills && cp -r /tmp/plan-optimizer ~/.claude/skills/
```

Or install the single-file package directly:

```bash
unzip plan-optimizer.skill -d ~/.config/opencode/skills/
```

Restart the agent. The skill triggers on phrases like "optimize this plan", "critique this approach", "improve this idea", or whenever a plan or prompt needs structure.

## Files

| Path | Contents |
|---|---|
| `SKILL.md` | Trigger description, five-step workflow, output template, heuristics |
| `references/scoring-and-frameworks.md` | Scoring rubric and framework selection |
| `references/audit-checklist.md` | Adversarial audit checklist |
| `references/examples.md` | Worked examples |
| `evals/evals.json`, `evals/triggers.json` | Evaluation cases and trigger tests (in the `.tar`) |
| `plan-optimizer.skill` | Zip-packaged skill |
| `plan-optimizer-skill-aio.tar` | Full source bundle |

## Example

```
You:  Optimize this plan: build a Chrome extension that summarizes tabs.
Agent: Scores (clarity 4, specificity 3, ...) → asks what "summarize" means and
       who it's for → offers 3 approaches (local model, API, hybrid) →
       finds 6 audit issues (permissions, cost, privacy, ...) →
       returns a rewritten plan with success criteria and verification steps.
```

## Design notes

- Never invents domain facts about the user; uses `[you fill this in: ...]` placeholders instead.
- Prefers the existing structure when the input is already decent.
- Optimized output is shorter and denser than the input unless the input was incomplete.
- For agent-facing plans it adds explicit verification steps and stop conditions.

## License

MIT © 2026 TonyD2F — see `LICENSE`.
